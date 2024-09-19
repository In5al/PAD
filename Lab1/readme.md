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
