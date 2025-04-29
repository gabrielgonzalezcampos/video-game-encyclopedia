# Video Game Multidimensional Database

Forked from [Trung Hoang video-game-encyclopedia project](https://github.com/trung-hn/video-game-encyclopedia)

## Description

This project is an enhanced version of the original RAWG video games dataset, transformed into a multidimensional data model that facilitates complex analysis. Unlike the original dataset that consolidated all information into a single CSV file, this version implements a star schema with a central fact table (`games.csv`) and multiple related dimensional tables, optimized for advanced analytical queries.

## Data Structure

### Main Fact Table
- **games.csv**: Contains basic information about each game (core metrics and attributes)

### Dimensional Tables
- **game_developers.csv**: Developers of each game
- **game_genres.csv**: Genres associated with each game
- **game_metacritic_platforms.csv**: Platform-specific Metacritic scores
- **game_platforms.csv**: Available platforms for each game and their requirements
- **game_publishers.csv**: Publishers of each game
- **game_ratings.csv**: Detailed breakdown of ratings by category
- **game_status.csv**: Game status statistics (completed, abandoned, etc.)
- **game_stores.csv**: Stores where each game is available
- **game_tags.csv**: Descriptive tags associated with each game

### Derived Metrics
- **game_derived_metrics.csv**: Calculated indicators that enrich the analysis:
  - `completability_index`: Ratio between beaten / (beaten + dropped)
  - `consensus_score`: Score combining professional and user ratings
  - `time_rating_ratio`: Cost per hour of gameplay
  - `platform_diversity_index`: Cross-platform availability
  - `acquisition_play_ratio`: Ratio between acquisition and effective play

## Directory Structure

```
.
|-- src
|   |-- Generate_csv.ipynb
|   |-- Get_game_id.ipynb
|   |-- Get_game_info.ipynb
|   `-- Combine_game_info.ipynb
|
`-- data
    |-- csv
    |   |-- game_id.csv
    |   |-- game_info.csv
    |   |-- games.csv
    |   |-- game_developers.csv
    |   |-- game_genres.csv
    |   |-- game_metacritic_platforms.csv
    |   |-- game_platforms.csv
    |   |-- game_publishers.csv
    |   |-- game_ratings.csv
    |   |-- game_status.csv
    |   |-- game_stores.csv
    |   |-- game_tags.csv
    |   |-- game_derived_metrics.csv
    |-- game_id
    |   |-- 1.json
    |   |-- 2.json
    |   `-- *.json
    |
    `-- game_info
        |-- 1.json
        |-- 2.json
        `-- *.json
```

## Getting Started

1. Install dependencies:
```
pip install -r requirements.txt
```

## Steps to Replicate the Multidimensional Dataset:

1. Run `Get_game_id.ipynb`: Retrieves IDs for all games available on the RAWG API.
2. Run `Get_game_info.ipynb`: Downloads detailed information for each game using the IDs obtained in the previous step.
3. Run `Generate_csv.ipynb`: Process all the data from previous step to build the multidimensional model, generating the 11 final tables.

## Tips

Due to the high volume of data, it's recommended to save the data from steps 1 and 2 in a fast storage device, like an M.2 drive.

## Fact Table and Dimensions

### Main Fact Table (games.csv)
| Variable | Type | Description |
|----------|------|-------------|
| id | Numeric | Unique game identifier |
| slug | Text | URL-friendly identifier |
| name | Text | Game name |
| released | Date | Release date |
| metacritic | Numeric | Metacritic score (0-100) |
| rating | Numeric | Average user rating (0-5) |
| rating_top | Numeric | Maximum rating received |
| playtime | Numeric | Average time to complete the game (hours) |
| esrb_rating | Categorical | Age classification |
| description_short | Text | Brief game description |
| website | URL | Official website |
| added | Numeric | Total users who added the game |
| screenshots_count | Numeric | Number of screenshots available |
| background_image | URL | Cover image |
| metacritic_url | URL | Link to Metacritic page |
| tba | Boolean | Indicates if it's "to be announced" |
| updated | Date | Last information update |

### Dimensions (Reference Tables)
Each dimensional table contains specific attributes and is linked to the fact table through the `game_id` field.

## Advantages of the Multidimensional Model

1. **Facilitates Complex Analysis**: Allows aggregations, filtering, and drill-downs across multiple dimensions.
2. **Optimizes Storage**: Reduces data redundancy by normalizing information.
3. **Improves Performance**: More efficient for analytical queries than a flat model.
4. **Enables Multidimensional Analysis**: Ideal for BI tools and advanced visualization.
5. **Enables Derived Metrics**: Facilitates calculation of KPIs and complex indicators.

## Use Cases

- Analysis of trends in the video game industry
- Study of the relationship between critical ratings and popularity
- Comparisons between genres, platforms, and developers
- Analysis of user behavior (purchase vs. completion)
- Creation of recommendation systems based on multiple factors

## Important Notes

- The model is optimized for OLAP analysis, not for transactional operations.
- Derived metrics allow discovering insights beyond raw data.
- The star schema facilitates integration with BI tools such as Tableau, Power BI, or web visualization platforms.

## Limitations

- The RAWG API has a limit of 500,000 page views per month.
- The complete extraction and transformation process can take several hours due to the volume of data.

## Acknowledgements

- To [RAWG](https://rawg.io/) for providing a robust and comprehensive API
- To [Trung Hoang](https://github.com/trung-hn) for the original project

## Inspiration

This multidimensional model allows for more sophisticated analysis of the video game industry, facilitating the extraction of valuable insights about trends, user preferences, and market behaviors.

## License

### Code

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

### Dataset
The multidimensional dataset (all CSV files) is licensed under **CC BY-NC-SA 4.0** (Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International).

This means:
- **BY** — You must give appropriate credit, provide a link to the license, and indicate if changes were made
- **NC** — You may not use the material for commercial purposes
- **SA** — If you remix, transform, or build upon the material, you must distribute your contributions under the same license as the original

For more details on this license, see [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).