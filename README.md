# Real-Time Location Tracking Application

## Overview
This is a real-time location tracking application that allows users to share their current location with others through a web interface. The application uses geolocation to track a user's position and displays it on an interactive map. When multiple users connect to the application, each user's location is displayed on the map with markers that update in real-time.

## Features
- Real-time location tracking using browser's Geolocation API
- Interactive map display using Leaflet.js
- Real-time updates via Socket.IO
- Automatic removal of disconnected users from the map
- Responsive design that works on both desktop and mobile devices

## Tech Stack
- **Frontend**:
  - HTML/CSS/JavaScript
  - Leaflet.js (for interactive maps)
  - Socket.IO client (for real-time communication)

- **Backend**:
  - Node.js
  - Express.js (web server framework)
  - Socket.IO (for WebSocket connections)
  - EJS (templating engine)

## Project Structure
```
├── app.js                 # Main server file
├── package.json           # Project dependencies
├── public/                # Static assets
│   ├── css/               # CSS stylesheets
│   │   └── style.css      # Main stylesheet
│   └── js/                # Client-side JavaScript
│       └── script.js      # Main client-side logic
└── views/                 # EJS templates
    └── index.ejs          # Main HTML template
```

## How It Works

### Server-Side (app.js)
The server is built with Express.js and Socket.IO to handle HTTP requests and WebSocket connections:

1. **Express Setup**: Configures the web server and serves static files from the 'public' directory.
2. **Socket.IO Integration**: Establishes WebSocket connections for real-time communication.
3. **Event Handling**:
   - `connection`: Triggered when a new user connects
   - `send-location`: Receives location data from clients and broadcasts it to all connected users
   - `disconnect`: Handles user disconnection and notifies other clients

### Client-Side (script.js)
The client-side code handles geolocation tracking and map display:

1. **Geolocation Tracking**: Uses the browser's Geolocation API to track the user's position.
2. **Socket.IO Communication**: Sends location updates to the server and receives updates from other users.
3. **Map Display**: Uses Leaflet.js to display an interactive map with markers for each connected user.
4. **Marker Management**: Adds, updates, and removes markers based on user connections and disconnections.

## How to Run the Application

### Prerequisites
- Node.js (v12 or higher)
- npm (Node Package Manager)

### Installation

1. Clone the repository or download the source code:
   ```bash
   git clone https://github.com/Soham8763/realtime-tracking.git
   # or download and extract the zip file
   ```

2. Navigate to the project directory:
   ```bash
   cd realtime-tracking
   ```

3. Install the dependencies:
   ```bash
   npm install
   ```

### Running the Application

1. Start the server:
   ```bash
   npm start
   # or
   node app.js
   ```

2. Open your web browser and navigate to:
   ```
   http://localhost:3000
   ```

3. Allow location access when prompted by your browser.

4. Share the URL with others on your local network to see multiple users on the map.

## Socket.IO Communication Flow

1. **Client Connects**:
   - A new Socket.IO connection is established when a user loads the page.
   - The server assigns a unique socket ID to the client.

2. **Location Sharing**:
   - The client obtains the user's location using the Geolocation API.
   - The client emits a `send-location` event with latitude and longitude data.
   - The server receives this event and broadcasts a `receive-location` event to all connected clients, including the sender's socket ID.

3. **Map Updates**:
   - All clients receive the `receive-location` event and update their maps accordingly.
   - If a marker for the socket ID already exists, its position is updated.
   - If no marker exists, a new one is created.

4. **User Disconnection**:
   - When a user closes the page or loses connection, the Socket.IO `disconnect` event is triggered.
   - The server emits a `user-disconnected` event with the disconnected user's socket ID.
   - All remaining clients remove the disconnected user's marker from their maps.

## Notes
- The application requires location permissions from the browser.
- For best results, use a modern browser with Geolocation API support.
- The map is centered on the most recently updated location.

## Future Enhancements
- User authentication
- Custom user names and avatars
- Route tracking and history
- Distance calculation between users
- Private tracking groups