# Durak.md
## Application Suitability
### Why is this application relevant?
<p>Durak.md is a multiplayer card game that allows players to join a lobby, play games in real time, and keep track of their performance. A lobby system helps manage game sessions, allowing players to join, create, or leave games seamlessly. The application will offer real-time gameplay, messaging, and a score tracking feature.<p>
<p>This project is relevant because it addresses the complexities of real-time multiplayer games, where multiple users need to interact simultaneously without significant delays. Microservices provide a scalable and fault-tolerant way to manage various game components like lobbies, user authentication, game logic, and score tracking.</p>

### Why does this application require a microservice architecture?
<p>A game like Durak.md has several independent components that are best managed as microservices:<p>
  
- Lobby management for real-time communication using WebSockets.
- Game engine for handling the game logic, turns, and game states.
- User management for player authentication, profile, and session tracking.
- Score tracking for updating and displaying player rankings and stats.

<p>By using microservices, each service can be developed, deployed, and scaled independently. For example, the Lobby service can be scaled separately if many users are waiting to join games, without impacting the game engine or user services. This also ensures fault tolerance—if the Game Engine service fails, it won’t crash the Lobby or User Management services.<p>

## Service Boundaries
![Use Case](https://github.com/In5al/PAD/blob/main/Lab1/diagram.jpg)

### Architecture

- Lobby Service - Handles WebSocket-based real-time communication for game lobbies, allowing players to join, leave, and chat in game rooms
- Game Engine Service - Manages the core game logic, including card dealing, turns, and gameplay rules.
- User Service - Manages user authentication, profiles, and session tracking.
- Score Tracking Service - Stores and retrieves player scores, ranks, and past game data.
- Notification Service - Sends notifications for game invites, moves, and real-time updates using WebSockets

## Technology Stack and Communication Patterns

### Lobby Service: 
- Backend: Python with Flask for HTTP APIs and WebSockets for real-time communication.
- Database: Redis for in-memory data storage (e.g., lobby details).
- Communication: WebSocket for real-time updates; REST for non-time-sensitive data.
  
### Game Engine Service:
- Backend: Python with Flask, handling game logic and rules.
- Database: MongoDB for storing game states.
- Communication: REST API for communication with the Lobby Service.

### User Service:
- Backend: Python (Flask).
- Database: PostgreSQL for user data.
- Authentication: JWT for secure session management.

### Score Tracking Service:
- Backend: Python (Flask).
- Database: Redis for real-time score tracking.
- Communication: REST API to query and update user scores.

## Data Management

### Lobby Service
Endpoint: `/api/lobby/join`
   - **Method**:  WebSocket
   - **Data Received**:
```json
{
  "user_id": "string",
  "lobby_id": "string"
}
```
- **Responses**:
  - **200**:
    ```json
       {
           "msg": "Joined lobby successfully."
       }
       ```
  - **404**:
    ```json
       {
           "msg": "Lobby not found."
       }
       ```

Endpoint: `/api/lobby/create`
   - **Method**:  POST
   - **Data Received**:
```json
{
  "user_id": "string",
  "game_type": "string"
}
```
- **Responses**:
  - **201**:
    ```json
       {
           "msg": "Lobby created successfully."
       }
       ```
  - **400**:
    ```json
       {
           "msg": "Invalid data."
       }
       ```

Endpoint: `/api/lobby/leave`
   - **Method**:  WebSocket
   - **Data Received**:
```json
{
  "user_id": "string",
  "lobby_id": "string"
}
```
- **Responses**:
  - **200**:
    ```json
       {
           "msg": "Left lobby successfully."
       }
       ```
  - **404**:
    ```json
       {
           "msg": "Lobby not found."
       }
       ```
    ## Game Engine Service

Endpoint: `/api/game/start`
   - **Method**:  POST
   - **Data Received**:
```json
{
  "lobby_id": "string",
  "players": ["string"]
}

```
- **Responses**:
  - **201**:
    ```json
       {
           "msg": "Game started successfully."
       }
       ```
  - **400**:
    ```json
       {
           "msg": "Invalid lobby ID."
       }
       ```

Endpoint: `/api/game/move`
   - **Method**:  POST
   - **Data Received**:
```json
{
  "game_id": "string",
  "player_id": "string",
  "move": "object"
}
```
- **Responses**:
  - **200**:
    ```json
       {
           "msg": "Move accepted."
       }
       ```
  - **400**:
    ```json
       {
           "msg": "Invalid move."
       }
       ```
    
