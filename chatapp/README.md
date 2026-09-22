# chatapp

Protocol: JSON over TCP
Framing: 2 byte big endian integer followed by that many bytes.

On an invalid message the server must immediatly disconnect the client.

## Client Messages
- type: `"identify"`, name: `string`
- type: `"message"`, content: `string`
- type: `"list_lobbies"`
- type: `"join_lobby"`, id: `number`
- type: `"leave_lobby"`
- type: `"create_lobby"`, name: `string`

## Server Messages
- type: `"id_assigned"`, id: `number`
- type: `"identified"`
- type: `"error"`, error: `Error`
- type: `"joined_lobby"`, id: `number`, clients: `Client[]`
- type: `"left_lobby"`
- type: `"lobby_list"`, lobbies: `Lobby[]`
- type: `"client_joined"`, client: `Client`
- type: `"client_left"`, id: `number`
- type: `"message"`, from: `number`, content: `string`

## Other Types
- Client: id: `number`, name: `string`
- Lobby: id: `number`, name: `string`, clients: `number`
- Error: `"already_identified"` | `"not_identified"` | `"already_in_a_lobby"` | `"not_in_a_lobby"` | `"no_such_lobby"`
