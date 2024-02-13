# Project BringPopcorn

Project BringPopcorn is an app designed for fetching movies and displaying them. Movies are shown on the left side of the box, and clicking on each one opens its details on the right side of the box.

We utilize the [OMDb API](https://www.omdbapi.com/) for fetching movie data.

## Search Functionality

When performing a search:

- Searches with less than 3 characters are ignored.
- Error handling informs users about unsuccessful searches, such as when no movie matches the query or when there's a connection issue.
- Each query triggers an HTTP request, and to optimize performance, we handle data fetching and race conditions using an AbortController.

## State Management

### States

- `query`: Stores the user's search query.
- `movies`: Holds the array of movies fetched from the OMDb API.
- `watched`: Manages the list of movies marked as watched by the user.
- `isLoading`: Indicates if data is currently being loaded.
- `error`: Stores error messages encountered during data fetching.
- `selectedId`: Stores the ID of the currently selected movie for displaying its details.
- `userRating`: Stores the user's rating for a movie.

### Refs

We use `useRef` for the search input to focus it on pressing the Enter key. The search input remains focused if it contains text.

### Effects

- **Movie Details**: Fetches movie details from the OMDb API when a movie is selected. Also sets the document title to the movie's title and cleans up event listeners on component unmount.
- **Storing Watched Movies**: Stores the watched movies list in local storage whenever it changes.
- **Fetching Movies**: Retrieves movies from the OMDb API based on the search query. Handles errors and aborts the fetch request if the component unmounts or a new query is triggered.
- **Focusing Search Input**: Listens for the Enter key press to focus the search input and prevent clearing if it's already focused.
- **Cleaning Aborted Fetches**: Clears up aborted fetch requests.

## Components

### App

The main component managing state, user interactions, and rendering. Utilizes hooks like useState and useEffect. It fetches movies, handles selection, adding to the watched list, and rendering the UI.

### Loader

Displays a loading message while fetching data.

### ErrorMessage

Displays error messages for failed API requests.

### NavBar

Renders the navigation bar with the app logo and search input.

### Logo

Simple component rendering the app logo.

### Search

Component for searching movies. Provides a search input field and handles input focus.

### NumResults

Displays the number of search results found.

### Main

Renders the main content of the application.

### Box

Collapsible box component to group related content.

### MovieList

Displays a list of movies fetched from the API.

### Movie

Renders individual movie items in the list with title, poster, and release year.

## Watched Movies Storage

The watched movies list is stored in local storage using useEffect. It ensures persistence between sessions.

## Functionality

- Boxes can be toggled open/closed.
- Users can rate movies with a star rating system.
- Adding movies to the list updates derived states like movie count, average IMDb rating, user rating, and average runtime.
- Users can delete movies from the list and their ratings are remembered.
