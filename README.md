import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Search } from "lucide-react";

const moviesData = [
  { id: 1, title: "Inception", year: "2010", rating: "8.8", genre: "Sci-Fi", poster: "https://image.tmdb.org/t/p/w500/qmDpIHrmpJINaRKAfWQfftjCdyi.jpg" },
  { id: 2, title: "Interstellar", year: "2014", rating: "8.6", genre: "Sci-Fi", poster: "https://image.tmdb.org/t/p/w500/gEU2QniE6E77NI6lCU6MxlNBvIx.jpg" },
  { id: 3, title: "The Dark Knight", year: "2008", rating: "9.0", genre: "Action", poster: "https://image.tmdb.org/t/p/w500/qJ2tW6WMUDux911r6m7haRef0WH.jpg" },
  { id: 4, title: "The Matrix", year: "1999", rating: "8.7", genre: "Sci-Fi", poster: "https://image.tmdb.org/t/p/w500/f89U3ADr1oiB1s9GkdPOEpXUk5H.jpg" },
];

const WatchitHomepage = () => {
  const [movies, setMovies] = useState(moviesData);
  const [search, setSearch] = useState("");
  const [filterGenre, setFilterGenre] = useState("All");

  const filteredMovies = movies.filter(movie =>
    movie.title.toLowerCase().includes(search.toLowerCase()) &&
    (filterGenre === "All" || movie.genre === filterGenre)
  );

  return (
    <div className="min-h-screen bg-black text-white p-4">
      <header className="text-center py-6 bg-gray-900 shadow-lg">
        <h1 className="text-4xl font-bold text-red-500">Watchit</h1>
        <p className="text-gray-400 mt-2">Your go-to site for movie ratings, earnings, and more</p>
      </header>
      
      <div className="flex flex-col sm:flex-row justify-center items-center mb-6 sticky top-0 bg-black p-4 z-10 gap-4">
        <div className="relative w-full max-w-md">
          <input 
            type="text" 
            placeholder="Search for movies..." 
            className="w-full p-3 bg-gray-900 text-white rounded-full pl-10 outline-none"
            value={search}
            onChange={(e) => setSearch(e.target.value)}
          />
          <Search className="absolute left-3 top-3 text-gray-500" />
        </div>
        
        <select 
          className="p-3 bg-gray-900 text-white rounded-full outline-none"
          value={filterGenre}
          onChange={(e) => setFilterGenre(e.target.value)}
        >
          <option value="All">All Genres</option>
          <option value="Sci-Fi">Sci-Fi</option>
          <option value="Action">Action</option>
        </select>
      </div>
      
      <section className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
        {filteredMovies.length > 0 ? filteredMovies.map((movie) => (
          <Card key={movie.id} className="bg-gray-800 rounded-lg overflow-hidden transform transition-transform hover:scale-105">
            <CardContent className="p-4">
              <img 
                src={movie.poster} 
                alt={movie.title} 
                className="h-40 w-full object-cover rounded-md mb-3"
              />
              <h2 className="text-lg font-semibold">{movie.title}</h2>
              <p className="text-sm text-gray-400">{movie.year} | ⭐ {movie.rating} | {movie.genre}</p>
              <Button variant="outline" className="mt-2 w-full">View Details</Button>
            </CardContent>
          </Card>
        )) : (
          <p className="text-center col-span-full text-gray-500">No movies found</p>
        )}
      </section>
    </div>
  );
};

export default WatchitHomepage;

