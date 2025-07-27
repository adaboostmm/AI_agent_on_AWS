##  Note: All materials are from Amazon Web Services workshops.

## Deploying an LLM to Amazon SageMaker AI real-time endpoint
To use SageMaker AI endpoints, first deploy a managed endpoint through SageMaker Jumpstart, a feature that helps 
machine learning practitioners quickly get started with hundreds of production-ready models in SageMaker AI.
   
`0-setup as how to deploy ENDPOINT`
-------------------------------------

`1-inference`
------------------
  - how to invoke an Amazon Bedrock model using AWS SDK for Python (`boto3`)
  - how to invoke an Amazon Bedrock model using LiteLLM
  - how to invoke a model hosted on Amazon SageMaker AI inference endpoints using AWS SDK for Python (`boto3`)
  - how to invoke a model hosted on Amazon SageMaker AI inference endpoints using the Amazon SageMaker Python SDK
  - how to invoke a model hosted on Amazon SageMaker AI inference endpoints using LiteLLM

## Tool Calling with Amazon Bedrock and Amazon SageMaker AI
The agent orchestrates these tools in sequence, creating workflows that seamlessly transition between different capabilities as needed. 
This approach allows systems to transcend the limitations of any single model or tool.

`2-tool-calling`
-------------------
- how to perform tool calling with an Amazon Bedrock model using AWS SDK for Python (`boto3`)
- how to perform tool calling with an Amazon Bedrock model using LiteLLM
- how to perform tool calling with a model hosted on Amazon SageMaker AI inference endpoints using AWS SDK for Python (`boto3`)
- how to invoke a model hosted on Amazon SageMaker AI inference endpoints using the Amazon SageMaker Python SDK
  
`3-agent-patterns`
------------------------
Autonomous agents are typically just LLMs using tools based on environmental feedback in a loop. 
Agents can be used for open-ended problems where it’s difficult or impossible to predict the required number of steps, 
and where you can’t hardcode a fixed path. 
The LLM will potentially operate for many turns, and you must have some level of trust in its decision-making. 
Agents' autonomy makes them ideal for scaling tasks in trusted environments.
Define the tools, once the tools are defined, we can define the autonomous agent loop. 
For that, we will be creating a class called AutonomousAgent.

<img width="573" height="294" alt="Screen Shot 2025-07-26 at 6 22 35 PM" src="https://github.com/user-attachments/assets/44350a88-2152-42d6-881d-224bd8eceaec" />

`4-frameworks`
---------------
## Using open-source frameworks

`Agno` is a lightweight library for building Agents with memory, knowledge, tools and reasoning.
Developers use `Agno` to 

- build Reasoning Agents, 
- Multimodal Agents, 
- Teams of Agents and Agentic Workflows.
  
`Agno` also provides a beautiful UI 
- to chat with your Agents, 
- pre-built FastAPI routes to serve your Agents and 
- tools to monitor and evaluate their performance.

`CrewAI Observability with Langfuse`

`Langfuse` is an open-source observability and analytics platform designed specifically for LLM applications. 
`Langfuse` helps you track, monitor, and analyze your LLM application's performance, costs, and behavior.

With `Langfuse`, you can:

- Track and analyze LLM interactions and their associated costs
- Monitor model performance and latency
- Debug production issues with detailed tracing
- Evaluate output quality and model behavior
- Collect user feedback and ground truth data and more.

`Building a hierarchical multi-agent travel assistant with CrewAI`

- create a travel assistant using multi-agent collaboration with the CrewAI framework.
- use this assistant to generate articles on the top activities and attractions for a specific location.

Structure of the travel assistant

travel assistant consisting of the following agents:

`Researcher Agent` - is responsible for gathering information on the top 5 attractions and activities in a specific location

`Content Writer Agent` - is responsible for writing an engaging article based on the information of the top 5 attractions

`Editor Agent` - is responsible for improving the flow and language use within the article

`5-observability`
---------------------
## Observability

Observability is a critical component when developing and deploying AI agents in production environments. 
As AI agents become more complex, involving multiple components, tools, and LLM calls, having visibility 
into their behavior becomes essential for debugging, optimization, and ensuring reliability.

## Why Observability Matters for AI Agents

- **Transparency**: Observability provides insights into how agents make decisions, which tools they use, and how they process information, making the "black box" of AI more transparent.
- **Debugging**: When agents produce unexpected outputs or fail, observability tools help pinpoint where and why issues occurred in the execution flow.
- **Performance Optimization**: By tracking metrics like latency, token usage, and tool call frequency, developers can identify bottlenecks and optimize agent performance.
- **Cost Management**: Monitoring token usage and API calls helps manage and optimize the costs associated with running AI agents at scale.
- **Continuous Improvement**: Collecting data on agent behavior enables iterative improvement of prompts, tools, and overall agent design based on real-world usage patterns.

In this section, we explore two approaches to implementing observability for AI agents:

1. **Langfuse**: An open-source observability platform specifically designed for LLM applications
2. **MLflow**: A versatile platform for managing ML workflows that can be used to track and trace agent executions

Both solutions provide valuable insights into agent behavior, helping you build more reliable, efficient, and cost-effective AI systems.

`99-use-cases`
---------------------
🧠 Building & Evaluating Complex Agents with crewai and flotorch-eval
A complete example of evaluating agents using the flotorch-eval package across key metrics. 
These metrics help assess both agent quality and system performance.

🔍 Evaluation Metrics

AgentGoalAccuracyMetric
- Evaluates whether the agent successfully understood and achieved the user's goal.
- Binary (1 = goal achieved, 0 = not achieved)

ToolCallAccuracyMetric
- Measures the correctness of tool usage by the agent—i.e., whether the agent called the right tools to complete a task.
- Binary (1 = relevant tools invoked, 0 = relevant tools not invoked)
  
TrajectoryEvalWithLLM
- Evaluates whether the trajectory (based on OpenTelemetry spans) is meaningful, either with or without a reference trajectory.
- Binary (1 = meaningful, 0 = invalid)
  
LatencyMetric
- Measures agent latency—how fast the agent responds or completes tasks.

UsageMetric
- Evaluates the cost-efficiency of the agent in terms of compute, tokens, or other usage dimensions.

🧠 Using SageMaker Endpoints as Tools for Agents

- how to integrate Amazon SageMaker endpoints as tools for AI agents,
- enabling them to leverage machine learning models for specialized tasks.

## Overview

1. Train and deploy a Machine Learning Model on Amazon SageMaker
2. Create a tool interface that allows AI agents to invoke the SageMaker endpoint
3. Use the SageMaker endpoint as a specialized tool within an agent workflow
4. Integrate the tool with an agent framework to enable AI agents to make predictions

## Key Components

- **Amazon SageMaker**: For training and hosting the machine learning model
- **Model Context Protocol (MCP)**: For creating a standardized tool interface
- **Strands Agents**: For building and orchestrating AI agents that use the SageMaker endpoint

## Files Included

- `demand_forecasting.ipynb`: Jupyter notebook for data preparation and model exploration
- `model-train-and-deploy.py`: Python script for training and deploying the XGBoost model
- `script.py`: SageMaker training and inference script for the XGBoost model
- `server.py`: MCP server implementation for the SageMaker endpoint tool
- `strands-agents-sagemaker-as-tool.ipynb`: Example of using the SageMaker endpoint with agents

  

