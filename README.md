# File Transfer Protocol (FTP) Client and Server Networking Project
 
## Project Overview

    Objective: Create a client-server application where the client can upload files to the server, download files from the server, and list available files in the server’s directory.
    Features:
        Server listens for client connections and processes commands.
        Supported commands:
            UPLOAD <filename>: Upload a file to the server.
            DOWNLOAD <filename>: Download a file from the server.
            LIST: List all files in the server’s directory.
        Basic authentication with a hardcoded username/password.
        Binary file transfer for handling any file type (text, images, etc.).
    Tools:
        Raw sockets (<sys/socket.h> on Linux, Winsock on Windows).
        Standard C++ for file I/O and string processing.
        No external libraries (to keep it simple).
    Directory Structure:
        server.cpp: Server code.
        client.cpp: Client code.
        server_files/: Directory where the server stores uploaded files.
    Learning Outcomes:
        Socket programming (TCP connections, send/receive).
        Protocol design (command parsing, message formats).
        Binary file transfer (handling arbitrary data).
        File system operations (reading/writing files, directory listing).
        Basic multithreading for handling multiple clients.

Implementation Details

    Protocol:
        Commands are sent as strings terminated by \n.
        File transfers are preceded by a 4-byte length field (network byte order) to indicate the file size.
        Responses from the server start with OK or ERROR followed by a message.
    Authentication:
        Hardcoded credentials: username=user, password=pass.
        Client sends credentials as AUTH user pass before other commands.
    Error Handling:
        Handles socket errors, file not found, invalid commands, and authentication failures.
        Graceful disconnection on errors.
    Cross-Platform Notes:
        Uses preprocessor directives (#ifdef _WIN32) for Windows-specific socket initialization (Winsock).
        Directory listing uses dirent.h (Linux) or Windows API.

How to Run

    Prerequisites:
        C++ compiler (g++, MSVC, etc.) with C++17 support.
        Windows: Link against Ws2_32.lib (included in the server code via #pragma).
        Linux: No additional libraries needed.
    Setup:
        Create a directory named server_files in the same directory as server.cpp to store uploaded files.
        Compile the server and client code:
        bash

    g++ server.cpp -o server -std=c++17
    g++ client.cpp -o client -std=c++17
    On Windows, use a suitable compiler (e.g., MSVC) and ensure Winsock is linked.

Run the Server:

    Start the server first:
    bash

    ./server
    It will listen on port 8888 and print "Server listening on port 8888...".

Run the Client:

    In another terminal, run the client:
    bash

    ./client
    The client connects to 127.0.0.1:8888 and authenticates with user/pass.

Interact with the Client:

    Enter commands like:
        UPLOAD test.txt: Uploads test.txt from the client’s directory to the server.
        DOWNLOAD test.txt: Downloads test.txt from the server to the client’s directory.
        LIST: Lists all files in the server’s server_files directory.
        EXIT: Closes the client.

