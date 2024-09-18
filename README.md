
# GoStore: Distributed File System

GoStore (ProjectDFS) is a simple Distributed File System (DFS) written in Go, utilizing **gRPC** and **Protocol Buffers** for communication. It provides a seamless and transparent experience for sharing data and files over a network, with support for multiple storage servers and fault tolerance via file replication. GoStore allows users to interact with remote files as if they were stored locally, using **FUSE** for user-space mounting.

## Features

- **Transparent File Access**: Files are hosted remotely but accessed as if they were on the local machine.
- **Fault-Tolerant**: Files are replicated across at least two storage servers, ensuring redundancy and data protection.
- **File Operations**: Supports basic file operations like reading, writing, deleting, copying, moving, and retrieving metadata.
- **Directory Management**: Includes operations for listing, creating, deleting, and changing directories.
- **Efficient Naming Server**: A single naming server handles file indexing and directs clients to the appropriate storage servers.

## Architecture
![image](https://github.com/user-attachments/assets/4c1cd3e4-cf25-4761-a43d-1bb2429938b2)

### Client
The client interacts with users through **FUSE**, allowing the file system to be mounted and used with traditional tools (e.g., Neovim). FUSE provides an abstraction layer that allows users to work with remote files without changing their usual workflows. 

- **FUSE** (File System in User-Space) allows file system drivers to be mounted without requiring root access or kernel modifications.
  
### Naming Server
The **Naming Server** handles administrative functions, such as:
- Registering new storage servers.
- Discovering storage servers hosting specific files.
- Handling client requests for operations like listing files in a directory.
  
The naming server uses an **Index Tree** to manage file indexing and metadata efficiently, reducing unnecessary connections to storage servers.

### Storage Server
The **Storage Server** is responsible for storing the actual files. Any number of storage servers can be added to the system, but files are replicated across only two servers to ensure fault tolerance. Each server stores and serves the files directly to clients after they receive file location information from the naming server.

## Communication Protocols

GoStore uses **gRPC** and **Protocol Buffers** for inter-service communication. These technologies allow high-performance, language-agnostic communication between the client, naming server, and storage servers.

- **gRPC**: A high-performance RPC framework that simplifies building distributed systems.
- **Protocol Buffers**: A platform-neutral, extensible way to serialize structured data, ensuring efficient communication across different services and languages.

## How to Run the System

To get started with GoStore locally, use Docker to set up the server infrastructure easily.

1. Clone the repository and navigate to the project directory.
2. Start the infrastructure using Docker Compose:

\`\`\`bash
docker-compose up
\`\`\`

3. Create a mount point for the file system:

\`\`\`bash
mkdir -p mnt_point
\`\`\`

4. Start the client to mount the file system:

\`\`\`bash
./Client
\`\`\`

5. After working with the file system, unmount it:

\`\`\`bash
sudo umount mnt_point
\`\`\`

For more detailed instructions and options, refer to the project’s [DockerHub repository](link_to_DockerHub_repo) and [GitHub project](link_to_GitHub_project).

## Contributions

We welcome contributions! Please visit our [Project Board](link_to_Project_Board) for a list of tasks and open issues.

## License

This project is licensed under the MIT License – see the LICENSE file for details.
