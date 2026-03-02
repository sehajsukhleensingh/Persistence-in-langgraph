# LangGraph Persistence – Stateful Chatbot & Workflow

This project demonstrates how to implement **persistence in LangGraph** to build stateful AI workflows and chatbots.

Without persistence, every `invoke()` call creates a fresh execution state.  
When the graph reaches `END`, the state is discarded — causing chatbots to forget previous messages.

This notebook solves that problem using LangGraph checkpointers.

---

##  Problem

When invoking a LangGraph workflow inside a loop:

- Each execution starts with a new state
- Previous messages are not retained
- Chatbots forget user context
- Execution history is lost

This happens because the graph reaches `END`, terminating the execution cycle.

---

## Solution

Persistence is enabled using:

```python
from langgraph.checkpoint.memory import InMemorySaver, MemorySaver
```

### Key Features Implemented:

- ✔ Stateful workflow execution
- ✔ Checkpoint saving & retrieval
- ✔ Full state history access
- ✔ Time travel to previous checkpoints
- ✔ State mutation and replay
- ✔ Thread-based memory isolation
- ✔ Chatbot with short-term memory

---

## Implementations

### Joke Workflow (Stateful Pipeline)

Graph:
```
START → gen_joke → explain_joke → END
```

Demonstrates:
- State tracking
- Checkpoint history
- Resuming from intermediate steps
- Updating past state and re-running

---

### Chatbot with Memory

Graph:
```
START → chat_llm_node → END
```

With `MemorySaver`:
- Messages persist across turns
- Each `thread_id` maintains isolated conversation memory
- Chatbot remembers user information

---

## Thread-Based Configuration

```python
config = {
    "configurable": {
        "thread_id": "1"
    }
}
```

Each thread maintains its own state, enabling multi-user support.

---

## Concepts Covered

- LangGraph state lifecycle
- Why `END` clears execution context
- Checkpoint-based persistence
- Time travel debugging
- Stateful conversational design
- Short-term memory implementation

### Persistence
    For assistance in Langgraph refers to the ability to save and restored the state of a workflow over time.
    Persistence not only stores last state , but also all the interim states of a workflow too.
    
    Due to persistence are able to implement concepts like 
    
    - fault tolerance in langGraph
    - resume old chats
    - HITL
    - short term memory in bots
    - time travel 
    - debugging 

---

## Tech Stack

- Python
- LangGraph
- LangChain
- Google Gemini
- dotenv

---

## Learning Outcome

This notebook demonstrates understanding of:

- Stateful AI workflow design
- Execution checkpointing
- Conversation memory systems
- Graph-based LLM orchestration

---

Built as part of deep exploration into conversational AI persistence and workflow engineering.
