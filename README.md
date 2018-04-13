# FinalProject20
MAIN PURPOSE OF CODE:
The main purpose of this program is to scrape/crawl the IMDB website which gathers information on theaters 5- 30 miles away from a zip code entered. The program will also gather a list of movies playing at the theater selected from the IMDB website. The URL to the IMDB website is http://www.imdb.com.  The information about these movies and theaters will be stored in two different cache files and I will use two classes (Theater and Movie) to reference information and create the SQL database. I create a variety of different charts on plotly to demonstrate the information gathered.


DATA SOURCES:
  The data sources I use for this program is IMDB http://www.imdb.com. I crawl a variety of different pages on this website to collect all the information I need to run the program. Also make sure you have the packages in requirement.txt so you are able to run the program.


INFORMATION NEEDED TO RUN PROGRAM:
  Plotly is used in this program. Read these instructions to install plotly to run this program: https://plot.ly/python/getting-started/. Create a secret.py file with your plotly credentials. Note that the test file only works if you use the caches that are in Github. This is because new information is refreshed each day on the IMDB website.

DESCRIPTION (code structure, names of significant data processing functions, and class definitions. If there are large data structures (e.g., lists, dictionaries) that you create to organize your data for presentation, briefly describe them.):

The functions that scrape and crawl the IMDB website are list_movietheaters and movie_information.
The list_movietheaters function gathers the movie theaters 5-30 miles away from the zip code a user enters. The function takes in a zip code and returns a list of theater objects. The function crawls 2 different movie theater pages to gather detailed information about a specific theater, such as the address and movies playing at the theater. Within the function, the class Theaters is called and creates a class object for each theater. Also, after the list of theater objects is created the list_movietheaters calls the insert_theaters function. The insert_theaters function takes in the list of Theater class objects and the zip code entered by the user, and inputs the information gathered from each object into the Theaters table.


The function movie_information takes in a Theater object and returns a list of movie objects. The function is designed to gather information about each movie that is playing at the theater (a theater object gets passed in). Three different pages are crawled to gather detailed information about each movie playing, for example name, title, year, description, gross profit in the USA, cumulative worldwide gross profit, etc. After a list of Movie class objects is created the Insert_Movies function is called. This function takes in a list of Movie class objects and the theater object, and inserts the information about each movie into the Movies table. At the end of Insert_Movies, the function update_movies_playing is called. update_movies_playing takes in theater class object. This function has a SQL query that selects an Id, from the movie table, that is equal to the name in the list theater_object.list_movies. After the movie Id is retrieved the Theater table gets updated with a list of movie Id's which represents the movies playing at a specific theater.

Starting with the function budget_and_cumulativegross till OpeningWeekendUSA_compared_GrossUSA (five functions total) these functions create graphs using plotly.
GRAPHS CREATED IN PROGRAM:
1.	Graphs the movies playing at a selected theater (names of movies x-axis) and the length of time (in minutes) of each movie (y-axis) [bar chart]
2.	Graphs the movies playing at a selected theater (names of movies x-axis) and shows the gross Profit USA for the movie compared to gross profit for the opening weekend in USA  for the movie (y-axis) [grouped bar chart]
3.	Graphs the movies playing at a selected theater (names of movies x-axis) and shows the budget for each movie (y-axis) and the length of time (in minutes) of each movie (y-axis) [scatter plot]
4.	Graphs a movie selected by the user and shows the percent revenue from the U.S compared to the percent revenue from the rest of the world [pie chart]
5.	Graphs movies playing at a selected theater (names of movies x-axis) and compares the budget of each movie to the cumulative worldwide gross (y-axis) [grouped bar chart]


USER GUIDE (how to run the program and how to choose presentation options):

Interactive Component:

zip <zipcode> :Is available at anytime. It lists all theaters between 5 and 30 miles away from the zipcode entered. Will show the user 10 theaters by default. If there are more than 10 theaters for the zipcode then the user will be asked if they would like to see more.
A 5 digit zip code

theater <result_number>:	Available only if there is an active result set (a list of theaters near a zipcode specified). It lists all movies showing at the theater selected.	An integer 1-len (result_set_size)

movie info <result_number>: Available only if there is an active result set (a list of movies showing at a specified theater). Shows further information about a movie selected.	An integer 1-len (result_set_size)

exit: Exits the program 	

help:	Shows the different commands that a user can enter 	

After a user enters the theater command the interactive will prompt the user asking them if they would like to see a graph of movie budget compared to cumulative worldwide gross ("yes or "no"), a graph of movie time ("yes or "no"), a graph of movie budget compared to movie length ("yes or "no"), a graph of Gross Profit USA compared Opening Weekend USA ("yes or "no")?. The graphs will open depending on if the user responds yes to these four different questions.

After a user enters the movie info command the interactive will prompt the user asking them if they would like to see a graph that compares revenue from the U.S versus the rest of the world (“yes” or “no”). The graph will open if the user responds yes to this question.
