# Agentic-AI
# AI PC Builder Agent using CrewAI and Gemini

## Project Overview

This project demonstrates how to build an AI-powered PC recommendation system using the CrewAI framework and Google's Gemini language model.

The AI agent acts as a PC Building Expert and helps users select the best computer components based on their budget and requirements. The agent analyzes the user's needs, researches suitable hardware, and generates a detailed PC build recommendation.

This project is a beginner-friendly example of how AI agents can be used to automate decision-making tasks and provide personalized recommendations.

---

# What is CrewAI?

CrewAI is a Python framework used to create AI agents that can perform tasks and solve problems.

Instead of interacting directly with a language model, CrewAI allows developers to create agents with specific roles, goals, and responsibilities.

These agents can work individually or collaborate with other agents to complete complex tasks.

### Example

An AI agent can be assigned roles such as:

- PC Building Expert
- Financial Advisor
- Travel Planner
- Research Assistant

Each agent is given a goal and uses an AI model to achieve that goal.

---

# What is Automation?

Automation is the process of using software to perform tasks automatically with little or no human intervention.

Instead of manually researching PC components, the AI agent performs the analysis and provides recommendations automatically.

### Benefits of Automation

- Saves time
- Reduces repetitive work
- Improves efficiency
- Provides faster results
- Helps users make informed decisions

---

# What is a Workflow?

A workflow is a sequence of steps that are followed to complete a task.

In AI systems, workflows help organize how agents perform tasks and generate results.

### Example Workflow in this Project

1. User provides a budget and requirements.
2. The AI agent analyzes the requirements.
3. The agent researches suitable PC components.
4. The agent compares available options.
5. The agent generates a detailed recommendation.
6. The result is displayed to the user.

---

# Creating an AI Agent

In this project, an AI agent is created using CrewAI.

The agent is assigned:

### Role

The role defines the profession or responsibility of the agent.

Example:

```python
role="PC Building Expert"
```

### Goal

The goal tells the agent what it must achieve.

Example:

```python
goal="Research and recommend the best components for a gaming PC build."
```

### Backstory

The backstory provides additional context and expertise to the agent.

Example:

```python
backstory="You are a PC building expert with extensive knowledge of computer hardware."
```

---

# Components Used in This Project

## Agent

An Agent is an AI assistant with a specific role and objective.

The PC Building Expert agent is responsible for recommending the best PC components based on the user's budget and requirements.

---

## Task

A Task represents a job assigned to an agent.

In this project, the task is to research and recommend PC components within a given budget.

---

## Crew

A Crew is a collection of agents and tasks working together.

It manages the execution of tasks and coordinates the workflow.

---

## Process

The Process determines how tasks are executed.

This project uses:

```python
Process.sequential
```

This means tasks are executed one after another in order.

---

## LLM (Large Language Model)

An LLM is the AI model that powers the agent's reasoning and responses.

This project uses:

```python
gemini/gemini-2.5-flash
```

Google Gemini helps the agent analyze requirements and generate recommendations.

---

# Project Workflow

The overall execution flow is:

User Input
↓
Agent Creation
↓
Task Assignment
↓
Crew Creation
↓
AI Processing
↓
PC Recommendation Output

---

# Source Code

The complete implementation can be found in:

```text
app.py
```

---

# Technologies Used

- Python
- CrewAI
- Google Gemini
- Large Language Models (LLMs)

---

# Learning Outcomes

Through this project, I learned:

- How AI agents work
- How to create agents using CrewAI
- How to assign tasks to agents
- How workflows are managed in AI systems
- How to integrate Google Gemini with Python applications
- How automation can be implemented using AI

---

# Future Improvements

Possible enhancements include:

- Multiple specialized agents
- Real-time hardware price checking
- Web search integration
- Comparison of multiple PC builds
- Graphical User Interface (GUI)
- Budget optimization features

---

Creating an AI Agent

This project demonstrates how to create an AI agent using CrewAI and Google’s Gemini model. The agent acts as a PC Building Expert and recommends gaming PC components based on a given budget and requirements
```python
from crewai import Agent, Task, Crew, Process, LLM # importing classes from crewai library to create an agent, define a task, and use a language model for processing the task.
import os

# Google Gemini API key
os.environ["GOOGLE_API_KEY"] = "AIzaSyDPLzINMwxOiaNlVXsYi9jv0RHZOqHvf30"

llm = LLM(
    model="gemini/gemini-2.5-flash",# define which model we are going to use for this automation task.
    temperature=0.3# if the value is higher the responeses will be more creative and longer !
)

#User input
PC_build = "Buliding a Gaming PC With a budget of 2000 dollars in which i want to play games like Cyberpunk 2077, Call of Duty, and Fortnite at high settings. I also want to do some video editing and streaming on Twitch. Can you recommend the best components for my gaming PC build within this budget?"
budget = 2000


#Agent Creation
pc_agent = Agent(
    role="PC Building Expert",
    goal="Research and recommend the best components for a gaming PC build within a budget of 2000 dollars while ensuring excellent gaming, streaming and video editing performance.",
    backstory="You are a PC building expert with extensive knowledge of computer hardware and gaming requirements. Your task is to help users build a gaming PC that meets their needs and budget.",
    verbose=True, # to generate detailed reasoning steps.
    llm=llm # to use the Google Gemini LLM or to define the tools that the agent can use for research and analysis.
)

# Assinging the task to the agent
task = Task( # calling task class to create a task for the agent.
    description="Research and recommend the best components for a gaming PC build within a budget of 2000 dollars.",
    # A detailed description of the task that outlines the specific requirements and constraints.
    expected_output="""
    A detailed gaming PC build recommendation including:
    - CPU
    - GPU
    - RAM
    - Storage
    - Motherboard
    - Power Supply
    - Case
    - Estimated prices
    - Total cost
    - Reasoning for each recommendation
    """,# A clear outline of what the expected output should include, such as specific components, estimated prices, total cost, and reasoning for each recommendation.
    agent=pc_agent # storing the agent that contains the specifications and goals for the task.
)

# Crew pipeline
'''the crew pipeline is a framework that allows you to organize and manage multiple agents and tasks.
It provides a structured way to coordinate the efforts of different agents working on various tasks,
ensuring that they can collaborate effectively to achieve the overall objectives.
In this case, we are creating a crew that includes our PC building agent and the task we have defined for it.'''

crew = Crew(
    agents=[pc_agent], # adding the agent to the crew
    tasks=[task], # adding the task to the crew
    process=Process.sequential, # it goes through the tasks in a sequential manner,
    #meaning that it will complete one task before moving on to the next.
    verbose=True # gives us better responses,detailed reasoning steps,
    #and insights into the agent's decision-making process.
)

# Run the crew pipeline
print("Starting the PC building process...")

result = crew.kickoff()

print("==" * 30)
print("PC building process completed. Here are the recommended components💁🏻:")
print("==" * 30)
print(result)
```
Key Concepts Used

* Agent – An AI assistant with a specific role and goal.
* Task – A job assigned to an agent.
* Crew – A collection of agents and tasks working together.
* Process – Defines how tasks are executed (Sequential or Hierarchical).
* LLM (Large Language Model) – The AI model used by the agent, such as Gemini.
