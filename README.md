# Generative AI on Amazon SageMaker and Amazon Bedrock
##  Note: All materials are from Amazon Web Services workshops.

https://aws.amazon.com/blogs/opensource/introducing-strands-agents-an-open-source-ai-agents-sdk/

This repository provides comprehensive resources for working with generative AI models using Amazon SageMaker and Amazon Bedrock. 
--fine-tune foundation models, 
--build RAG applications, create agents, or 
--implement responsible AI practices

#### [Building RAG Workflows with SageMaker and Bedrock](./workshops/building-rag-workflows-with-sagemaker-and-bedrock/)
- Build experimental RAG applications
- Implement RAG with SageMaker and OpenSearch
- Fine-tune embedding models
- Customize models with RAFT
- Apply guardrails to LLM outputs

#### [Distributed Training and Deployment on SageMaker AI](./workshops/distributed-training-deployment-on-sagemaker-ai/)
- Use SageMaker JumpStart for fine-tuning
- Implement distributed training with FSDP and QLoRA
- Deploy models on SageMaker HyperPod with Kubernetes

#### [DIY Agents with SageMaker and Bedrock](./workshops/diy-agents-with-sagemaker-and-bedrock/)
- Basic inference with Bedrock and SageMaker
- Implement tool calling capabilities
- Build agent patterns (autonomous, orchestrator-worker, etc.)
- Use agent frameworks (LangGraph, CrewAI, Strands, etc.)
- Add observability with Langfuse and MLflow

#### [Fine-tuning with SageMaker AI and Bedrock](./workshops/fine-tuning-with-sagemakerai-and-bedrock/)
- Set up a Foundation Model Playground
- Customize foundation models
- Evaluate models with LightEval
- Implement responsible AI with Bedrock Guardrails
- Develop FMOps fine-tuning workflows with SageMaker Pipelines

# AI agent on Amazon Web Services
Harness the power of LLM and create autonomous AI agents on AWS.
An AI agent is a software programme that interacts with its environment to collect data and use the data to perform tasks to meet predetermined goals.

## Two main ways to consume Foundation Models:

### 1. managed, with Amazon SageMaker AI
1. A fully managed development environment to build, train and deploy ML model quickly.
2. A vetted hub of Foundation Models(FMs)
3. A robust infrastructure for deploying FMs
4. A high-performance automation platform
### 2. serverless, with Amazon Bedrock
1. A fully managed service for easy access to various FMs through a single API
2. Customization: An environment to fine-tune models with domain specific data
3. Built-in security features for Data Protection
4. Seamless integration with AWS services
5. Pay as you use
### and another way: Host own model and serving stack in Amazon EC2.

## IAM permnission for building agentic workflows
1. AmazonSageMakerFullAccess
2. AWSLambdaFullAccess
3. AmazonS3FullAccess
4. AmazonBedrockFullAccess
## Core components from LLM to Autonomous Agent
1. Foundation Models: Enable natural language understanding, reasoning and decision-making capabilities
2. Tool Integration: Utilize various tools, APIs and data sources. Function calling allows agents to interact with the world by letting LLM decide which tools to leverage and then iterate on top of iot.
3. Memory Systems: Maintain contexts across multiple interactions
   a. Short-term memory: temporary context, current prompts, responses
   b. Long-term memory: persistent information(facts and preferences), implemented using vector dbs or graphs, knowledge retention over extended periods
   c. Episodic memory: agent's experimental record to track what, when and why.
   learns from past experience, improves performance overvtime through accumulated experience.
   d. Semantic memory: factual knowledge and concepts in a structured formal, supports accurate reasoning processes by providing a foundation of organized information that agents can draw upon for decision-making.
## Agentic Workflows
### 1. Prompt Chaining:
<img width="2401" height="1000" alt="image" src="https://github.com/user-attachments/assets/15e3c80e-76f7-49f3-9b47-d2df6a9b2233" />

        a. decomposes a task into a sequence of steps, each LLM call processes the output of the previous one.
        b. gopal is to trade off latency for higher accuracy, by making each LLM call an easier task.
        c. example: generating a marketing copy, translating it into different languages, writing outline of a document based on list of criteria
### 2. Parallelization:   
<img width="2401" height="1000" alt="image" src="https://github.com/user-attachments/assets/f6200a6f-0d26-4988-a971-8742ec695be0" />

        a. Sectioning: break a task into independent subtasks and LLMs can work simultaneously  and have the outputs aggregated programmatically
        example: one model processes user queries and another LLM screens them for inappropriate content or requests; automating evals where each LLM call evaluates a different aspect of the model's performance on a given prompt.
        b. Voting: run same task multiple times by different LLMs to get diverse outputs.
        example: 
          (i) reviewing code for vulnerabilities: several different prompts review and flag the code 
          (ii) evaluating the appropriateness of a content: multiple prompts evaluating different aspects or differentr vote thresholds to balance false positives and negatives.
### 3. Routing:
<img width="2401" height="1000" alt="image" src="https://github.com/user-attachments/assets/14108a96-a27b-43ff-9614-7c4e27d758a7" />

        a. classifies an input and directs it to a specialized followup task.
        b. allows separation of concerns to build more specialized prompts
        c. without this, optimization for one kind of imput can hurt performance on other inputs.
        example: 
          (i) direct different types of customer service queries(general questions, refund requests, technical support) into different downstream processes, prompts, and tools
          (ii) route easy/common questions to smaller models and hard/unusal questions to more capable models to optimize cost and speed.
### 4. Supervisror (Orchestrator-Workers):
<img width="2401" height="1000" alt="image" src="https://github.com/user-attachments/assets/1e67fbb6-4f0d-4aa7-99fd-60599c92388d" />

        a. a central LLM dynamically breaks down tasks, delegates them to worker LLMs, and synthesizes their results.
        b. a key difference from parallelization is its flexibility-subtasks aren't predefined, orchestrator determines it based on the specific input.
        example:
          (i) coding products that make complex changes to multiple files each time
          (ii) search tasks involving gathering and analyzing information from multiple sources for possible relevant information.
### 5. Self-Reflection (Evaluator-Optimizer):
<img width="2401" height="1000" alt="image" src="https://github.com/user-attachments/assets/7612f150-a5ab-4081-b23b-34fc7c55c754" />

        a. one LLM call generates a response 
        b. another LLM provides evaluation and feedback in a loop
        c. analogous to the iterative writing when a human writer might go through when producing a polished document.
        example:
          (i) particularly effective when clear evaluation criteria exists and iterative refinement provides measurable value.
          (ii) LLM responses can be demonstrably improved when a human articulates their feedback and LLM can provide such feedback.
## Multi-Agent Collaboration
          a. leverage a hierarchy of specialized agents, each equipped with a focused set of tools
          b. an agent orchestrator selects the most appropriate agent for a given task
          c. The modular strategy offers a sophisticated problem-solving; it can also impose constraints on the interaction between agents, reducing the inherent non-deterministic nature of language models and leading to more reliable outcomes.
