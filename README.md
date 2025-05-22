# Network File System (NFS) Implementation

## Project Overview
This project implements a distributed Network File System (NFS) with a centralized Naming Server (NS) and multiple Storage Servers (SS). Clients can perform various file operations through this system, including reading, writing, copying, creating, and deleting files.

## Architecture
The system consists of three main components:

1. **Naming Server (NS)**: 
    - Acts as a central directory service
    - Maps file paths to appropriate storage servers
    - Manages storage server registration
    - Implements LRU caching for frequently accessed paths

2. **Storage Servers (SS)**:
    - Store actual file data
    - Implement read/write operations with reader-writer locks
    - Support both synchronous and asynchronous write operations
    - Handle file streaming and information retrieval

3. **Clients**:
    - Connect to the naming server to locate files
    - Perform direct operations with storage servers
    - Support various file operations (read, write, create, delete, copy)

## Features
- **Distributed Storage**: Files distributed across multiple storage servers
- **Path-based Routing**: Logical file paths mapped to physical storage locations
- **Caching**: LRU cache for efficient path-to-server lookups
- **Concurrent Access**: Reader-writer locks for handling multiple clients
- **File Operations**: Create, read, write, delete, copy, and get file info
- **Streaming Support**: Audio file streaming capability
- **Asynchronous Operations**: Large file writes handled asynchronously

## Getting Started

### Prerequisites
- GCC compiler
- POSIX-compliant system (Linux/Unix)
- Network connectivity between machines running the components

### Compilation
Use the provided script to compile all components:
```bash
./script.sh
```

### Running the System
1. **Start the Naming Server**:
```bash
./namingServer <port>
```

2. **Start Storage Servers**:
```bash
./storageServer <naming_server_ip> <naming_server_port> <ss_port> <port_for_clients> <base_path>
```

3. **Run the Client**:
```bash
./client <naming_server_ip> <naming_server_port>
```

## Client Commands
- `READ <path>`: Read file content
- `WRITE <path> <data>`: Write data to file
- `CREATE <path> <name> -f/-d`: Create file (-f) or directory (-d)
- `DELETE <path> <name>`: Delete a file or directory
- `COPY <source_path> <dest_path>`: Copy files/directories
- `GET <path>`: Get file information
- `STREAM <path>`: Stream audio file
- `EXIT`: Exit the client

## Implementation Details
- Thread-based concurrency model
- Socket programming for network communication
- Hash tables for efficient path lookups
- Semaphores for reader-writer synchronization
- Error handling for various failure scenarios