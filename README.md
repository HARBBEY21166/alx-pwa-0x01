# MoviesDatabase API Documentation

## API Overview
The MoviesDatabase API provides comprehensive access to an extensive movie database, allowing developers to retrieve detailed information about movies, including titles, release years, genres, and image resources. This API enables rich movie-related application development with flexible querying capabilities.

## API Version
**Current Version**: v1 (as of January 2024)

## Available Endpoints

1. `/titles`
   - Retrieve movie titles with advanced filtering
   - Supports pagination, year filtering, genre selection
   - Returns detailed movie metadata

2. `/title/{id}`
   - Fetch specific movie details by unique identifier
   - Provides comprehensive information about a single movie

3. `/genres`
   - List available movie genres
   - Useful for building genre-based filters

## Request and Response Format

### Typical Request
```json
{
  "year": 2023,
  "genre": "Action",
  "limit": 10,
  "page": 1
}
```

### Typical Response
```json
{
  "results": [
    {
      "id": "unique_movie_id",
      "titleText": { "text": "Movie Title" },
      "primaryImage": { "url": "image_url" },
      "releaseYear": { "year": 2023 }
    }
  ],
  "total": 100,
  "page": 1
}
```

## Authentication
- Requires RapidAPI authentication
- API key must be included in request headers:
  - `x-rapidapi-host`: "moviesdatabase.p.rapidapi.com"
  - `x-rapidapi-key`: Your unique API key

## Error Handling
- 400: Bad Request (invalid parameters)
- 401: Unauthorized (invalid API key)
- 404: Resource Not Found
- 429: Rate Limit Exceeded
- 500: Internal Server Error

## Usage Limits and Best Practices
- Rate Limit: 500 requests/month on free tier
- Recommended request caching
- Implement pagination for large datasets
- Handle potential null/undefined responses
- Use error try-catch blocks

## Example Implementation
```typescript
const fetchMovies = async (year: number, genre: string) => {
  const response = await fetch('/titles', {
    method: 'POST',
    headers: {
      'x-rapidapi-key': process.env.MOVIE_API_KEY
    },
    body: JSON.stringify({ year, genre })
  });
  
  if (!response.ok) {
    throw new Error('Movie fetch failed');
  }
  
  return response.json();
};
```