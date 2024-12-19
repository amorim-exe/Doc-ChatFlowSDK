
# API Documentation: ChatFlow SDK

**Version:** 1.0  
**Author:** Codeless LLC  
**Last Updated:** December 2024  

---

## Overview  
The ChatFlow SDK is a powerful tool that allows developers to integrate a fully functional chat system into their applications. Whether you're building mobile or web applications, this SDK facilitates real-time messaging and activity feeds. By using this SDK, developers can create dynamic, engaging chat systems that enhance user interaction. It supports a wide range of features, from sending messages to managing user participation in chat rooms. Furthermore, the SDK offers built-in tools for real-time updates, making it an ideal choice for modern communication platforms.

---

## Getting Started

### Prerequisites  
Before you start using the ChatFlow SDK, ensure that your development environment is prepared with the following:

- A working Node.js environment (for web applications) or the appropriate mobile SDKs (for mobile applications).
- A valid **API Key** from the ChatFlow platform, which you can obtain from your platform's dashboard.
- Access to the **ChatFlow management console** to configure permissions, set up rooms, and manage users.

### Installation

**For Web Applications:**  
To get started with web applications, install the ChatFlow SDK via npm:
```bash
npm install chatflow-sdk
```

**For Mobile Applications (React Native):**  
For React Native applications, use the following npm package:
```bash
npm install react-native-chatflow-sdk
```

### Authentication  
The SDK requires an API key for authentication to ensure secure access to the chat services. To authenticate, simply pass your API key when initializing the ChatFlow SDK.

```javascript
const chatFlow = new ChatFlowSDK({ apiKey: 'YOUR_API_KEY' });
```

---

## API Endpoints

### 1. Send a Message  
This endpoint allows you to send a text message from the current user to a specified chat room.

**Endpoint:**  
`POST /api/v1/messages/send`

**Request Parameters:**

- `roomId` (string): The ID of the chat room where the message will be sent.
- `message` (string): The text content of the message.
- `userId` (string): The ID of the user sending the message.

**Example Request:**
```javascript
chatFlow.messages.send({
  roomId: '12345',
  message: 'Hello, world!',
  userId: 'user_001'
});
```

**Response:**
```json
{
  "status": "success",
  "message": "Message sent successfully.",
  "messageId": "msg_001"
}
```

### 2. Get Chat History  
This endpoint retrieves the message history for a specific chat room.

**Endpoint:**  
`GET /api/v1/messages/history`

**Request Parameters:**

- `roomId` (string): The ID of the chat room to retrieve the history for.
- `limit` (integer, optional): The maximum number of messages to retrieve (default: 50).
- `before` (string, optional): A timestamp to filter messages sent before a specific time.

**Example Request:**
```javascript
chatFlow.messages.history({
  roomId: '12345',
  limit: 20
});
```

**Response:**
```json
{
  "status": "success",
  "messages": [
    {
      "messageId": "msg_001",
      "userId": "user_001",
      "timestamp": "2024-12-19T12:34:56Z",
      "content": "Hello, world!"
    },
    {
      "messageId": "msg_002",
      "userId": "user_002",
      "timestamp": "2024-12-19T12:35:00Z",
      "content": "Hi there!"
    }
  ]
}
```

---

### Real-Time Chat with WebSockets  
The ChatFlow SDK supports real-time communication using WebSockets, providing seamless updates when new messages or events occur in the chat system.

#### Establishing a WebSocket Connection
To start receiving real-time updates, establish a WebSocket connection by passing the API key and chat room ID.

```javascript
const socket = chatFlow.socket.connect({
  apiKey: 'YOUR_API_KEY',
  roomId: '12345'
});

socket.on('message', (message) => {
  console.log('New message:', message);
});

socket.on('user_typing', (user) => {
  console.log(user + ' is typing...');
});
```

---

## User Management

### 1. Add a User to a Chat Room  
This endpoint allows you to add a user to a chat room, enabling them to participate in the conversation.

**Endpoint:**  
`POST /api/v1/rooms/add_user`

**Request Parameters:**

- `roomId` (string): The ID of the chat room where the user will be added.
- `userId` (string): The ID of the user being added.

**Example Request:**
```javascript
chatFlow.rooms.addUser({
  roomId: '12345',
  userId: 'user_003'
});
```

**Response:**
```json
{
  "status": "success",
  "message": "User added successfully."
}
```

---

## Features

- **Real-Time Notifications:** Receive notifications for new messages, user activity, and room changes.
- **Activity Feed:** Track user activity, including joining, leaving, and message events in real-time.
- **Message Reactions:** Allow users to add reactions (like thumbs up, heart, etc.) to messages.

---

## Troubleshooting

### 1. Invalid API Key  
If you receive a `401 Unauthorized` error, check that your API key is valid and has the necessary permissions. You can regenerate the key from your ChatFlow account dashboard if needed.

### 2. WebSocket Connection Issues  
If you are unable to establish a WebSocket connection, ensure that your WebSocket server is up and running. Verify that the room ID and API key are correct. If problems persist, consider using fallback mechanisms to handle connection issues.

---

## Conclusion  
The ChatFlow SDK provides an easy-to-use, feature-rich platform for integrating chat and real-time activity feeds into your applications. Whether you're building a small messaging feature or a full-fledged chat system, this SDK is flexible and scalable to meet your needs.  

For more detailed examples, additional features, and troubleshooting tips, please refer to our official documentation or contact our support team.
