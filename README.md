# Project BringPopcorn

Project BringPopcorn is an app for fetching movies and displaying them. Movies are shown on the left side of the box, and clicking on each one opens the details on the right side of the box.

In this project, we are utilizing the [OMDb API](https://www.omdbapi.com/) for fetching movies.

## How Searching Works

When performing a search:

- Under 3 characters, the input will not search for movies.
- We handle errors to inform the user if there is no movie with that title or if the connection is lost during the search.
- Each query triggers an HTTP request, which may take time and resources for longer requests. To optimize this, we clean up data fetching and handle race conditions using AbortController.

## States and Effects

### States

The states include:

- Loading state for searching and for displaying movie details.
- On each click of the same movie, it selects it. On the second click, it nullifies the movie's ID. Every click opens the clicked movie in details.

- `query`: Stores the search query entered by the user.
- `movies`: Stores the array of movies fetched from the OMDb API.
- `watched`: Stores the list of movies marked as watched by the user.
- `isLoading`: Indicates whether data is currently being loaded.
- `error`: Stores error messages encountered during data fetching.
- `selectedId`: Stores the ID of the currently selected movie for displaying its details.

### Effects

- `useEffect` for fetching movies:
  - Fetches movies from the OMDb API based on the search query.
  - Handles errors and updates state accordingly.
  - Aborts the fetch request if the component unmounts or if a new query is triggered.

## Functionality

Both boxes can be closed and opened with the `-` and `+` signs.

After clicking any movie, the user can rate the movie based on their taste. A star rating system is included for this purpose. It shows the number of stars on hover, and clicking on them saves the user's rating. Conditional rendering is used; if the user has rated the movie, the "Add to List" button will appear. Pressing "Esc" while the movie details are open will close it and clean event listeners.

After adding a movie to the list, there are several derived states:

- The number of movies added to the list (length).
- The average IMDb rating for the movies.
- The average rating given by users.
- The average time for movies.

On the right side of the movies list item, users can click on the "X" to delete the movie. If the user has already rated a movie and then adds it to the list, upon opening the movie again, the star rating component will display the user's previous rating.
