# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Capstone Project - League of Legends champion recommender
Author:
Ryan Yong

- [Background](#Background) 
- [Problem Statement](#Problem-Statement)
- [Data Collection](#Data-Collection)
- [Data Engineering & EDA](#Data-Engineering-and-EDA)
- [Initial Model](#Initial-Model)
- [Final Hybrid Model](#Final-Hybrid-Model)
- [Evluation](#Evaluation)
- [Conclusion](#Conclusions)



# Background

Riot Games is a gaming company founded in California. They are mostly known for creating one of the most popular and active games in the world known as League of Legends. Building on a Free-to-Play model, League of Legends has no cost to play, only charging for cosmetic skins for in-game champions. Seeing as cosmetic skin monetization is their primary revenue generator, increasing their player base and ensuring player retention is their primary concern. However, with 167 champions available to date, most players end up playing only a handful of champions, unsure which of the remaining unplayed champions would best suit them. This recommender system aims to combat this issue by recommending users based on their champion mastery new champions for them to try and ensure player retention. The recommendation will also serve to improve skin sales indirectly when users purchase new skins for their recommended champions.

---

# Problem Statement

How can one build a League of Legends (LoL) champion recommender system to increase user play time and improve skin sales

---

# Data Collection

Data was scraped using Riotwatcher, a python wrapper using Riot's in-house API tool. A secondary dataset was obtained from [LoL Wiki.](https://leagueoflegends.fandom.com/wiki/League_of_Legends_Wiki). Initial attempts at scraping the secondary dataset failed, and due to time constraints, the dataset was manually collected.

# Data Engineering and EDA

### Exploratory Data Analysis
EDA for data scraped from champions and accounts involves gaining insights into the dataset's characteristics, identifying patterns, and understanding its underlying structure. It was worth noting that the champion mastery for user accounts followed a log-normal distribution, meaning that upon using a logarithmic scale, a normal distribution was seen.

Further analysis on the account dataset includes analysing the distribution of champion mastery by the userbase as well as outlier detection. For the champion dataset, champion traits were analysed and categorical data columns such as 'Class', 'Position','Resource','Range tpye' and 'Adaptive type' were one-hot encoded to ensure a fully numerical dataset. Relationships between these traits were also analyzed using heatmap.

# Initial Model

The initial recommender system only used account data and used cosine similarity to deduce similar accounts to the user, allowing for quick comparisons and highlighting champions that the similar accounts played more on which the user account has not, giving the recommendations as such. 

### Evaluation

The inital recommender system was poor in the sense that the recommendation was too general, considering it only accounted for account champion mastery scores. Furthermore, rank was not a factor in the recommendation, leading to bad results where users were just not recommended any suitable champions.

# Final Hybrid Model

The final model was a hybrid system comprising of Collaborative Filtering (CF) and Content-Based Filtering (CB). The CF portion uses Singular Value Decomposition (SVD) to reduce the account dataset dimensionality, allowing for an application of the CB filtering based on cosine similarity to measure up the user's account with the dataset. Afterwhich, a hybrid rank-based weightage system was applied on the dataset based on the individual ranks of each account alongside the account's rank-proximity to the user's account. The combination of everything resulted in a final singular list of all the champions ranked in order of recommendation, factoring in champion similarity, account data as well as rank based analysis.

## Evaluation

The evaluation of this recommender system was based on the R^2 value of the SVD model, which proved to be 0.87 on test and unseen data. In addition, a survey rating was conducted on the top 10 recommended champions on the current user base. This survey rating serves as an initial litmus test to the player base, and further wide-scale implementation of the ratings should be conducted. 

The initial tests prove to be positive, with a Hit Ratio of 83.3% within the top 3 recommendations. Furthermore, a Mean Average Precision (MAP) across all survey results was 0.974, with every user finding a new main champion within the first 7 options.

### Conclusions

In conclusion, this project has effectively built a recommender system that helps users find new and similar champions to their existing champion pool. This helps users obtain new novel champions and resetting their excitement for the game, while also improving player retention for League of Legends. With a player base that has a wider and more diverse champion pool, Riot Games should see an increase in skin sales if they decide to implement a champion recommender within the League of Legends Client.

---

### Files

* code
  1. 01a_data_scrape.ipynb
  2. 01b_wiki_scrape_attempt.ipynb
  3. 02_champion_dataset_EDA.ipynb
  4. 03_account_dataset_EDA.ipynb
  5. 04_initial_recommender_system.ipynb
  6. 05_final_hybrid_system.ipynb
  7. 06_implmentation.ipynb
* data
  1. account_mastery_dataset.csv
  2. account_rank_mastery_dataset.csv
  3. accounts_dataset.csv
  4. champion_data.csv
  5. champion_features.csv
  6. engineered_champion_data.csv
  7. test_accounts_rank_mastery.csv
* images
  1. account_region_options.png
  2. summoner_region_options.png
* pickles
  1. champion_similarity_df.pkl
  2. cols.pkl
  3. scaler.pkl
  4. svd.pkl
  5. train_predicted_matrix.pkl
  6. Vt_k.pkl
* Capstone Presentation.pdf
* README.md 
