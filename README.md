# 🎮 Videogame Recommendation System Using Steam Reviews

**Authors**: Gerardo Gómez Argüelles, Tirdod Behbehani, Oliver Tausendschön  
**Date**: March 26th, 2025

---

## 📌 Introduction

In the age of digital distribution, platforms like Steam offer thousands of games, making it increasingly difficult for players to discover titles that align with their interests. This project presents a recommendation system that leverages the rich information found in user-generated reviews, moving beyond traditional rating-based methods. Our system uses text mining techniques to understand what players appreciate or dislike about different games and recommends new titles based on these preferences.

The system begins by collecting Steam reviews along with game metadata, including genre and whether the review is positive or negative. We then incorporate simulated user input—artificially written reviews expressing both likes and dislikes—to build a dual-sided user profile. Each game and user profile is converted into numerical vectors using TF-IDF, and recommendations are made based on cosine similarity, combining both textual similarity and genre preferences.

---

## 🧠 Methodology

We scraped 40,649 reviews for 95 games across 15 genres. Reviews are categorized as positive or negative, and we separated these sentiments throughout the pipeline. After preprocessing with lemmatization, filtering, and token normalization, we aggregated game reviews and computed TF-IDF vectors per sentiment.

The user profile was created using simulated positive and negative reviews. Cosine similarity scores were computed between the user profile and game profiles. A final recommendation score was calculated by combining text-based similarity with genre alignment.

**Final Score Formula**:  
`Final Score = (Positive Similarity - Negative Similarity) + λ × Genre Match Score`  
We used `λ = 0.5` for balancing textual and metadata-based recommendations.

---

## 📊 Results

The system successfully recommended games such as *Kingdom Come: Deliverance II*, *Europa Universalis IV*, and *Age of Empires IV*, which strongly aligned with the user’s preferences for RPGs, strategy, and immersive gameplay.

The separation of positive and negative reviews proved crucial, allowing the system to detect subtle preferences and avoid recommending games with unwanted features, even if they share some traits with liked titles.

---

## 🔁 Adaptive Feedback

To make the system dynamic and responsive, we implemented an adaptive feedback loop. After receiving a recommendation, the user can provide feedback by liking or disliking it. This feedback updates the genre profile (but not the text-based component), reinforcing or penalizing genres based on user reactions.

For instance:
- Liking a game increases the weight of its genres in the user profile.
- Disliking a game decreases the influence of those genres on future recommendations.

This approach provides lightweight personalization and helps the system improve over time without requiring complex retraining.

---

## ⚙️ Project Structure

All components of this project are stored inside the `Delivery/` folder.





```plaintext
Delivery/
├── 1_Steam_API_Call.ipynb                 # Notebook for scraping Steam data via API
├── 2_Text_Preprocessing.ipynb            # Text preprocessing: cleaning, lemmatization
├── 4_Recommendation_System.ipynb         # Full pipeline: user profiling & recommendations
│
├── Steam_Reviews_1.csv                   # Raw review dataset
├── all_Steam_Reviews_cleaned_1.csv       # Cleaned and lemmatized review dataset
├── positive_steam_reviews_1.csv          # Subset of recommended (positive) reviews
├── negative_steam_reviews_1.csv          # Subset of not recommended (negative) reviews
├── game_top_tfidf_words_by_doc.csv       # TF-IDF matrix (top words per game document)
│
├── Report_Game_Recommendation_System.pdf # Full project write-up as a formatted report


---

## 📈 Performance Considerations

Traditional recommender metrics such as Precision@K or NDCG are not suitable for our system because it uses the user's own input for profile creation. Evaluating the model on that same input would be circular and biased.

Instead, we evaluate:
- Cosine similarity distributions between games and the user profile
- Evolution of recommendations after adaptive feedback
- Alignment between the final recommendations and user-declared preferences

This approach highlights the qualitative improvements the system makes with minimal feedback.

---

## 💬 Conclusion

This project demonstrates the potential of combining textual review analysis with structured metadata for building more nuanced and personalized recommendation systems. By separating positive and negative feedback, and incorporating genre metadata with adaptive feedback, we achieved a hybrid system capable of generating meaningful and tailored game suggestions.

While we used an artificial user profile due to API and hardware constraints, the system architecture is generalizable and scalable. Future improvements could include:
- Integration of real user behavior data (e.g., hours played)
- Use of advanced NLP models (e.g., LLMs) for better understanding review content
- Online learning from user behavior over time

The flexibility of our pipeline makes it a promising foundation for more intelligent and interactive recommendation systems on platforms like Steam.

---
