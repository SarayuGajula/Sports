PHASE 1: Core Functionality
Goal: Lay the foundation for processing and handling odds data.
Methods for OddsCalculator: american_to_decimal(american_odds):,
                            decimal_to_american(decimal_odds):,
                            calculate_implied_probability(odds, odds_format="decimal"),
                            calculate_no_vig_probabilities(implied_probs),
                            calculate_vig(implied_probs),
                            convert_odds(odds, from_format="american", to_format="decimal")
Methods for OddsDataHandler: __init__, load_data(self, odds_data), get_events(self)
                            filter_events_by_sport(self, sport_key),
                            filter_events_by_bookmaker(self, bookmaker),
                            sort_events_by_odds(self, team_name, descending=True),
                            get_best_odds(self)

Odds Calculator:
Converts American odds (+150, -150) to implied probabilities.
Removes the bookmaker's "vig" to calculate fair probabilities.
Data Handling (In-Memory):
Provides methods to load, filter, and sort odds data stored in memory.
Focuses on temporary analysis without persisting data to a database.

**DONE (I THINK)


PHASE 2: Database Integration
Goal: Introduce database functionality for persistent data storage and retrieval.
Methods: init(self, db_name), create_odds_table(self), fetch_mock_odds_data(self)
          save_odds_to_db(self, odds_data), get_odds_by_sport(self, sport_title: str),
          get_odds_by_team(self, team: str), get_latest_odds(self, limit: int = 10),
          delete_old_odds(self, days: int = 7)
Database Setup:
Creates a SQLite database (odds_db.db) and initializes the OddsTable.
Save Data:
Fetches mock odds data and saves it to the database for long-term storage.
Interaction:
Enables storing, querying, and managing odds data in the database.
Lays the groundwork for scalable data handling.

**DONE(I THINK)
**PLEASE CHECK MAIN FILE, NO IDEA WHAT IS GOING ON.


PHASE 3: Fetch Odds from APIs
Goa: Introduce real-world odds data by integrating external APIs (e.g., OddsAPI).
Methods: create_table(), add_odds(sport_key, event, bookmaker, team, odds, commence_time),
        fetch_odds(), fetch_odds_by_sport(sport_key), fetch_odds_by_bookmaker(bookmaker),
        fetch_odds_by_team(team)
Fetch Sports:l
  Retrieves available sports from OddsAPI and stores them in the database.
Fetch and Normalize Odds:
  Collects odds data from the API.
  Normalizes the data for consistency across different sportsbooks.
Save Odds:
  Stores fetched odds data in the database, ensuring proper indexing and structure.
##This is kind of not entirely true. We do not have a save method, because our
##add_odds(...)'s, fetch_odds()'s, fetch_odds_by_sport()'s functionalities includes saving, but saving isn't the main thing
##we are trying to do. It's adding, and saving comes with it.

DONE (I THINK)
**REST IS NOT GOOD**








Phase 4: EV and Arbitrage Detection **THIS IS WHERE I AM COMPLETELY LOST*
Goal: Analyze odds data for profitable betting opportunities.
      The three things are calculate/detect +EV, detect arbitrage, save (IDK where though)
      *Calculate EV and Detect Arbitrage are both located within BettingAnalyzer class. **MESSED UP AS WELL**
      *The BettingAnalyzer class file also contains dataclasses for easiness of location event attributes. **MESSED UP AS WELL**
      *Save results functionality belongs in the ResultsStorage class.
Methods (only for Calcuate EV and Detect Arbitrage) from BettingAnalyzer class:
    fetch_grouped_odds(),
Calculate EV:
  Compares implied probabilities to calculate the expected value of a bet.
  Identifies bets with positive EV (profitable opportunities).
Detect Arbitrage:
    Finds opportunities where combined odds across sportsbooks guarantee a profit regardless of the outcome.
Save Results: **I AM STRUGGLING WITH THIS, DO NOT KNOW HOW TO DO**
  Saves EV and arbitrage opportunities to the database for further analysis.
**Having trouble with saving results, don't know how to do.**



Phase 5: Notifications
Goal: Notify users of high-value betting opportunities.

Define Notification Rules:

Set thresholds for EV or discrepancies (e.g., EV > 0.1).
Notification System:

Sends alerts (e.g., email) to users when conditions are met.


Phase 6: PrizePicks Integration
Goal: Compare PrizePicks lines with sportsbook odds to find discrepancies.

Fetch PrizePicks Data:

Retrieves PrizePicks props using OddsAPI or other sources.
Highlight Discrepancies:

Compares PrizePicks lines with fair sportsbook odds.
Identifies significant differences and calculates EV.
Save Discrepancies:

Stores discrepancies and EV in the database.


Phase 7: Reporting and Automation
Goal: Automate the entire pipeline and provide actionable insights.

Generate Reports:

Summarize discrepancies and EV data into CSV or JSON reports.
Highlight top opportunities.
Integrate All Phases:

Combine data fetching, analysis, and notifications into a seamless pipeline.


Phase 8: Optimization and Scaling
Goal: Improve performance and scalability.

Optimize:

Enhance database queries and introduce caching.
Scale:

Transition to more robust databases (e.g., PostgreSQL).
Deploy on cloud platforms to handle larger datasets.


Phase 9 (Optional): User Interface
Goal: Create a user-friendly dashboard.

Build UI:

Develop a web interface to display odds, EV, and discrepancies.
Mobile Integration:

Add push notifications or SMS alerts.
Phase 10: Deployment
Goal: Make the system fully operational and accessible.

Deploy:
Host the project on a cloud platform.
Set up automated updates and security features.









