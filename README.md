# Movie Recommender System 🎬

Hey there! This is a movie recommender system. Think of it as your personal guide to finding awesome movies you'll love!

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This project is released under the MIT License. That basically means you're free to use, change, and share it. Click the badge for more details!



## Description
This project is a content-based movie recommender system that uses cosine similarity to suggest movies similar to a selected movie. It leverages the TMDB API to fetch movie posters and Streamlit to create an interactive user interface.



## Table of Contents
1.  [Features](#features)
2.  [Tech Stack](#tech-stack)
3.  [Installation](#installation)
4.  [Usage](#usage)
5.  [How to Use](#how-to-use)
6.  [Project Structure](#project-structure)
7.  [API Reference](#api-reference)
8.  [Contributing](#contributing)
9.  [License](#license)
10. [Important Links](#important-links)
11. [Footer](#footer)



## Features
*   🎬  **Movie Recommendation:** Recommends movies based on content similarity.
*   🔍  **Content-Based Filtering:** Uses cosine similarity to find similar movies.
*   🖼️  **Poster Display:** Fetches and displays movie posters from TMDb API.
*   ✨  **Streamlit UI:** Interactive web interface for movie selection and recommendation.



## Tech Stack
*   🐍  **Python:** Programming language.
*   💽  **Pickle:** Used for serializing and de-serializing Python object structures, mainly to load the model and similarity matrix.
*   ⚡  **Streamlit:** Web framework for creating interactive apps.
*   📡  **Requests:** Library for making HTTP requests to the TMDB API.



## Installation
1.  Make sure you have Python installed.
2.  Install the required libraries: streamlit and requests. You can install them using pip: `pip install streamlit requests`.
3.  Download the `movie_list.pkl` and `similarity.pkl` files. Ensure they are in the same directory as `app.py`.
4.  Run the Streamlit app: `streamlit run app.py`.



## Usage
1.  Run the Streamlit application: `streamlit run app.py`.
2.  Select a movie from the dropdown menu.
3.  Click the 'Show Recommendation' button.
4.  View the recommended movies and their posters.



## How to Use
This movie recommender system can be used to enhance user experience on movie streaming platforms or provide personalized movie suggestions.



### Real-World Use Cases:
*   **Streaming Platforms:** Integrate the system to suggest movies to users based on their viewing history or preferences.
*   **Movie Databases:** Use the recommender to provide similar movie suggestions on movie detail pages.
*   **Personal Movie Lists:** Help users discover new movies that align with their taste.



### Example:
```python
import streamlit as st
import pickle
import requests

def fetch_poster(movie_id):
    url = "https://api.themoviedb.org/3/movie/{}?api_key=8265bd1679663a7ea12ac168da84d2e8&language=en-US".format(movie_id)
    data = requests.get(url)
    data = data.json()
    poster_path = data['poster_path']
    full_path = "https://image.tmdb.org/t/p/w500/" + poster_path
    return full_path

def recommend(movie):
    index = movies[movies['title'] == movie].index[0]
    distances = sorted(list(enumerate(similarity[index])), reverse=True, key=lambda x: x[1])
    recommended_movie_names = []
    recommended_movie_posters = []
    for i in distances[1:6]:
        # fetch the movie poster
        movie_id = movies.iloc[i[0]].movie_id
        recommended_movie_posters.append(fetch_poster(movie_id))
        recommended_movie_names.append(movies.iloc[i[0]].title)

    return recommended_movie_names,recommended_movie_posters


st.header('Movie Recommender System')
movies = pickle.load(open('movie_list.pkl','rb'))
similarity = pickle.load(open('similarity.pkl','rb'))

movie_list = movies['title'].values
selected_movie = st.selectbox(
    "Type or select a movie from the dropdown",
    movie_list
)

if st.button('Show Recommendation'):
    recommended_movie_names, recommended_movie_posters = recommend(selected_movie)
    col1, col2, col3, col4, col5 = st.columns(5)

    with col1:
        st.text(recommended_movie_names[0])
        st.image(recommended_movie_posters[0])

    with col2:
        st.text(recommended_movie_names[1])
        st.image(recommended_movie_posters[1])

    with col3:
        st.text(recommended_movie_names[2])
        st.image(recommended_movie_posters[2])

    with col4:
        st.text(recommended_movie_names[3])
        st.image(recommended_movie_posters[3])

    with col5:
        st.text(recommended_movie_names[4])
        st.image(recommended_movie_posters[4])
```



## Project Structure
```
Movie-recommender-system/
├── app.py           # Streamlit application
├── movie_list.pkl   # Movie list data (Pickle file)
├── similarity.pkl   # Similarity matrix (Pickle file)
└── README.md        # Documentation
```



## API Reference
The application uses the TMDB API to fetch movie posters. You can find more information about the API [here](https://www.themoviedb.org/documentation/api).

*   **API Key:** `8265bd1679663a7ea12ac168da84d2e8`
*   **Endpoint:** `https://api.themoviedb.org/3/movie/{movie_id}?api_key={api_key}&language=en-US`



## Contributing
Contributions are always welcome!

1.  Fork the repository.
2.  Create a new branch for your feature or bug fix.
3.  Commit your changes.
4.  Push to the branch.
5.  Submit a pull request.



## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.



## Important Links
*   **Repository:** [https://github.com/Talha4543/Movie-recommender-system](https://github.com/Talha4543/Movie-recommender-system)



## Footer
Developed by [Talha4543](https://github.com/Talha4543).

[Fork me on GitHub](https://github.com/Talha4543/Movie-recommender-system) | Give a ⭐ [Star](https://github.com/Talha4543/Movie-recommender-system) | Report [Issues](https://github.com/Talha4543/Movie-recommender-system/issues)
