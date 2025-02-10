# Real-Time Gaming Leaderboard

A scalable, low-latency, real-time gaming leaderboard built using **Node.js**, **Express.js**, **Redis**, and **Socket.io**.

## Features
- **Real-Time Score Updates**: Players' scores update instantly.
- **Top-N Players Query**: Fetches the top-ranked players.
- **Player Rank Lookup**: Retrieve a player's current rank quickly.
- **Nearby Rank Query**: View players ranked around a given player.
- **WebSockets for Real-Time Updates**: Push updates to clients without polling.

## Tech Stack
- **Backend**: Node.js (Express.js)
- **Database**: Redis (Sorted Sets for fast lookups)
- **Real-Time Communication**: Socket.io
- **Containerization**: Docker

## API Endpoints
### Update Player Score
```
POST /leaderboard/score/update
```
**Request:**
```json
{
  "playerId": "player123",
  "scoreDelta": 50
}
```
**Response:**
```json
{
  "playerId": "player123",
  "updatedScore": 1000,
  "currentRank": 10
}
```

### Get Top-N Players
```
GET /leaderboard/top?n=10
```
**Response:**
```json
{
  "leaderboardId": "global",
  "topPlayers": [
    { "playerId": "playerA", "score": 1500, "rank": 1 },
    { "playerId": "playerB", "score": 1490, "rank": 2 }
  ]
}
```

### Get Player Rank
```
GET /leaderboard/rank/{playerId}
```
**Response:**
```json
{
  "playerId": "player123",
  "score": 1000,
  "rank": 10
}
```

### Get Nearby Ranks
```
GET /leaderboard/nearby/{playerId}?range=5
```
**Response:**
```json
{
  "playerId": "player123",
  "startRank": 45,
  "endRank": 55,
  "players": [
    { "playerId": "playerX", "score": 1020, "rank": 44 },
    { "playerId": "player123", "score": 1000, "rank": 45 }
  ]
}
```

## Setup & Installation

### Prerequisites
- **Node.js** (>=14.x)
- **Redis** (running locally or via Docker)

### Install Dependencies
```sh
npm install
```

### Start Redis (if using Docker)
```sh
docker run -d --name redis-leaderboard -p 6379:6379 redis
```

### Run the Server
```sh
npm start
```

### WebSocket Real-Time Updates
Players receive real-time updates when their scores change.

## Deployment
To run the app inside a Docker container:
```sh
docker build -t gaming-leaderboard .
docker run -p 5000:5000 gaming-leaderboard
```

## Contributing
1. Fork the repo
2. Create a feature branch (`git checkout -b feature-name`)
3. Commit changes (`git commit -m 'Add feature'`)
4. Push to branch (`git push origin feature-name`)
5. Open a Pull Request

## License
MIT


