# Recommendation_System_Steam
🎮 Videogame Recommendation System Using Steam Reviews

Authors: Gerardo Gómez Argüelles, Tirdod Behbehani, Oliver Tausendschön
Date: March 26th, 2025
Introduction

In the age of digital distribution, platforms like Steam offer thousands of games, making it increasingly difficult for players to discover titles that align with their interests. This project presents a recommendation system that leverages the rich information found in user-generated reviews, moving beyond traditional rating-based methods. Our system uses text mining techniques to understand what players appreciate or dislike about different games and recommends new titles based on these preferences.

The system begins by collecting Steam reviews along with game metadata, including genre and whether the review is positive or negative. We then incorporate simulated user input—artificially written reviews expressing both likes and dislikes—to build a dual-sided user profile. Each game and user profile is converted into numerical vectors using TF-IDF, and recommendations are made based on cosine similarity, combining both textual similarity and genre preferences.
Methodology

We start by scraping 40,649 reviews from Steam, covering 95 games across 15 genres. Reviews are categorized as recommended or not recommended, allowing us to separate positive and negative sentiment during analysis. After thorough preprocessing—including lemmatization, stopword removal, and filtering of HTML tags and emojis—we aggregate reviews per game and compute TF-IDF vectors separately for positive and negative reviews. This enables us to capture different perspectives on each game’s features.

To model the user’s preferences, we simulate a user who writes reviews for a small number of games. These reviews are again divided by sentiment, and each sentiment is represented by a single TF-IDF vector. We then compute cosine similarity between these user vectors and each game’s vectors to measure alignment with liked and disliked traits. A final score is calculated by subtracting negative similarity from positive similarity and incorporating a genre matching component, which compares the user’s genre preferences with each game’s genre metadata.
FinalScore=(PositiveSimilarity−NegativeSimilarity)+λ×GenreMatchScore
FinalScore=(PositiveSimilarity−NegativeSimilarity)+λ×GenreMatchScore

Here, λ is a weighting parameter (set to 0.5) to balance textual similarity with genre alignment.
Results

The results show that this hybrid approach, which integrates both textual insights and structured metadata, offers a nuanced method of generating game recommendations. Our analysis reveals that the user’s top preferences are role-playing and adventure games, with frequently used words in positive reviews including "story", "world", and "experience". The final list of recommended games includes titles like Kingdom Come: Deliverance II and Warhammer 40,000: Space Marine 2, which align well with the identified preferences.

We also visualize the top features in user reviews, the genre distributions, and the similarity score distributions. These insights reinforce the importance of separating sentiment, as certain features like “combat” can appear in both positive and negative reviews depending on context.
Adaptive Feedback System

To further personalize the system, we introduce a lightweight adaptive feedback loop. Users can approve or reject recommended games, which dynamically updates their genre preference profile. Games the user likes reinforce the associated genre weights, while disliked games reduce their influence. This iterative update does not alter the text-based component, keeping the system simple yet responsive. Re-running the recommendation process with updated profiles results in a refined list of suggestions that better align with the user’s evolving tastes.
Performance Considerations

Traditional metrics like Precision@K or NDCG are ill-suited for our approach, which already incorporates the user’s past reviews. As such, we rely on internal consistency measures such as cosine similarity distributions and shifts in genre alignment after feedback integration. While these are not absolute metrics, they offer valuable diagnostic insight.

One key limitation is the artificial nature of the user profile and the hardware constraints preventing large-scale scraping. Nonetheless, the system demonstrates a promising direction for personalized game recommendation by integrating both sentiment analysis and metadata.
Conclusion

This project illustrates how textual analysis of Steam reviews can be used to generate personalized game recommendations. By separating positive and negative sentiments, combining them with genre data, and introducing adaptive feedback, we create a system that mirrors real-world user behavior more accurately than traditional recommender systems.

Future work could explore the use of large language models to further enhance the textual analysis component, as well as integrating richer metadata from Steam, such as hours played or achievement progress. Overall, our method provides a foundation for more intuitive and sentiment-aware game recommendation systems.
