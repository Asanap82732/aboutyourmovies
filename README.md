<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dynamic Movie Info</title>
    <style>
        /* Global Styles */
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            color: white;
            margin: 0;
            padding: 0;
        }
        header {
            background-color: rgba(0, 0, 0, 0.7);
            padding: 20px;
            text-align: center;
            border-bottom: 2px solid #f4f4f4;
        }
        h1 {
            font-size: 2.5em;
            margin: 0;
            font-family: 'Roboto', sans-serif;
        }
        .container {
            padding: 30px 50px;
        }

        /* Movie Card Styles */
        .movie {
            background-color: #ffffff;
            border-radius: 12px;
            box-shadow: 0px 6px 18px rgba(0, 0, 0, 0.1);
            margin: 30px 0;
            display: flex;
            transition: transform 0.3s ease;
        }
        .movie:hover {
            transform: scale(1.05);
        }
        .movie img {
            border-radius: 12px;
            width: 200px;
            height: 300px;
            object-fit: cover;
            margin-right: 20px;
        }
        .movie-details {
            flex-grow: 1;
            padding: 20px;
            color: #333;
        }
        .movie h2 {
            color: #2575fc;
            font-size: 1.8em;
            margin-bottom: 15px;
        }
        .movie p {
            margin: 5px 0;
        }

        /* Button Styles */
        .btn {
            padding: 12px 20px;
            background-color: #2575fc;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        .btn:hover {
            background-color: #1e65b0;
        }

        .form-container {
            background-color: #ffffff;
            border-radius: 12px;
            padding: 20px;
            margin-top: 50px;
            box-shadow: 0px 6px 18px rgba(0, 0, 0, 0.1);
        }
        input, textarea {
            width: 100%;
            padding: 12px;
            margin: 10px 0;
            border-radius: 5px;
            border: 1px solid #ddd;
        }
        input[type="url"] {
            width: 100%;
            margin-bottom: 20px;
        }
        textarea {
            resize: vertical;
            min-height: 150px;
        }
        
        /* Social Share and Like Button Styles */
        .social-buttons {
            margin-top: 15px;
        }
        .social-buttons button {
            background-color: transparent;
            color: #2575fc;
            font-size: 1.2em;
            margin-right: 15px;
            cursor: pointer;
            border: none;
        }
        .like-button {
            color: #ff6347;
        }
        .share-button {
            color: #32cd32;
        }

        footer {
            background-color: #333;
            color: white;
            text-align: center;
            padding: 15px 0;
            position: fixed;
            bottom: 0;
            width: 100%;
        }
    </style>
</head>
<body>

<header>
    <h1>Welcome to Dynamic Movie Info</h1>
    <p>Discover, Add, and Share Your Favorite Movies!</p>
</header>

<div class="container" id="movies-container">
    <!-- Movie listings will be dynamically inserted here -->
</div>

<!-- Movie Submission Form -->
<div class="container form-container">
    <h3>Add Your Favorite Movie</h3>
    <form id="movie-form">
        <input type="text" id="movie-title" placeholder="Movie Title" required>
        <input type="text" id="movie-year" placeholder="Release Year" required>
        <input type="text" id="movie-genre" placeholder="Genre" required>
        <input type="text" id="movie-director" placeholder="Director" required>
        <input type="text" id="movie-cast" placeholder="Cast" required>
        <textarea id="movie-description" placeholder="Description" rows="5" required></textarea>
        <input type="url" id="movie-image" placeholder="Image URL" required>
        <button type="submit" class="btn">Add Movie</button>
    </form>
</div>

<footer>
    <p>© 2025 Movie Info. All rights reserved.</p>
</footer>

<script>
    // Sample movie data
    const movies = [
        {
            title: "The Dark Knight",
            year: 2008,
            genre: "Action, Crime, Drama",
            director: "Christopher Nolan",
            cast: "Christian Bale, Heath Ledger, Aaron Eckhart",
            description: "When the menace known as the Joker emerges from his mysterious past, he wreaks havoc and chaos on the people of Gotham, forcing Batman to come out of his self-imposed exile and fight against the criminal mastermind.",
            image: "https://via.placeholder.com/200x300?text=Dark+Knight"
        },
        {
            title: "Inception",
            year: 2010,
            genre: "Action, Adventure, Sci-Fi",
            director: "Christopher Nolan",
            cast: "Leonardo DiCaprio, Joseph Gordon-Levitt, Ellen Page",
            description: "A thief who enters the dreams of others to steal secrets from their subconscious is given the inverse task of planting an idea into the mind of a CEO.",
            image: "https://via.placeholder.com/200x300?text=Inception"
        }
    ];

    // Function to display movies dynamically
    function displayMovies() {
        const container = document.getElementById('movies-container');
        container.innerHTML = ''; // Clear existing movies

        movies.forEach((movie, index) => {
            const movieElement = document.createElement('div');
            movieElement.classList.add('movie');
            movieElement.innerHTML = `
                <img src="${movie.image}" alt="${movie.title} Poster">
                <div class="movie-details">
                    <h2>${movie.title}</h2>
                    <p><strong>Release Year:</strong> ${movie.year}</p>
                    <p><strong>Genre:</strong> ${movie.genre}</p>
                    <p><strong>Director:</strong> ${movie.director}</p>
                    <p><strong>Cast:</strong> ${movie.cast}</p>
                    <p><strong>Description:</strong> ${movie.description}</p>
                    <div class="social-buttons">
                        <button class="like-button" onclick="likeMovie(${index})">👍 Like</button>
                        <button class="share-button" onclick="shareMovie('${movie.title}')">🔗 Share</button>
                    </div>
                </div>
            `;
            container.appendChild(movieElement);
        });
    }

    // Event listener for form submission
    document.getElementById('movie-form').addEventListener('submit', function(e) {
        e.preventDefault(); // Prevent the form from submitting normally

        // Get form values
        const title = document.getElementById('movie-title').value;
        const year = document.getElementById('movie-year').value;
        const genre = document.getElementById('movie-genre').value;
        const director = document.getElementById('movie-director').value;
        const cast = document.getElementById('movie-cast').value;
        const description = document.getElementById('movie-description').value;
        const image = document.getElementById('movie-image').value;

        // Create a new movie object
        const newMovie = {
            title,
            year,
            genre,
            director,
            cast,
            description,
            image
        };

        // Add the new movie to the movies array
        movies.push(newMovie);

        // Clear the form
        document.getElementById('movie-form').reset();

        // Update the movie list
        displayMovies();
    });

    // Like a movie (can be enhanced to track likes)
    function likeMovie(index) {
        alert(`You liked "${movies[index].title}"!`);
    }

    // Share movie details (could be expanded with actual sharing functionality)
    function shareMovie(title) {
        alert(`You are sharing the movie: ${title}`);
    }

    // Call the function to display movies when the page loads
    window.onload = displayMovies;
</script>

</body>
</html>
