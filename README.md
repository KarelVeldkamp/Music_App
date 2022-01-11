# Music app
This is a repository with the source code for a music web app hosted at https://carlitov.shinyapps.io/feature_networks/. I started writing the app for a programming course in 2020. Its all writen in R, and is mostly built aroud the spotify API. It consists of three main features: A recommender that builds you a playlist based on one of your own spotify playlists, a visualisation of collaborations between artistst, and a visualisations of the lyrics of a song or an entire album. 

Some of the features can take quite a long time because of the spotify API rate limit. 

### Music recommendation
The music recommendation page allows you to log into spotify and select one of your playlists. It will then recommend a new playlist based on the songs in the selected playlist, and give you the option to add the new playlist to your spotify account. 

The underlying algorithm is quite simple:
- First, for all songs in the playlist, I get pre-extracted spotify audio features. These include Dancability, Energy, Tempo, Speeciness and Accousticness. 
- On these features, I perform k-means clustering, choosing the value of K using silhouette scores. 
- Then, a large pool of candidate songs is created. The pool of songs consists of the top songs of the artists that are in the playlist, the top songs of artists that are similar to the artists in the playlist, according to the spotify similar artists feature, and the top songs of any artists that have collaborated with artists in the playlist. 
- For each of the K clusters, I select the songs that are most close to the cluster mean, and add them to the playlist. The number of songs added per cluster depends on the cluster size in the original playlist. 

The algorithm is quite simple, and the recommendations can sometimes be all over the place, however you can definitely find some cool songs using the app.

### Visualisation of collaborations
This page lets you visualize the collaborations of a certain artist. Specifically, you can select an artists, and it will look up all the artists that have ever worked with them. The collaborators will then all be nodes in the network, and an edge represents wether the collaborators have also collaborated with each other. Node size represents the number of collaborations with the selected artist, and edge size represents the number of collaborations between two nodes.

### Visulisation of lyrics
This is the most simple page on the app, and the one I started with. You can simply search for a song or an album, and three visualisations will be plotted: A wordcloud, a barchart of word frequency and a barchart of the spotify audio features. It is based on the Genius API. 
