# TruGo - Backend

Backend application for an online game to replicate **Truco Gauderiano**, a traditional card game from Gaucho culture.

> **Note**: This backend was developed by me and [@cauafsantosdev](https://github.com/cauafsantosdev). The complete project repository is maintained at: [TruGo - Original Repository](https://github.com/cauafsantosdev/TruGo/tree/dev)

## 📚 Documentation in Other Languages

- 🇬🇧 [English](README.md)
- 🇪🇸 [Español](README_ESP.md)
- 🇧🇷 [Português](README_PT.md)

## 📋 Overview

TruGo is a multiplayer system based on WebSocket that allows players to create rooms, join teams, and play truco in real time. The project uses Go (Golang) as a backend language, offering real-time bidirectional communication with WebSocket.

## 🎮 Features

- **Real-Time Multiplayer**: Bidirectional communication with WebSocket
- **Room System**: Dynamic creation and management of game rooms
- **Teams**: Division of players into teams
- **State Management**: Tracking of game state, rounds, cards, and bets
- **Event-Based API**: JSON payload structure for different types of actions

## 📁 Project Structure

```
BackEnd/
├── main.go                 # Entry point, WebSocket server configuration
├── go.mod                  # Project dependencies
├── models/
│   ├── card.go            # Card definitions
│   ├── game.go            # Game, room and state structures
│   ├── player.go          # Player definition
│   └── payloads.go        # Payload structures for communication
├── ws/
│   ├── handler.go         # WebSocket event router
│   ├── game.go            # Main game logic
│   └── salas.go           # Room management
└── teste/                 # Test files and configuration
    ├── config.js
    ├── game01.js, game02.js
    ├── payload.md
    └── player*.html       # HTML interfaces for testing
```

## 🔧 Dependencies

- **Go 1.24.4** or higher
- **gorilla/websocket**: WebSocket library for Go
- **google/uuid**: UUID generation

```go
require (
    github.com/google/uuid v1.6.0
    github.com/gorilla/websocket v1.5.3
)
```

## 🚀 How to Run

### Prerequisites

- Go installed on your machine ([Download](https://golang.org/dl/))

### Installation and Execution

1. **Clone or navigate to the project:**
   ```bash
   cd /home/steven/Steven/projetos/TruGo/BackEnd
   ```

2. **Install dependencies:**
   ```bash
   go mod download
   ```

3. **Run the server:**
   ```bash
   go run main.go
   ```

   The server will start and wait for WebSocket connections:
   ```
   TruGo WebSocket started
   ```

4. **Connect to WebSocket:**
   - Address: `ws://localhost:8080/ws`
   - Or configure the port via the `PORT` environment variable

## 📡 WebSocket API

The server communicates via JSON messages. Each message has a `type` that determines the action to be executed.

### Message Types

#### Room Dynamics
- `CRIAR_SALA` - Create a new game room
- `ENTRAR_SALA` - Enter an existing room
- `ENTRAR_EQUIPE` - Choose a team/team
- `LISTAR_SALAS` - List all available rooms

#### Gameplay
- `JOGAR_CARTA` - Play a card
- `APOSTAR` - Place a bet
- Other game actions

### Payload Example

```json
{
  "type": "CRIAR_SALA",
  "sala_id": "uuid-of-room",
  "jogador_id": "uuid-of-player",
  "data": {}
}
```

## 🎯 Game Structure

### Room (Sala)
- Status: Current room status
- Game: Current game state
- Players: List of players in the room

### Game State (EstadoJogo)
- State: Current phase of the game
- Round: Round information
- Team01/Team02: Competing teams
- Deck: Available cards
- PlayerHand: Responsible player
- PlayerIdx: Current player index

### Player (Jogador)
- Unique ID
- Hand of cards
- Team
- Status in the room

### Card (Cartas)
- Suit
- Value
- Truco score

## 🧪 Tests

There are test files in the `teste/` folder:
- `game01.js`, `game02.js` - Test scripts
- `player*.html` - HTML interfaces for testing multiple players
- `payload.md` - Payload documentation
- `config.js` - Test configuration

## 🔌 Connection Flow

1. Client connects to `/ws` endpoint
2. Server accepts the WebSocket connection
3. Client sends JSON messages with actions
4. Server processes via `EscolhaType()` and routes to appropriate handler
5. Server returns response or notifies other players

## 📝 Notes

- The server uses `sync.Mutex` to manage safe concurrent access to rooms
- All rooms are kept in memory during execution
- Communication is full-duplex, allowing real-time notifications

## 🤝 Contributing

To contribute with improvements, test your implementation with the files in `teste/`.

## 📄 License

This project is part of TruGo - a project to replicate Truco Gauderiano.

---

**Developed with Go and WebSocket** 🎮
