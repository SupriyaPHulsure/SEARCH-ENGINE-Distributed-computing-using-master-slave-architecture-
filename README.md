# SEARCH ENGINE: Distributed computing using master-slave architecture 

Tiny Google is a high data intensive search engine that enables people to search for words as form of queries. With the rise of the internet, distributed or cloud-based computing supporting data intensive applications is at the forefront. Tiny Google is an attempt to enable parallel based data processing on distributed servers in the elements network. It is a client-server based framework that indexes text documents, maintains sorted index tables and allows searching word queries over a distributed set of servers. In this project we do two things: a) Create a client-server setup using TCP sockets for document indexing and searching in the elements network and b) Implement the functionalities of a) in the Hadoop cluster using Apache Hadoop.

## SYSTEM DESIGN:

### Client Server-Based Model using TCP Sockets

The system is based on a basic client server architecture communicating with TCP/IP [1] protocol. The system has three working modules: 1) Client (user) module 2) Master-server module and 3) Worker server module. It is as shown in Figure 1. The Clients (marked orange) are the users who is using the client application for searching and indexing. The Master Server (marked white) is the main module interacts with the clients and redirects their requests to each of the worker servers (marked green). All the operations take place in the worker servers. In our system design, any server in the elements network can be initiated as the master server and multiple servers (except the master server) can act as worker servers. Worker servers are allocated dynamically based on their availability.


As far as the clients are concerned, any elements machine in the network can act as Client. The client only communicates with the master server which in turn communicates with the worker servers. All the data intensive operations are done on the worker servers. The following are the functionalities of each of the working components:

#### 1. Client: 
Interfaces with the user asking for the type of operation they want to perform. It has two types of requests: INDEX and SEARCH. Upon user’s choice it directs such requests to the Master Server.

#### 2. Master-server: 
This is the main node which acts as a server to the clients and as client to the worker servers. It can communicate with both modules simultaneously. It takes in requests from the client and initiates connections with the workers through threads, for parallel processing. The operation request that the master server sends to the workers are: MAP, REDUCE and SEARCH. MAP and REDUCE are two operations request for the indexing operation while SEARCH is for the searching operation. Upon getting the results from the workers, it re-directs them back to the clients.

#### 3. Worker Server: 
These are the nodes that actually perform the operations based on the request given from master-server. It has three functionalities:1) MAP, which creates a temporary index table for each of the file segments, 2) REDUCE, which creates the final inverted index table in a lexicographical order and 3) SEARCH, which searches for a particular word in the final inverted index table and returns a tuple of document indexes ranked by the frequency of the word occurrence in the document.
