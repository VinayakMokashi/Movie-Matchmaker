# Personalized Cinema: An Efficient Item-Based Movie Recommendation Model

An item-based collaborative filtering movie recommendation engine, leveraging the MovieLens 100K dataset to provide personalized movie recommendations. This project focuses on item similarity, using correlation analysis to suggest movies aligned with user preferences.

## Project Overview:

This project builds a movie recommender system using item-based collaborative filtering. The MovieLens 100K dataset provides user ratings, enabling us to draw insights on user preferences and suggest similar movies through correlation analysis.

## Features:

__Exploratory Data Analysis (EDA)__: In-depth analysis to uncover trends in movie ratings and user preferences.

__Single Movie Recommendation__: Provides similar movie suggestions based on a specific movie chosen by the user.

__Full Dataset Recommendation__: Recommends movies based on item-item relationships across the entire dataset for personalized user recommendations.

## Files:

__Code.ipynb__: Entire code implementation

__Movie_Id_Titles__: Contains the data for Item ID and the movie title

__u.data__: Main data

__My_Ratings__: Reviews for some movies given by me

## Dataset:

__Source__: MovieLens 100K

__Contents__: 100,000 ratings from 1000 users on 1700 movies movies.

__Format__: Includes movie titles, user IDs, ratings, and timestamps.

## Requirements:

Python 3.x

Pandas

NumPy

Matplotlib / Seaborn (for EDA)

## Methodology:

__Data Loading__: Import and preprocess the MovieLens 100K dataset.

__Exploratory Data Analysis (EDA)__: Analyze trends, including most-rated and highest-rated movies.

__User-Item Matrix Creation__: Create a matrix where each row is a user, and each column is a movie. Values represent ratings.

__Item-Based Collaborative Filtering__:

__Single Movie Sample__: Calculate correlation between one selected movie and others to recommend similar movies.

__Entire Dataset Filtering__: Apply item-based collaborative filtering across all movies to make recommendations based on user-specific ratings.

## Results:
The recommender successfully suggests movies similar to user preferences based on item-item relationships, demonstrating the power of item-based collaborative filtering for personalized recommendations.

## Future Improvements:

__Hybrid Model__: Combine item-based and user-based filtering to improve recommendation accuracy.

__Enhanced Filtering Techniques__: Incorporate advanced filtering (e.g., content-based features).

__Scalability__: Adapt the model for larger datasets beyond MovieLens 100K.

