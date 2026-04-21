# Penn Ball

## Introduction
The goal of PennBall is to provide a comprehensive, easy to use analytical and statistical
reference platform of the NBA for NBA fans, Ballers, casual viewers and professionals alike. By
offering detailed insights and allowing for somewhat quantitative analysis on players and teams
with a wide array of historic and recent data, we would like to help our users better understand
the progression and development of game strategies and player skill sets.

The current landscape of basketball statistics websites and basketball media often leaves users
wanting more from their data interactions. Some common issues our team aims to address
include:
- Static Data Interaction: A lot of websites do not allow users to interact with the data
beyond basic sorting and filtering.
- Limited Data Scope: Most websites lack a comprehensive coverage of both historical
and recent data.
- Lack of Clarity: Some of the professional analytical websites and tools are way too
complex and convoluted to navigate and understand.
- Boring to use and look at: A lot of websites don’t enhance their user interfaces and users
are often looking at default html formatted tables with little ways to interact with.

Therefore, our application functionalities specifically target these shortcoming by implementing:

- Interactive Dashboards: Allows users to interact with data through dynamic graphs,
images, tables and search bars.
- Broad Data Integration: Including extensive datasets that cover multiple decades of NBA
games.
- Simplistic Interface Design: The platform incorporates multiple interface levels connected
through a simplified overview dashboard.
- Interesting Data Categories and Aesthetic UI: Application provides many unique data
categories to explore as well as plenty of images and photos to look at.

## Architecture

### Technologies Used
- Front-end UI: ReactJS
- Back-end: NodeJS
- Database: MySQL hosted on AWS RDS
- Data processing: Python with BeautifulSoup

### Page Descriptions
Regardless of page, the top navbar includes buttons/links to the players/teams page, as well as
a search bar that allows users to search for a specific player, which they can click on to access
the specific player page. This search query streams live based on what the user is typing, using
the fetch() Javascript function.

**Our website consist of four primary pages, as follows:**

Players: This page is reachable through the /players url. It shows a table of players, which by
default includes players’ names, headshots, stats, points, position, college, country, and team. It
is also organized by ppg by default. Users can click on players listed to access a specific player
page.
The user has the option of pressing a button on this page to change the organization of the
table to be by variance, which shows players ranked by the variance in ppg. This allows fans to
evaluate which players have greatest variance in game-to-game performances. The user can
also organize the page by “top pairs,” which organizes the table by pairs of players who have
had the most exciting matchups. This allows fans to see what future games might be most
exciting.

Specific player: This page is reachable through the /players/[:player_id] url. It shows a specific
player’s general details, headshot, stats, as well as performances in the ten most recent games.
It allows fans to see a player’s overall performance and stats as well as more recent trends in
their performance.

Teams: This page is reachable through the /teams url. It shows all NBA teams as well as their
respective conference, division, and some more complex stats about their toughest opposing
player, the average points scored by their toughest opposing player, and the percentage of
games won by the team given it scores a higher FG % than its opponent. This allows fans to
see the general stats about teams, the players each team should look out for, and how
important shooting well is to a team’s performance. Users can click on teams listed to access a
specific team page.

Specific team: This page is reachable through the /teams/[:team_id] url. It shows a specific
team’s conference and division, as well as a table of its players. The table of players includes
the players’ names, headshots, stats, positions, country, and college. Users can click on each
player to access the specific player page.

## Data

### Data sets:
**https://github.com/swar/nba_api**: This dataset contains data from the NBA.com website and
includes a vast array of data on player stats, game events, team stats, and more. Data on all
active players, and all games. Around ~110,000 Game data points. To retrieve data, we called
APIs to generate CSV files in Google Collab.

**https://www.sports-reference.com/cbb/**: This dataset contains data from college basketball
games and includes players stats and team records. We found the dataset online after
searching for NCAA basketball data. We scraped the dataset using BeautifulSoup and other
packages in Python.

Pre-processing: To populate the games table, we had to parse the match up column to retrieve
the home and away team. Specifically, the match up includes two teams separated by either @
or vs. We cased in both, to retrieve the home and away team’s IDs and created columns for
TEAM_ID and OTHER_TEAM_ID. To create the PlayerStats table, we also computed the field
goal percentage, 3 point percentage, and free throw percentage, since we were given the made
shots and attempted shots for each of those shot categories. This way, if we were ever
interested in these particular attributes, we handle the computation beforehand, and we can just
retrieve it with a SQL call, without computation. To populate the teams table, we manually
created a hashmap since the Division and Conference information was not included in the data
we were drawing from. But since this information is publicly available, we created a hashmap
with 32 keys, mapping to conference and division tuples, which we then applied to generate a
table including this information. Additionally, we created two tables for caching in the below
queries. We created a Players Pair table and a Division Tuples table which sped up complex
queries #1 and #5 respectively. The schemas are described more in the query section.

## Database

<img width="1012" height="456" alt="Screenshot 2026-04-21 at 5 59 52 PM" src="https://github.com/user-attachments/assets/0ebd2b7e-f2d4-40e7-af25-c27b14181fb3" />

