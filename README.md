# cppChatterbox 🗨️

*cppChatterbox* is a terminal-based chat application developed in C++ using **Boost.Asio** for asynchronous networking. It supports multiple clients chatting with each other through a central server. The project showcases core concepts like async I/O, multithreading, message encoding, and session management.

---

## ✨ Key Features

- 🔄 **Asynchronous I/O**: Non-blocking communication with `boost::asio::async_read` and `async_write`.
- 🧵 **Threading**: Each client session runs on a dedicated thread for smooth multitasking.
- 💬 **Room Chat**: Clients connect to a room where messages are broadcast to all.
- 🧱 **Modular Design**: Logical separation between networking, message handling, and session control.

---

## 🧠 Architecture Overview

### 🔧 Components

- **Session**: Manages individual client communication (read/write).
- **ChatRoom**: Holds active clients and forwards messages.
- **ChatMessage**: Encodes and decodes messages (header + body).

### 🧩 Class Diagram (UML)

```mermaid
classDiagram
    class IParticipant {
        <<interface>>
        +deliver(ChatMessage& message)*
    }

    class ChatSession {
        -socket
        -buffer
        -ChatRoom& room
        +start()
        +deliver(ChatMessage& message)
        +read_async()
        +write_async()
    }

    class ChatRoom {
        -participants
        -messageHistory
        +join(IParticipant participant)
        +leave(IParticipant participant)
        +broadcast(ChatMessage& message)
    }

    class ChatMessage {
        -char data[]
        -size_t bodyLength
        +encode()
        +decode()
        +getBody()
        +setBody()
    }

    IParticipant <|-- ChatSession
    ChatSession *-- ChatRoom
    ChatSession *-- ChatMessage
    ChatRoom o-- ChatMessage
    ChatRoom o-- IParticipant

---

## 📌 Prerequisites

### 🪟 For Windows Users – Install Ubuntu via WSL

> Run this in PowerShell (as Admin):

```powershell
wsl --install -d Ubuntu
```

📌 **Reboot** your PC after this command finishes. Then, open "Ubuntu" from Start Menu to continue.

---

## 🔧 Setup & Run (All Commands Below)

### 📁 1. Clone the repository

```bash
git clone https://github.com/ajaysoni12/cppChatterbox.git
cd cppChatterbox
```

> 🪟 PowerShell equivalent (in Ubuntu terminal on WSL):
```powershell
git clone https://github.com/ajaysoni12/cppChatterbox.git
cd cppChatterbox
```

---

### 📦 2. Install required dependencies

```bash
sudo apt update
sudo apt install -y libboost-all-dev g++ make
```

---

### 🏗️ 3. Build the project

```bash
make
```

To clean build:
```bash
make clean
make
```

---

## 🚀 Run the Chat App

> Use any available port (9099 is generally safe)

### 🖥️ Start the Server

```bash
./chatApp 9099
```

### 💬 Start a Client (in another terminal)

```bash
./clientApp 9099
```

Run as many clients as you like in separate terminals.

---

## 🗂️ Project Structure

```
cppChatterbox/
├── chatApp         # Server binary
├── clientApp       # Client binary
├── Makefile
├── *.cpp, *.hpp    # Source files
├── README.md       # You're here!
```

---

## 💡 Notes

- Make sure `./chatApp` and `./clientApp` are executable (`chmod +x` if needed)
- You must run server first before connecting clients
- Each client runs in its own thread and receives broadcasted messages

---

## 📄 Example Run

Terminal 1 (Server):

```bash
./chatApp 9099
```

Terminal 2 (Client 1):

```bash
./clientApp 9099
```

Terminal 3 (Client 2):

```bash
./clientApp 9099
```

Start chatting between clients — all messages are broadcast by server.

---

## 🙌 Credits

Learn this project from Lovepreet Bhai & Inspired by Boost.Asio examples and designed for educational networking demos.

---

### 🔚 Done!

Copy, paste, run — you're good to go. Happy hacking! 💬✨
