# Telugu Farmer API

## Overview
An AI-assisted crop recommendation and farming support API for Telugu farmers. Provides crop recommendations, profit estimates, weather data, drone booking, farmer discussions, and agricultural content — all with Telugu language support.

## Architecture
- **Runtime**: Node.js 20
- **Framework**: Express.js
- **Entry point**: `src/server.js`
- **Frontend**: Static HTML/JS/CSS served from `public/index.html` by the Express server itself
- **Port**: 5000

## Key Features
- Crop recommendation engine based on season, soil type, and irrigation
- Profit/economics calculator per crop
- Weather integration via OpenWeatherMap API
- Reverse geocoding via OpenStreetMap Nominatim (no key required)
- Drone booking (simulated or via external API)
- In-memory farmer discussion board
- Ad/branding portal
- Agricultural content feed
- Optional LLM-generated Telugu explanations

## Project Structure
```
src/server.js       - Main Express server (API + static file serving)
public/index.html   - Full frontend (single HTML file with embedded JS/CSS)
package.json        - Dependencies and scripts
.env                - Environment variables (copy of .env.example with PORT=5000)
```

## Environment Variables
- `PORT` - Server port (default: 5000)
- `OPENWEATHER_API_KEY` - OpenWeatherMap API key for weather data
- `DRONE_API_BASE_URL` - External drone booking API base URL (optional)
- `DRONE_API_KEY` - External drone booking API key (optional)
- `LLM_API_URL` - LLM endpoint for Telugu AI explanations (optional)
- `LLM_API_KEY` - LLM API key (optional)

## Development
```bash
npm run dev    # Start with file watching (node --watch)
npm start      # Start without watching
```

## API Endpoints
- `GET /health` - Health check
- `GET /api/weather?lat=&lon=` - Weather forecast
- `POST /api/recommendations` - Crop recommendations + profit
- `GET /api/location/reverse?lat=&lon=` - Reverse geocoding
- `POST /api/profit` - Custom profit calculation
- `POST /api/drone/book` - Drone booking
- `GET /api/ads` - Agricultural ads
- `GET /api/content` - Educational content
- `GET /api/discussions` - Discussion posts
- `POST /api/discussions` - Create discussion post
- `GET /api/discussions/:postId/comments` - Get comments
- `POST /api/discussions/:postId/comments` - Add comment
- `POST /api/ads/request` - Ad/branding request

## Notes
- In-memory storage (discussions, ad requests reset on server restart)
- For production use, replace in-memory stores with a database
- Frontend uses relative API URLs (no hardcoded localhost) to work through Replit's proxy
