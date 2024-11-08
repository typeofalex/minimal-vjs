## Minimal yjs / syncedStore example with Vue 3

This repo wants to show a minimal CRDT project, using SyncedStore / yjs to let users collaboratively share and edit arbitrary data.

## Usage
The project synchronises data using WebRTC, so the users need a signaling server so they can find each other, the rest works purely peer to peer.
The signaling server is the one provided by yjs WebRTC provider. 

### Start signaling server
```
cd signaling
docker compose up -d
```

### Build and start the Vue project
```
cd frontend
npm install
npm run dev
```

## Credits
This is just a showcase. The work has been done by yjs and SyncedStore
https://github.com/yjs/yjs
https://github.com/YousefED/SyncedStore
