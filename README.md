# 📹 Emmogle - Real-Time P2P Video Chat & Messaging

A full-stack, Omegle-style 1-on-1 random video calling and live messaging web application. The platform enables anonymous, instant browser-to-browser media streaming powered by WebRTC and real-time signaling via Socket.io and TypeScript.

---

## 🚀 Key Features

- **⚡ Instant 1-on-1 Matchmaking:** Automatically pairs waiting users into isolated peer rooms using dynamic UUID room generation.
- **🎥 Low-Latency P2P Video & Audio:** Direct browser-to-browser video streaming utilizing native WebRTC APIs (`RTCPeerConnection`, `MediaDevices.getUserMedia`).
- **💬 Real-Time In-Session Chat:** Integrated synchronous text messaging running over WebSockets concurrently with video.
- **🔄 Session & Disconnect Handling:** Real-time detection of peer disconnects, automated room cleanup, and smooth session resetting.
- **👥 Live Online Presence:** Broadcasts live counts of active users connected to the platform.
- **🛡️ Type-Safe Signaling Backend:** Written in TypeScript to ensure structured event handling, reliable signaling handshakes, and predictable state transitions.

---

## 🛠️ Architecture & Tech Stack

### **Frontend (Client)**
- **JavaScript (ES6+) & HTML5/CSS3**
- **Vite** — Fast, modern frontend tooling and bundling
- **WebRTC API** — ICE candidate exchange, SDP offer/answer negotiation, and media streaming
- **Socket.io Client** — Real-time signaling and chat communication

### **Backend (Server)**
- **Node.js & Express** — Application server framework
- **TypeScript** — Strongly typed server-side development
- **Socket.io** — Signaling server for WebRTC handshakes and messaging relays
- **UUID** — Unique room identifier generation for matchmaking queues

---

## ⚙️ Getting Started

### Prerequisites
- [Node.js](https://nodejs.org/) (v16 or higher recommended)
- npm or yarn

### Installation & Setup

1. **Clone the repository** (or navigate to the project directory):
   ```bash
   git clone https://github.com/Divyshek0/emmogle.git
   cd emmogle
   ```

2. **Start the Backend Server**
   Open a terminal and run:
   ```bash
   cd server
   npm install
   npm start
   ```
   *The signaling server will start on `http://localhost:8000`.*

3. **Start the Frontend Client**
   Open a new terminal window and run:
   ```bash
   cd client
   npm install
   npm run dev
   ```
   *Vite will start the dev server (typically on `http://localhost:5173`). Open this URL in your browser.*

---

## 🔄 How It Works (WebRTC Signaling Workflow)

1. **User Connection**: When a user clicks *Start*, the client connects to the Socket.io server and enters the matchmaking queue.
2. **Room Allocation**: The server either pairs the user with an already waiting peer (`p1`) or initializes a new room (`p2`).
3. **Signaling Exchange**:
   - `p1` generates a WebRTC SDP offer and transmits it through Socket.io.
   - `p2` receives the offer, sets its remote description, generates an SDP answer, and returns it.
   - Both clients exchange ICE candidates via the signaling server to establish the optimal direct P2P network path.
4. **Peer-to-Peer Communication**: Once connected, audio and video streams flow directly between peers with ultra-low latency, bypassing the server.
