# MOVIE ANALYSIS FOR MICROSOFT STUDIO

## Repository Contents

Below is a list of the contents of this repository.

zippedData: original sources of dataset used

student- Microsoft analysis.ipynb: Jupyter Notebook containing my project

Presentation.pdf.pdf: The non technical presentation

READme Microsoft analysis.md: The README explaining the contents of the repo.

title.basics.csv: First Dataset used

title.ratings.csv: Second Dataset used



# Overview

This project analyzes data from IMDb, which is an online database containing information related to movies and other films. Exploratory data analysis including univvariate and multivariate analysis shows that success of a movie depends on the genre, length of the movie and the ratings it has received. The Microsoft studio can use these insights to decide what to allocate resources to and also the kind of movies that would be profitable for them.  


# Business Problem
Microsoft sees all the big companies creating original video content and they want to get in on the fun. They have decided to create a new movie studio, but they don’t know anything about creating movies. I have explored the nature of the movies that are currently showing best performance at the box office. I then displayed how length of film, genre and customer feedback translates to good performance of a movie.

# Data Understanding

Data used was from from two files from IMDb.
The first dataset contains information on title basics: 'title.basics.csv', referenced as df dataframe.
It has 6 columns namely: tconst,  primary_title, original_title, start_year, runtime_minutes and genres
The second dataset contains information on title ratings: 'title.ratings.csv',referenced as df2 dataframe.
It has three columns namely: tconst, averagerating and numvotes

In order to further understand the data, the following aspects were assessed
1. The number of columns in each dataset.
2. The general information contained in each dataset. E.g:
 The data type of each column
 The none null count
3. Descriptive statistics for numerical columns in each dataset. E.g: 
Mean
Standard deviation
Median
Quartiles



# Analysis and Evaluation
There was a check on Outliers, Duplicates and missing values.

An analysis was done and this provides the basis for the actions that will inform Microsoft studio's choice of movies.

## Prefered Movie genres

Some movie genres are produced more than others. This may be due to the great reception in the market. 
We have the Documentary and Drama genres each taking up 21% of all the movies produced.




## Impact of number of votes for a movie on the ratings

Ratings have an impact on the performance of movies created by big companies. High ratings from our analysis increase as the number of votes for them increase. consequently, movies with lower ratings have fewer votes.
    


## Does the length of a movie affect the rating

Most high rating movies were 90 minutes long and low rating movies had a slightly shorter. Medium rating movies had a higher median than the high rating therefore for a movie to do well, length has to be considered in order to get that optimum sweet spot for consumers.



# Conclusion

This analysis leads to a few recommendations for the head of Microsoft's new movie studio.

1. Produce a genre that the market demands most (as indicated by what producers are producing more of). Documentaries ranking highest, may be prefered by consumers due to the fact that they are based on real life. A single genre will also give the company an edge in the market.

2. Invest in consumer feedback. Movies that had high ratings also had many people accessing them and rating them. Microsoft, being a tech company can leverage that and ensure it has algorithms for fetching feedback from consumers.

3. Have an optimal time for the length of the movie. Many movies that rate highly are 90 minutes long. Therefore this seems to be the optimal length for successful viewership by consumers. 


## Next Steps
Further analysis would give more insights to the Microsoft studio by:
1. Modelling the impact of change in title on the ratings. This data is available in the given dataset.
