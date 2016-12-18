# standalone-rtc-server

A standalone rtc srever running on socket.io

## Listened Events

### `create or join`

Message required:
```javascript
{
  room: 'roomId', // The room id user applied.
}
```

3 events may emit from server:

#### `created`: when there is no client in room, user will create a new room.

the return data is unique `id`.

#### `joined`: when there are some clients in room, and not full, user will join the room.

the return data is:
```javascript
{
  clientId: '', // the unique id
  roomClients: [] // the online clients's id
}
```

#### `full`: when the room is full, user's apply to join this room will abort.

Nothing returned then full.

### `communication`

This event used for rtc communication.

`message` refer to:
```javascript
{
  type: 'type', // this include: offer, answer, candidate
  sendTo: 'someId', // required, send message to others.
  sender: 'myId', // the sender's id, 2-ways communication need this.
  desc: {}, // desc, createOffer or createAnswer need it.
  label: event.candidate.sdpMLineIndex, // the candidate label
  id: event.candidate.sdpMid, // the candidate id
  candidate: event.candidate.candidate // the candidate object.
}
```