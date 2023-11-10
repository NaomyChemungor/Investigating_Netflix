# Investigating_Netflix
# Importing pandas and matplotlib
import pandas as pd
import matplotlib.pyplot as plt

netflix_df=pd.read_csv("netflix_data.csv")

#Filtering data to remove TV shows
netflix_subset=netflix_df[netflix_df["type"] != "TV Show"]

#creating a new data frame
netflix_movies=netflix_df.loc[:,["title", "country", "genre", "release_year", "duration"]]

# Filter movies with duration less than 60 minutes
short_movies = netflix_movies[netflix_movies['duration'] < 60]

# Print the first 20 rows of short_movies
print(short_movies.head(20))

colors = []
for index, row in netflix_movies.iterrows():
    genre = row['genre']
    
# assigning genre
    if genre == "Children":
        colors.append('purple')
    elif genre == "Documentaries":
        colors.append('Green')
    elif genre == "Stand-Up":
        colors.append("yellow")
    else:
        colors.append("maroon")
        
netflix_movies['colors'] = colors
fig = plt.figure()
plt.scatter(netflix_movies["release_year"],netflix_movies["duration"], c=netflix_movies["colors"])

plt.xlabel('Release Year')
plt.ylabel('Duration (min)')
plt.title('Movie Duration by Year of Release')

answer = "No"
print("Are we certain that movies are getting shorter?", answer)

