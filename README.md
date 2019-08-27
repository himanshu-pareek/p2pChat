# Peer to Peer (P2P) Chat Application
A peer-to peer (P2P) application is an application primitive, where there is no dedicated central server nodes. Every node in the network canconnect with each other and transfer data among themselves. In this P2P chat application, weconsidered a close group of friends who want to chat with each other. The chat application uses TCP as the underlying transport layer protocol. For P2P implementation, every instanceof the chat application runs a TCP server (we call this as peer-chat server) where the chat application listens for incoming connections. The protocol details are as follows. The same process of the application also runs one or multiple TCP clients (based on the number of peers) to connect to the other users and transfer messages.

## Design Requirments
<ol>
  <li> The entire chat application runs under a single process. So, the peer-chat server is an iterative server, and NOT a concurrent server.</li>
  <li> Every participating user maintains a <i>user_info</i> table that contains-<br />
  <ol>
    <li> Name of the friend, </li>
    <li> IP address of the machine where the chat application is running, </li>
    <li> Port number at which the peer-chat server is running. </li>
  </ol>
    This table is static and shared a priori with all the participatingusers. </li>
  <li> For the chat purpose, a user enters message using the keyboard. The message format is as follows:<br />
    <i> friend name/<msg></i> where <i>friendname</i> is the name of the friend to whom the user wants to send message, and <i>msg</i> is the corresponding message. </li>
  <li> The communication mode is asynchronous, indicating that a user can enter the message any time. The console should always be ready to accept a new message from the keyboard, unless the user is already typing another message.
</ol>

## Protocol Primitives:
<ol>
  <li> Every instance of the chat application runs a TCP server which binds itself to a well known port and keep on listening for the incoming connections. There can be a maximum of 5 peers (users), so a maximum of 5 connections need to be supported. </li> 
  <li> Once the server receives a connection, it accepts the connection, reads the data from that connection, extracts the message, and displays it over the console. </li>
  <li> Once a user enters a message through keyboard,<br />
    <ol>
      <li> The message is read from the <i>stdin</i>, the standard input file descriptor. </li>
      <li> The application checks whether a client socket to the corresponding server already exists. If a client socket does not exist, then a client socket is created to the corresponding server based on the lookup over <i>user_info</i> table. </li>
      <li> The message is sent over the client socket. </li>
    </ol>
  </li>
  <li> If there is no activity over the client socket for a timeout duration, then the client socket is closed. </li>
</ol>

## Using the application:
<ol>
  <li> Write name of the user, ip address and port number of the corresponding user's machine in users.txt file (space seperated). </li>
  <li> Copy users.txt file to all the machines in the same folder where the .cpp file is. </li>
  <li> Compile the source code. <br />
    <b>g++ chat_server.cpp -std=c++11</b>
  </li>
  <li> Run the application using: <br />
    <b>./a.out port-number-of-your-machine</b>
  </li>
</ol>



