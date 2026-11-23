# ReelMatch

Picking a movie in a group usually means passing one screen around. In ReelMatch, people join a room on their phones and swipe on titles while a laptop or TV can show the shared state. [Try ReelMatch](https://reelmat.ch/)

## Keeping votes and room state in sync

The Next.js client sends a vote to a FastAPI service, which persists votes and tallies in PostgreSQL. The phone receives an acknowledgment. A versioned event stream updates clients that are following the room.

A request can reach the server even if the phone loses the response. Repeating the same vote leaves the tally stable. A client reconnecting to the event stream can replay missed updates when they are still available, or recover from a fresh room snapshot.

## Testing the behavior

The vote tests cover repeated submissions and changes to an existing vote. The realtime client tests exercise how a client applies room updates. For movie search, I track exact-title results separately from exploratory ranking so I can catch regressions in familiar-title lookups while improving discovery.
