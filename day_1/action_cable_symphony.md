# The Action Cable Symphony - An Illustrated Musical Adventure

- [The Action Cable Symphony - An Illustrated Musical Adventure](#the-action-cable-symphony---an-illustrated-musical-adventure)
  - [Video](#video)
  - [Notes](#notes)
    - [Server](#server)
    - [Clients](#clients)
    - [Security](#security)
    - [Latency](#latency)

## Video

https://www.youtube.com/watch?v=x3b9KlzjJNM

## Notes

- [simphony.dev](https://www.simphony.dev)

### Server

- MIDI file to JSON
- Multiparting a MIDI
- A flow of data from conductor to orchestrator members
- Conductor -> MIDI channels (instruments) -> player channel
- Clients only listen to parts they need
- Conductor tells players what instrument they are playing
- Conductor can create a buffer and send commands to player channels like play or stop
- Clients can send meta info back to conductor
- Some endpoints makes more sense to use REST than others
- Websockets do not replace REST endpoints, they just augment them
- Concerns about scability
  - AnyCable

### Clients

- Written in React
- Actions are reaction to listening on websockets
- Phone ocnnects -> Assign parts -> listen to the conductor
- Uses Tone.js and synths

### Security

- Dashboard uses Devise & JWTs
- JWTs are self contained, session encoded in token, and stateless in nature
  - They are signed, base64 encoded, with three distinct sections separated by a .
  - Header.Payload.Signature
    - Header
      - Algorith: HS256
      - Type: JWT
    - Payload
      - Subject
      - Name
      - Issued at
    - Signature
      - b64 header + b64 oayload + secret

### Latency

- Every step adds another hop and makes everything take longer
- Timesync.js
  - p2p and server syncing
  - callbacks when event offset has changed
- Ask rails server what the time is and server sends back a stamp that shows offset
- If we have load balancing, etc. server times are all different
