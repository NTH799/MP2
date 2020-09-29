# MP2
###Nicholas Hillis

This assignment uses code from the following github repository: https://github.com/joshheinrichs/go-chat-tcp

### Setup
Using two terminals you can run this with \
`go run server.go` and
 `go run client.go`
 
### Client

The client uses goroutines to create lobbies that are used to send messages between clients.
The server will only send logs on what the clients are up to using time to index the logs.

####functions:
* `Read(conn net.Conn)` is a function that reads from the connection socket and gives it to the console
* `Write(conn net.Conn)` creates a reader and writer to  get the message and send it to the connection socket
* `main()` starts the goroutines to handle the connection

The client does not have a lot of code as the server manages and handles all the functions that are typed in the client terminal

### Server

The server holds the bulk of the code and has a lot of defaulted errors to print out as the clients run.
Please note that the goland errors of CONN_PORT and CONN_TYPE do not affect the running of the program and will create errors if deleted. I have experimented with fixing
this issue as well as trying a user input but none of those ideas worked.

####functions:
* `NewLobby()` creates a lobby which needs to be made AND joined to send messages
* `(lobby *Lobby) Listen` takes a previously designed lobby struct and has it listen for messages and uses cases to implement all the various interactions between client and lobby.
* `(lobby *Lobby) Join` first checks to see if the MAX_CLIENTS has been reached and if not it allows for another client to join
* `(lobby *Lobby) Leave(client *Client)` handles when a client types `/leave`
* `(lobby *Lobby) DeleteChatRoom(chatRoom *ChatRoom)` checks to see if a chatroom is either expired or empty and then deletes it
* `(lobby *Lobby) Parse(message *Message)` handles the sent messages to the lobby by using cases to see if the message is actually a command
* `(lobby *Lobby) SendMessage(message *Message) ` tries to send the message but returns an error if you are not in a chatroom
* `(lobby *Lobby) CreateChatRoom(client *Client, name string)` arguably the most important function, this creates the chat rooms that allow for messaging
* `JoinChatRoom, LeaveChatRoom, ChangeName, ListsChatRooms, and Help` are all commands that are explained near the bottom


### Chat Commands

The following special chat commands exist in the program: 

* `/create chatroom` creates a chat room named chatroom
* `/join chatroom` joins a chat room named chatroom
* `/leave` leaves the current chat room (replaces EXIT in this problem set)
* `/list` lists all chat rooms
* `/name Nick` changes the client name to Nick
* `/help` lists all commands
* `/quit` quits the program

Any other text sends as a message to the current chat room.