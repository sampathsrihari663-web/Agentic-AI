# AI Chatbot using LangGraph, Groq, and Streamlit

## Project Overview

This project demonstrates how to build a simple AI chatbot using LangGraph, Groq, and Streamlit.

The chatbot accepts user input through a Streamlit interface, processes the request using a LangGraph workflow, sends the message to a Groq-hosted Large Language Model (LLM), and returns the generated response to the user.

This project helps beginners understand how LangGraph workflows, states, nodes, edges, and AI models work together to create intelligent applications.

---

# What is LangGraph?

LangGraph is a framework built on top of LangChain that helps developers build stateful AI applications.

It allows developers to create workflows using nodes and edges, where each node performs a specific task and edges define the path that execution follows.

LangGraph is commonly used for:

- AI Agents
- Chatbots
- Workflow Automation
- Multi-Agent Systems
- Applications with Memory

---

# What is a Graph?

A graph is a collection of nodes connected by edges.

It defines how information flows through an application.

Example:

User Input

↓

Chatbot Node

↓

Output

---

# What is a Node?

A node is a function that performs a specific task within a workflow.

In this project, the chatbot node receives the user's message, sends it to the language model, and returns the generated response.

---

# What is an Edge?

An edge connects nodes together.

It determines how execution moves from one node to another.

In this project:

```python
graph.add_edge("chatbot", END)
```

This means the workflow ends after the chatbot node finishes execution.

---

# What is State?

State is the information shared between nodes.

In this project, the state stores the user's message and the generated response.

Example:

```python
class state(TypedDict):
    message: str
```

---

# What is Groq?

Groq is a platform that provides extremely fast inference for Large Language Models.

It allows developers to access models such as:

- Llama 3
- Gemma
- Mixtral
- DeepSeek

In this project, Groq is used to generate responses for user questions.

---

# What is Streamlit?

Streamlit is a Python framework used to build web applications quickly.

It allows developers to create user interfaces directly using Python without writing HTML, CSS, or JavaScript.

---

# Workflow Used in this Project

User Message

↓

State Creation

↓

Chatbot Node

↓

Groq LLM

↓

Response Generation

↓

END

↓

Display Response

---

# Source Code

```python
import streamlit as st # Import Streamlit library
from typing import TypedDict # from typing import TypedDict,Typeddict is used to define a type that represents a dictionary with specific keys and value types.
from langgraph.graph import StateGraph,END # Import StateGraph and END from langgraph.graph

#state graph is a data structure that represents the states and transitions of a system.
#It is used to model the behavior of a system and to analyze its properties.

from langchain_groq import ChatGroq # Import ChatGroq from langchain_groq

#ChatGroq is a class which has details of what api key is and which model it is using.
#It is used to interact with the GROQ API and to generate responses based on the specified model.

llm = ChatGroq(
    groq_api_key="Your Groq API Key", # Specify your GROQ API key
    model="llama-3.1-8b-instant", # Specify the model to use
)

# State Graph
class state(TypedDict):
   message:str # Define a key 'message' of type string

# chatbot node
def chatbot(state):
    replay = llm.invoke(state["message"]) # Call the invoke method of llm with the message from the state
    return {"message": replay.content}

graph = StateGraph(state) # Create a StateGraph with the defined state type

graph.add_node("chatbot", chatbot) # Add a node to the graph with the name "chatbot" and the function chatbot

graph.set_entry_point("chatbot") # Set the entry point of the graph to "chatbot"

graph.add_edge("chatbot", END) # Add an edge from the "chatbot" node to the END state

app = graph.compile() # Compile the graph to create an application

# Streamlit UI
st.title("Chatbot Application") # Set the title of the Streamlit app.

user_input = st.text_input("you:->") # Create a text input field for the user to enter their message.

if st.button("send"):
    result = app.invoke({
        "message": user_input
    }) # Invoke the app with the user's message and store the result.

    st.success(result["message"])
```

---

# Technologies Used

- Python
- LangGraph
- LangChain
- Groq API
- Streamlit
- Llama 3.1 8B Instant

---

# Installation

```bash
pip install langgraph
pip install langchain-groq
pip install streamlit
```

---

# Run the Project

```bash
streamlit run app.py
```

---

# Learning Outcomes

Through this project, I learned:

- How LangGraph workflows operate
- How states are passed between nodes
- How nodes and edges are connected
- How to integrate Groq with LangGraph
- How to build AI chatbots
- How to create web applications using Streamlit

---

# Future Improvements

- Add conversation memory
- Add multiple nodes
- Add tool calling
- Add web search capabilities
- Add chat history
- Add multi-agent workflows
