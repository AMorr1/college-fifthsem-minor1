# Project Title:- "AUTOMATED CRYPTOGRAPHIC FILE TRANSFER"


# Aim of the repository
This is the repository maintained for the progress report of the work done in the each day in the Minor Project 1.


# Problem Statement

The client-server communication channel is widely used in many applications. These kinds of applications usually have a very protected server side, whereas the Client-side are prone to loopholes and can be hacked into by another client. 
The client-side is always vulnerable to threat attacks, or unauthorized access. The main objective of this project is to develop an Automated Cryptographic File transfer, to provide security measures at both the ends. 

# Server file(server.c)

                                                      UDP Server :
1) Create UDP socket.
2) Bind the socket to server address.
3) Wait until datagram packet arrives from client.
4) Process the datagram packet and send a reply to client.
5) Go back to Step 3.

                                                 Stages for server:-


1) Socket creation:

int sockfd = socket(domain, type, protocol)

sockfd: socket descriptor, an integer (like a file-handle)

domain: integer, communication domain e.g., AF_INET (IPv4 protocol) , AF_INET6 (IPv6 protocol)

type: communication type

SOCK_STREAM: TCP(reliable, connection oriented)

SOCK_DGRAM: UDP(unreliable, connectionless)

protocol: Protocol value for Internet Protocol(IP), which is 0. This is the same number which appears on protocol field in the IP header of a packet.(man protocols for more details)

2) Setsockopt:

int setsockopt(int sockfd, int level, int optname,const void *optval, socklen_t optlen);

This helps in manipulating options for the socket referred by the file descriptor sockfd. This is completely optional, but it helps in reuse of address and port. Prevents error such as: “address already in use”.

3) Bind:

int bind(int sockfd, const struct sockaddr *addr,socklen_t addrlen);

After creation of the socket, bind function binds the socket to the address and port number specified in addr(custom data structure). In the example code, we bind the server to the localhost, hence we use INADDR_ANY to specify the IP address.

4) Listen:

int listen(int sockfd, int backlog);

It puts the server socket in a passive mode, where it waits for the client to approach the server to make a connection. The backlog, defines the maximum length to which the queue of pending connections for sockfd may grow. If a connection request arrives when the queue is full, the client may receive an error with an indication of ECONNREFUSED.

5) Accept:

int new_socket= accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);

It extracts the first connection request on the queue of pending connections for the listening socket, sockfd, creates a new connected socket, and returns a new file descriptor referring to that socket. At this point, connection is established between client and server, and they are ready to transfer data.


                                                                              Necessary Functions :

int socket(int domain, int type, int protocol)

Creates an unbound socket in the specified domain.

Returns socket file descriptor.

                                                                                     Arguments :

1) domain – Specifies the communication
   
   domain ( AF_INET for IPv4/ AF_INET6 for IPv6 )
   
   type – Type of socket to be created
   
   ( SOCK_STREAM for TCP / SOCK_DGRAM for UDP )
   
   protocol – Protocol to be used by socket.
   
   0 means use default protocol for the address family.

int bind(int sockfd, const struct sockaddr *addr, socklen_t addrlen)

Assigns address to the unbound socket.

2) sockfd – File descriptor of socket to be binded
  
  addr – Structure in which address to be binded to is specified
  
  addrlen – Size of addr structure


ssize_t sendto(int sockfd, const void *buf, size_t len, int flags,const struct sockaddr *dest_addr, socklen_t addrlen)

Send a message on the socket

3) sockfd – File descriptor of socket
   
   buf – Application buffer containing the data to be sent
   
   len – Size of buf application buffer
   
   flags – Bitwise OR of flags to modify socket behaviour
   
   dest_addr – Structure containing address of destination
   
   addrlen – Size of dest_addr structure

ssize_t recvfrom(int sockfd, void *buf, size_t len, int flags,struct sockaddr *src_addr, socklen_t *addrlen)

Receive a message from the socket.

4) sockfd – File descriptor of socket
   
   buf – Application buffer in which to receive data
   
   len – Size of buf application buffer
   
   flags – Bitwise OR of flags to modify socket behaviour
   
   src_addr – Structure containing source address is returned
   
   addrlen – Variable in which size of src_addr structure is returned

int close(int fd)

Close a file descriptor

5) fd – File descriptor
