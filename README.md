# TicTacToe Program – MultiPlayer
> This is the README file for [Lab_5](https://osu.instructure.com/courses/97443/files/27903209/download?download_frd=1)

**NAME:** Conner Graham, Ben Nagel  
**DATE:** 03/04/2021

## Table of Contents:
- [Included Files](#included-files)
- [TicTacToe Server](#tictactoe-server)
  - [Description](#description-server)
  - [Usage](#usage-server)
  - [Assumptions](#assumptions-server)
- [TicTacToe Client](#tictactoe-client)
  - [Description](#description-client)
  - [Usage](#usage-client)
  - [Assumptions](#assumptions-client)

## Included Files
- [makefile](https://github.com/CSE-5462-Spring-2021/assignment5-conner-ben/blob/main/makefile)
- Server (Player 1) Design Document - [Design_Server.md](https://github.com/CSE-5462-Spring-2021/assignment5-conner-ben/blob/main/Design_Server.md)
- TicTacToe Server Source Code - [tictactoeServer.c](https://github.com/CSE-5462-Spring-2021/assignment5-conner-ben/blob/main/tictactoeServer.c)
- Client (Player 2) Design Document - [Design_Client.md](https://github.com/CSE-5462-Spring-2021/assignment5-conner-ben/blob/main/Design_Client.md)
- TicTacToe Client Source Code - [tictactoeClient.c](https://github.com/CSE-5462-Spring-2021/assignment5-conner-ben/blob/main/tictactoeClient.c)

## TicTacToe Server
> By: Conner Graham

### DESCRIPTION <a name="description-server"></a>
This lab contains a program called "tictactoeServer" which sets up
multiple net-enabled TicTacToe games that clients can play simultaneously.
This server sets up a communication endpoint for other players to communicate
with, initializes a set of game boards, and processes any commands received
from other players. These commands can include initialize a game of TicTacToe
when a player requests one or responding to other player's moves until a
winner is found or the game is a draw. If a player takes too long to respond,
the game times out and is reset for another player to play. If no player
responds to the server for a period of time, the server times out and all
ongoing games are reset for other players to play. The specific tasks the
server performs are as follows:
- Create and bind server socket from user provided port
- Print server info and listen for commands
- Initialize all game boards
- Set server timeout time
- Accept UDP DGRAM command from waiting client
- Process the command for the corresponding game
- Reset ongoing games that have timed out
- Reset all games if server has timed out

If the number of arguments is incorrect or the remote port is
invalid, the program prints appropriate messages and shows how to
correctly invoke the program. 

### USAGE <a name="usage-server"></a>
Start the TicTacToe P1 Server with the command...
```sh
$ tictactoeServer <local-port>
```

If any of the argument strings contain whitespace, those
arguments will need to be enclosed in quotes.

### ASSUMPTIONS <a name="assumptions-server"></a>
- It is assumed that the Player 1 (server) will terminate the server
  when they are done playing, in which case clients will need to
  find another serevr to connect to if they sich to play.
- It is assumed that the client will never enter the int -1 (char '/')
  for a move as it is being used as an error code.
- It is assumed that the player making the "New Game" request will
  always send their messages from the same IP address and port number
  used to make the request.

## TicTacToe Client
> By: Ben Nagel

### DESCRIPTION <a name="description-client"></a>
This lab contains a program called "tictactoeClient" which creates and sets up a datagram transfer protocal client. This client sends datagrams to the specified server( IP address and port), reads in a datagram from the server and sends a datagram back. This process continues until a winner or a tie has been reached.

The specific tasks the client performs are as
follows:
- Create server socket from user provided IP/port
- Perform datagram transfer over the connection
- Terminate the connection to the server

### USAGE <a name="usage-client"></a>
Start the TicTacToe P2 Client with the command...
```sh
$ tictactoeClient  <local-port> <remote-IP>
```

If any of the argument strings contain whitespace, those
arguments will need to be enclosed in quotes.

### ASSUMPTIONS <a name="assumptions-client"></a>
- Client send and recieves a 40 byte datagram(excluding the inital datagram which is 2 bytes)
- A datagram is sent and recevied 
- The spaces on the tictactoe board are 1-9
- Player 1 is the "server": they are the one who calls bind()   
- Player 1 goes first
- On any errors, close the connection 
- It is assumed that the IP addresses 0.0.0.0 and 255.255.255.255 are invalid remote server addresses to connect to as they are reserved values.
