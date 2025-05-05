# Frontdesk Engineering Test:
Human-in-the-Loop AI Supervisor

A human-in-the-loop system for AI agents that allows them to escalate questions to human supervisors when they don't have sufficient knowledge to answer that also learns from it.

### Goal
Build the first version of a human-in-the-loop system for our AI agents. If the AI doesn’t know the answer, it should escalate to a human supervisor, follow up with the original customer, and update its knowledge base automatically.

### Technologies Used

- **Backend**:
  - Node.js with Express.js
  - MongoDB with vector search capabilities
  - OpenAI API for embeddings and LLM
- **Agent Server**:
  - LiveKit SDK for voice agent capabilities
  - OpenAI for text generation and processing
- **Dashboard Frontend**:
  - React with TypeScript
  - TailwindCSS for styling
  - TanStack Query for data fetching
- **Voice Assistant Frontend**:
  - Using LiveKit's example repository: https://github.com/livekit-examples/voice-assistant-frontend

## Getting Started

### Prerequisites

- Node.js
- MongoDB Atlas account with vector search enabled
- OpenAI API key
- LiveKit account and API credentials
- Deepgram API key (used by LiveKit for speech-to-text)

## System Components

### AI Agent

The agent uses LiveKit for voice interaction and is powered by OpenAI's models. It has three main tools:

- `bookAppointment`: For scheduling appointments
- `searchKnowledge`: To search the knowledge base for answers
- `requestHumanHelp`: To escalate questions to supervisors

### Knowledge Base

The knowledge base uses MongoDB with vector search to enable semantic matching:

- Questions are stored with their corresponding answers and tags
- Embeddings are generated for efficient semantic search
- Status tracking (answered/unanswered) for query lifecycle management

### Supervisor Interface

A React-based dashboard with:

- Tab-based navigation between answered and unanswered questions
- Real-time updates using polling
- Simple interface for providing answers to escalated questions

## Design Decisions

### Knowledge Base Structure

- Used MongoDB with vector search for semantic matching
- Created composite embeddings combining questions, answers, and tags
- Implemented tagging for additional filtering and categorization

### Human Request Flow

- Simple lifecycle: Unanswered → Answered
- Polling mechanism for real-time updates (5-second intervals)
- Timeout handling (30 seconds) for supervisor availability

### Scalability Considerations

- MongoDB Atlas for database scaling
- Indexed queries for efficient retrieval
- Vector search for semantic matching scales to larger knowledge bases

## Future Improvements

- Implement WebSocket for real-time updates instead of polling
- Add authentication for supervisors
- Support for live call transfers to human supervisors
