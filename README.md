# LangGraph + Groq AI Chatbot

## Project Overview

This project is a conversational AI chatbot built with **Python**, **LangGraph**, **Groq**, and **Streamlit**. A user sends a message through the Streamlit interface. The backend passes that message through a LangGraph workflow to a language model hosted by Groq, then displays the model's reply.

The project demonstrates how to connect a language model to a simple chat interface and organize the chatbot's processing using a graph-based workflow.

## Objectives

- Build a simple AI chatbot that responds to user questions.
- Connect a language model through the Groq API.
- Use LangGraph to define and execute the chatbot workflow.
- Create a browser-based interface with Streamlit.
- Practice integrating Python libraries and an external AI API.

## Technologies Used

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| LangGraph | Defines the chatbot's state and processing flow |
| LangChain Groq | Connects the application to a Groq-hosted language model |
| Groq API | Provides access to the language model |
| Streamlit | Creates the web-based chat interface |

## Theory and Working

### 1. Large Language Model (LLM)

A Large Language Model is an AI model trained on large amounts of text. It processes a prompt and generates a response based on patterns learned during training. In this project, the LLM receives the user's message and generates the chatbot's answer.

### 2. Groq

Groq provides an API for running supported language models. The chatbot sends the user's prompt to the selected model through the Groq service. The service returns the generated response to the application.

### 3. LangChain Groq

`ChatGroq` is the LangChain integration used to communicate with Groq. It lets the Python application configure a model and invoke it with a message.

### 4. LangGraph

LangGraph is a framework for building applications as workflows made of nodes and edges.

- **State:** Holds information used during a workflow, such as the conversation messages.
- **Node:** A function that performs a step. In this chatbot, the model node sends the messages to the LLM and returns its response.
- **Edge:** Defines which step runs next.
- **START and END:** Represent the beginning and completion of the workflow.

For a basic chatbot, the graph can be simple: the workflow starts, runs the chatbot node, and then ends.

### 5. Streamlit

Streamlit provides the user interface in a web browser. It displays the chat history, accepts the user's message, sends it to the backend, and shows the returned response.

## System Workflow

1. The user enters a message in the Streamlit chat interface.
2. The frontend sends the message to the chatbot backend.
3. LangGraph starts the workflow and passes the conversation state to the chatbot node.
4. The node invokes the configured Groq language model.
5. Groq returns the generated answer.
6. The backend returns the answer to Streamlit.
7. Streamlit displays the response to the user.

```text
User
  |
  v
Streamlit Chat Interface
  |
  v
LangGraph Workflow
  |
  v
Chatbot Node
  |
  v
Groq API / Language Model
  |
  v
Generated Response
  |
  v
Streamlit displays the answer
```

## Project Structure

```text
chatbot_ui/
├── langgraph_backend.py     # LangGraph workflow and model connection
├── streamlit_frontend.py    # Streamlit chat interface
└── README.md                # Project documentation
```

The exact filenames and responsibilities may differ if your project uses a different structure.

## Setup and Execution

### 1. Create a virtual environment

Run these commands in PowerShell from your project folder:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

### 2. Install dependencies

```powershell
python -m pip install -U langchain langchain-core langchain-groq langgraph python-dotenv streamlit
```

### 3. Configure the Groq API key

Create a key at <https://console.groq.com/keys>, then configure it in the backend's `ChatGroq` setup. If you choose to place the key directly in the source code, replace the placeholder below with your own key:

```python
llm = ChatGroq(
    model="openai/gpt-oss-20b",
    api_key="YOUR_GROQ_API_KEY",
    temperature=0
)
```

Do not upload a real API key to GitHub or share it publicly. If a key has been exposed, revoke it and create a new one. If the selected model is unavailable, use a model currently supported by your Groq account.

### 4. Start the chatbot

With the virtual environment activated, run:

```powershell
python -m streamlit run streamlit_frontend.py
```

Open the local URL printed in the terminal.

## Advantages

- Simple interface that is easy to use.
- Uses a hosted language model rather than requiring the model to run locally.
- Separates the frontend from the chatbot workflow.
- LangGraph provides a structure that can be extended with additional nodes and conditional paths.

## Limitations

- Responses depend on the selected model and the availability of the Groq service.
- The chatbot may generate incorrect or incomplete information.
- The application requires an internet connection and a valid API key.
- Conversation history is retained only as implemented by the application; this project description does not assume persistent storage.

## Future Enhancements

- Add conversation memory or persistent chat history.
- Add document question-answering using uploaded files.
- Add tools such as weather or web search.
- Add user-friendly error handling and loading indicators.
- Deploy the Streamlit application for public access with the API key stored securely.

## Conclusion

This project demonstrates a basic AI chatbot using a Groq-hosted language model, LangGraph for workflow orchestration, and Streamlit for the user interface. It provides a foundation for learning how LLM-powered applications are connected and how a simple chatbot can be expanded into a more capable AI assistant.
