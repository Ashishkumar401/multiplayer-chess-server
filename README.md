# Multiplayer Chess Server

A Node.js backend that relays chess moves between clients in the same Socket.IO room. Each game uses a room ID so clients can subscribe to one game's moves.

## Run locally

```sh
npm ci
npm start
```

Connect two Socket.IO clients to `http://localhost:4000`. On each client, emit `join-room` with the same room ID. Have one client emit `move` with a move payload followed by that room ID. The other client receives the payload.

| Client event | Server behavior |
| --- | --- |
| `join-room(roomId)` | Joins the socket to the room and broadcasts `joined-room` to its members |
| `move(payload, roomId)` | Forwards the payload to other sockets in the specified room |
| Disconnect | Logs the disconnected socket ID |

[Read the complete event handlers](server.js). Clients supply the board interface and move payload. Legal-move checks, turn enforcement and persistent game state are outside the current server implementation.
