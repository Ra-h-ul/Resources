# LangChain 

LangChain is a framework designed to assist in the development of applications that involve large language models (LLMs) such as GPT, with a focus on simplifying the process of interacting with these models and integrating them into various applications. It enables the creation of applications capable of reasoning, memory retention, data retrieval, and other complex tasks by chaining together LLMs and external tools like APIs, databases, or search engines.

## Alternatives to LangChain

- **LlamaIndex (formerly GPT Index):** A framework that helps organize and query large-scale data using LLMs, similar to LangChain but more focused on indexing and retrieval.
- **Haystack:** A more focused framework for building NLP pipelines, supporting both LLM-based and traditional NLP tasks, and integration with various search engines.
- **GPT-3/4 APIs:** Direct API calls to OpenAI's GPT models can be used for simpler LLM interactions, without additional chaining or memory management layers.

## Advantages of LangChain

- **Ease of Use:** LangChain abstracts away much of the complexity of working with LLMs, making it easier to integrate and build applications.
- **Modularity:** The framework allows developers to chain various tools, allowing for complex workflows involving multiple models, external APIs, and databases.
- **Flexibility:** It provides the ability to integrate custom tools and LLMs for unique use cases.
- **Memory Management:** LangChain offers memory management features that enable the model to retain context across multiple interactions with a user, which is useful for building conversational agents.
- **Integration:** LangChain seamlessly integrates with a variety of APIs, databases, and search engines, allowing it to support real-time information retrieval, database lookups, and much more.

## Disadvantages of LangChain

- **Complexity:** While it abstracts many tasks, the flexibility and modularity of LangChain can sometimes lead to complexity, requiring deeper understanding of the architecture.
- **Dependency on LLMs:** It is built around large language models, so it may not be suitable for projects that do not require or involve LLMs.
- **Learning Curve:** Due to its flexible nature and variety of features, new users may face a learning curve in understanding how to properly chain components and manage workflows.

## Before LangChain

Before frameworks like LangChain, building applications that leverage LLMs required more manual setup for each use case. Developers had to integrate APIs, handle memory and state management, and manually code the logic for chaining together different components (e.g., retrieving data from a database, interacting with an API, or handling multiple user interactions). The use of models was often more isolated and required custom code for specific needs.


---
## Main Components of LangChain


##    1. **Core Engine / LLM**  
The language model (such as GPT-3/4 or others) that performs the natural language processing tasks.

 ## 2. **Chain**
A chain in LangChain refers to a series of sequential or interconnected steps that process inputs and outputs. Chains are designed to handle tasks by combining various tools, models, or APIs into a workflow.

**Examples of Chains:**
1. **LLM Chain:** Combines a language model with a prompt template to generate outputs.
2. **Sequential Chain:** Executes multiple chains in order, passing the output of one as the input to the next.
3. **Retrieval-Augmented Generation (RAG) Chain:** Retrieves relevant documents and generates responses based on them.

**Use Case:**
- Fetching context using a retriever and then using a language model to generate a response based on the retrieved data.


## 3.  **Agents**
Agents are dynamic decision-makers in LangChain that decide which tool, chain, or model to use at runtime based on the current task and context. They are particularly useful for complex, multi-step tasks.

### **Key Features:**
- Use tools like APIs, search engines, or calculators.
- Dynamically respond to user inputs and adapt workflows.
- Require prompts that specify the tools available and the problem to solve.

### **Agent Types:**
1. **Zero-Shot Agents:** Execute tasks without specific training for the task.
2. **Multi-Tool Agents:** Select and use multiple tools during execution.
3. **Conversational Agents:** Retain context across multiple exchanges for chatbot-like interactions.



## **Chain vs Agent**

| **Aspect**         | **Chain**                                       | **Agent**                                      |
|---------------------|-------------------------------------------------|-----------------------------------------------|
| **Behavior**        | Executes a predefined, linear sequence of tasks. | Dynamically decides which tool or chain to use. |
| **Flexibility**     | Fixed workflow.                                | Adaptive to input and runtime context.         |
| **Complexity**      | Simpler and predictable.                       | Handles more complex and dynamic tasks.        |
| **Use Case**        | Well-defined processes like document retrieval. | Open-ended tasks like querying APIs or tools.  |

## 4.   **Memory**
Retains the history of interactions or knowledge over time, which helps in creating more contextual and personalized responses.

Types of Memory

- **Conversation Memory / Conversation buffer :** Stores user interaction history (e.g., chat logs) and makes it accessible for context retrieval. This type is particularly useful in building chatbots or conversational agents.

      Conversation Buffer window : ConversationBufferWindowMemory keeps a list of the interactions of the conversation over time. It only uses the last K interactions. This can be useful for keeping a sliding window of the most recent interactions, so the buffer does not get too large.

- **Document Memory:** For storing and retrieving documents or knowledge pieces relevant to the ongoing task. This type is useful in systems that combine information retrieval with language generation.

- **Contextual Memory:** Keeps track of context-specific details, like user preferences or specific instructions, which are useful when building more personalized or context-aware applications.

- **Entities:**
Entities in LangChain refer to specific pieces of information (like names, dates, or locations) extracted from or managed within the context of a conversation or document. LangChain can recognize, track, and use these entities dynamically for various tasks.

     ### **Key Features of Entities in LangChain**

    1. **Entity Recognition**:
        - Extract named entities from text using NLP models.
        - Entities include persons, organizations, dates, products, etc.

    2. **Entity Tracking**:
        - Maintain a record of entities across interactions, ensuring context continuity in conversations or workflows.

    3. **Entity Storage**:
        - Save entities in memory for reuse, helping systems personalize responses or track important details.


## 5. **Tools**
 External resources (such as APIs, databases, or other systems) that the language model can use during processing.

## Tool Calling in LangChain

- **Tool calling** in LangChain enables agents to dynamically call predefined tools during execution. This is essential for workflows where an agent must rely on external utilities (like APIs, search engines, or custom functions) to perform specific tasks. The agent determines which tool to use based on the user query and the tool descriptions provided.


## **Key Components**

1. **Tool**: A utility or function the agent can use.
   - Defined with a name, description, and function.
2. **Agent**: Responsible for deciding which tool to invoke and when.
3. **Execution Flow**: The agent interprets user input, selects a tool, and uses it to generate a response.

---
# Callbacks in LangChain

In LangChain, **callbacks** are used to monitor and react to events during the execution of a chain, agent, or workflow. Callbacks provide a way to add custom behavior, logging, or tracking at various points in the execution process, such as before or after a specific step or after receiving the final output.

## Key Features of Callbacks in LangChain

- **Event Handling**: Callbacks can be triggered during various stages of the execution, like before an agent decides, after a tool is called, or when the final output is generated.
- **Customization**: You can define your own callback functions to capture logs, track progress, or interact with external systems (e.g., monitoring or analytics services).
- **Integration with Chains and Agents**: Callbacks can be applied to chains and agents to add functionality like logging, metrics collection, and dynamic behavior modification.

## Types of Callbacks

- **Before and After Execution**: Callbacks can be set to run before or after an action is executed, such as before a chain executes or after a tool completes.
- **Custom Callback Handlers**: Custom callback functions can be used to define specific behaviors that you need for your application, such as writing logs or sending notifications.

___
# Workflows in LangChain

In LangChain, **workflows** refer to a sequence of tasks or operations that are executed to solve a specific problem or achieve a goal. Workflows typically consist of multiple steps, which may include retrieving data, processing it, interacting with APIs, and generating responses using language models (LLMs). LangChain provides a framework to design and manage these workflows, making it easy to integrate different components such as agents, tools, memory, and LLMs.




---
# **Multimodality** :   
 Multimodality refers to the ability to work with data that comes in different forms, such as text, audio, images, and video. Multimodality can appear in various components, allowing models and systems to handle and process a mix of these data types seamlessly.

---
# Implementing and Managing Agent Tools in LangChain

LangChain's agent framework enables the implementation and management of tools that an agent can dynamically invoke to perform tasks. Here's a step-by-step guide:

## **1. Define Tools**
Tools in LangChain are utilities or APIs integrated for specific tasks, such as database queries, API calls, or custom Python functions. Each tool must have:
- **A name**: Unique identifier.
- **A description**: Explains its purpose.
- **A function**: Contains the logic or action performed.


    python
    
        from langchain.tools import Tool

        def search_tool(query: str) -> str:
            return f"Results for {query}"

        tool = Tool(
            name="SearchTool",
            func=search_tool,
            description="Search the web for relevant information"
        )

2. Create an Agent : LangChain provides several agent classes (e.g., ZeroShotAgent, ConversationalAgent). Tools are specified during the agent's initialization.


        from langchain.agents import initialize_agent, AgentType
        from langchain.chat_models import ChatOpenAI

        llm = ChatOpenAI(temperature=0)  # LLM for decision-making
        agent = initialize_agent(
            tools=[tool],
            llm=llm,
            agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION,
            verbose=True
        )

3. Execution : Pass user input to the agent, and it dynamically decides when and how to use the tools.

        response = agent.run("Find information on LangChain")
        print(response)

4. Add More Tools : Multiple tools can be added, enabling the agent to choose the appropriate tool for the task.

---

## **Prompt**
A prompt in LangChain is the text input given to an LLM to guide its response. Prompts are essential for specifying the task or behavior you want the model to follow.

### **Types of Prompts:**
1. **Basic Prompt:** A simple question or command.
   - Example: "Write a summary of this article."
2. **Template Prompt:** A reusable template with placeholders for dynamic inputs.
   - Example: `"Summarize the following text: {text}"`
3. **Few-Shot Prompt:** Includes examples in the prompt to guide the model.
   - Example:
     ```
     Q: What is the capital of France?
     A: Paris
     Q: What is the capital of Japan?
     A: Tokyo
     ```

### **Prompt Engineering:**
- Crafting effective prompts to achieve desired outputs.
- Using system messages, instructions, or examples to set expectations.



---

## Role Embeddings in LangChain

Role embeddings are a way to incorporate the roles or personas of different entities in an interaction. In LangChain, this could refer to how different agents or tools are treated within a system. For example:

- **User Role:** The human interacting with the system.
- **Assistant Role:** The LLM or agent that generates responses.
- **Tool Role:** External systems that the model interacts with (e.g., database, API).

Role embeddings help in structuring the conversation or interaction flow by clarifying the responsibilities of each entity involved. This enables more effective use of LLMs and external tools in generating contextually appropriate responses based on the roles of the entities.


___
# LangChain Expression Language (LCEL)

**LangChain Expression Language (LCEL)** is a powerful declarative framework designed for expressing logic, workflows, and operations within LangChain. It allows developers to create dynamic and flexible workflows, enabling better control over the behavior of agents and chains.



## **Features of LCEL**
1. **Declarative Syntax**: Simplifies the definition of complex workflows.
2. **Dynamic Evaluation**: Supports on-the-fly computation and decision-making.
3. **Integration with LangChain Components**: Seamlessly works with tools, memory, and agents.



## **Core Concepts**

1. **Expressions**: 
   - LCEL uses expressions to represent logic or calculations.
   - These can include variables, functions, and operations.

2. **Variables**:
   - Variables hold context or intermediate results.
   - Accessible and modifiable during execution.

3. **Conditionals**:
   - Enables branching logic for workflows.
   - Example: `if`, `else`, and `switch`.

4. **Loops**:
   - Supports iteration over lists or repeated tasks.

---


# How LangChain Works with LLMs, Transformers, and RAG

LangChain is designed to work with Large Language Models (LLMs), Transformers, and Retrieval-Augmented Generation (RAG) models. Here's how it integrates these components and their roles in building AI applications:

## 1. Working with LLMs (Large Language Models)

LangChain integrates LLMs like GPT-3, GPT-4, or any other transformer-based model to handle natural language processing tasks, such as text generation, summarization, and question answering.

- **LLMs in LangChain:**
    - LangChain acts as a wrapper around these LLMs, providing an interface to call them easily within larger workflows. For example, the LLMChain component allows you to chain together multiple LLM calls and use them in a structured flow.
    - **Prompting:** LangChain helps in managing the prompts and responses between different LLMs, allowing you to pass data from one step to another seamlessly.

## 2. Transformers

Transformers are deep learning models that power most LLMs. In LangChain, transformers are used for various NLP tasks and can be directly accessed through frameworks like Hugging Face's Transformers library.

- **Using Transformers with LangChain:**
    - LangChain allows easy access to transformer models for tasks like text summarization, text classification, and tokenization. It leverages the capabilities of transformers for efficient natural language processing and text generation.
    - **Tokenization:** LangChain helps in processing text data into tokens, which transformers understand to perform tasks like language generation.

## 3. RAG (Retrieval-Augmented Generation)

RAG is an approach that combines information retrieval with text generation. In this setup, relevant information is first retrieved from an external knowledge base (e.g., documents, databases), and then a language model is used to generate more accurate and informed responses based on that information.

- **RAG in LangChain:**
    - **Retrieval Integration:** LangChain integrates with various retrieval systems (e.g., FAISS, Elasticsearch) to fetch relevant documents from external databases or knowledge sources.
    - **Generation:** Once the relevant documents are retrieved, they are passed to a language model for generation. LangChain helps in chaining this process, where first the model retrieves data, then generates answers based on it.
    - **Dynamic Queries:** LangChain enables dynamic and real-time querying, where the language model adjusts its responses based on the most recent information fetched during the conversation or task.

---

# How LangChain is Used in Building AI Applications

LangChain simplifies the development of AI applications by providing a structured way to use LLMs in combination with other external systems, data sources, and memory management. Here's how it can be used:

- **Conversational AI (Chatbots):**
    - LangChain enables the development of advanced chatbots that can carry on multi-turn conversations by retaining context over time.
    - **Memory:** The framework provides robust memory management systems, allowing bots to remember user interactions, making them more personalized.
    - **Contextual Responses:** It allows for combining user input with context (e.g., previous conversation history or data from external APIs) to generate informed responses.

- **Document Search and Summarization:**
    - RAG and external retrieval systems in LangChain allow you to build applications that retrieve information from documents or databases and then generate concise summaries or answers to user queries.
    - **Document Retrieval:** LangChain can query large data sources and return relevant documents or text, which are then processed by the LLM to generate responses.

- **Task Automation:**
    - LangChain can be used to build workflows that automate tasks, such as generating reports, processing emails, or interacting with APIs to fetch real-time data, using chains of different LLMs and tools.

- **Personalized Applications:**
    - By using memory management, LangChain helps build personalized AI applications that adapt over time based on user behavior, preferences, and interaction history.

---


# API Integration in LangChain

LangChain allows easy integration with external APIs to enhance the functionality of applications. Here’s how API integration is done in LangChain:

### External Tool Integration:
- LangChain can integrate with any external API to fetch real-time data, perform computations, or use third-party services. This is done using Tool components, which allow you to define custom API calls that interact with the language model.
- For example, you can build a custom API tool that fetches weather data or financial information, and pass this data as context to the LLM for more accurate responses.

### Custom API Integration:
- You can define a Tool for each API endpoint and chain these tools with the LLM. The tools can be triggered based on the context of the conversation or user input.
- For instance, if a user asks a question about the weather, LangChain can route the query to a weather API (via a Tool), fetch the response, and then send that information to the LLM to generate a final response.

### Agent Integration:
- LangChain also provides an agent-based architecture that allows you to build intelligent workflows that interact with APIs and take autonomous actions. Agents can decide which API or tool to use based on the incoming input or current context.

### Real-Time API Calls:
- The AgentExecutor in LangChain executes API calls and LLM queries in real-time. It makes decisions based on predefined rules or learned behavior, automatically querying APIs when necessary to enhance the AI application's responses.

---

# LangChain vs LangChain4j

LangChain and LangChain4j are both frameworks that enable easy integration of Large Language Models (LLMs) with other systems and tools for building sophisticated AI applications. While they serve the same fundamental purpose of facilitating the creation of LLM-powered applications, they are tailored to different programming languages.

## LangChain

- **Overview**: LangChain is a Python-based framework that simplifies the integration of LLMs and other tools in AI applications. It provides a rich set of functionalities for working with LLMs, document retrieval (via RAG), memory management, and API integrations.
- **Primary Use**: LangChain is widely used in the Python ecosystem for building chatbots, document search engines, personalized assistants, and other LLM-driven applications.
- **Key Features**:
  - **Integration with LLMs**: Supports popular LLMs like GPT-3, GPT-4, T5, and more.
  - **Memory Management**: Offers built-in support for retaining conversation history and context across interactions.
  - **Tool Integration**: Allows integration with external APIs, databases, and services to enhance AI capabilities.
  - **RAG (Retrieval-Augmented Generation)**: Combines document retrieval with language model generation for more accurate responses.
  - **Chaining**: Facilitates chaining different models and tools into complex workflows.
- **Technologies**: LangChain is built on top of Python, leveraging the powerful ecosystem of Python libraries for NLP, machine learning, and web development.

## LangChain4j

- **Overview**: LangChain4j is a Java-based framework that brings the functionality of LangChain to the Java ecosystem. It allows developers to use LLMs with tools like memory management, RAG, and API integration in Java applications.
- **Primary Use**: LangChain4j is intended for developers working in Java who want to integrate LLMs and create AI applications without needing to switch to Python.
- **Key Features**:
  - **Java Integration**: LangChain4j makes it easy to build AI applications in Java while taking advantage of the same high-level features available in LangChain.
  - **LLM Support**: Works with various LLMs by integrating with services like OpenAI or other model providers.
  - **Memory Management**: Supports memory management for conversational AI, enabling persistent contexts and responses across interactions.
  - **Tool Integration**: Provides a way to integrate external APIs, databases, and services with Java-based AI applications.
  - **RAG**: Supports Retrieval-Augmented Generation, allowing for more precise and contextual responses.
  - **Java-Specific Libraries**: LangChain4j utilizes Java libraries and frameworks, offering a familiar environment for Java developers.
- **Technologies**: LangChain4j is built for Java, using Java's ecosystem for tool integration, NLP, and web-based APIs.

---

## LangChain vs LangChain4j - Key Differences

| Feature                        | LangChain (Python)                                  | LangChain4j (Java)                              |
|---------------------------------|-----------------------------------------------------|-------------------------------------------------|
| **Programming Language**        | Python                                              | Java                                            |
| **Primary Ecosystem**           | Python-based ecosystem for AI and NLP tools         | Java-based ecosystem for AI and NLP tools       |
| **LLM Integration**             | Supports LLMs like GPT-3, GPT-4, T5, BART, etc.     | Integrates with OpenAI and other LLM providers  |
| **Memory Management**           | Built-in memory for retaining context               | Supports memory management for conversational AI|
| **RAG Integration**             | Native support for RAG (document retrieval + generation) | Supports RAG-like workflows in Java-based applications|
| **API Integration**             | Easy integration with APIs via Python libraries     | Supports integration with APIs and tools using Java|
| **Community**                   | Larger community in the Python ecosystem            | Smaller, growing community in the Java ecosystem|
| **Flexibility**                 | Highly flexible due to Python's ecosystem           | More constrained by Java’s capabilities but still powerful|

---

## When to Use LangChain vs LangChain4j

### Use LangChain (Python):
- When you’re working in a Python-based environment.
- If you need access to the large number of AI, machine learning, and NLP libraries available in Python.
- When building AI applications like chatbots, document search engines, and complex LLM-based workflows with full flexibility.

### Use LangChain4j (Java):
- When your project is based on Java and you need to integrate LLMs without moving to Python.
- If you're developing enterprise-level applications that require the robustness and scalability of Java.
- When working in environments where Java is the preferred language or existing systems are already built in Java.

---

# LangChain4j Alternatives

LangChain4j is designed for Java developers to work with Large Language Models (LLMs) and other AI tools, but there are several alternatives in the Java ecosystem for integrating LLMs and building AI-powered applications. Here are some alternatives:

### 1. Deep Java Library (DJL)
- **Overview**: DJL is an open-source Java library for deep learning, supporting several frameworks like TensorFlow, PyTorch, and MXNet. It simplifies the integration of machine learning models, including LLMs, into Java applications.
- **Use Case**: Primarily used for integrating machine learning models in Java applications, including deep learning models, but doesn't focus solely on LLMs like LangChain4j.

### 2. OpenNLP
- **Overview**: Apache OpenNLP is a machine learning-based toolkit for natural language processing tasks such as tokenization, sentence splitting, and named entity recognition.
- **Use Case**: While OpenNLP doesn't focus on LLMs specifically, it's a solid alternative for Java developers needing NLP tools for tasks like text classification, tokenization, or language parsing.

### 3. AllenNLP (with Java wrapper)
- **Overview**: AllenNLP is a Python-based library built on top of PyTorch, designed for NLP. However, some developers have created Java wrappers for AllenNLP to leverage the power of this framework in Java applications.
- **Use Case**: Although it's not natively built for Java, using a Java wrapper around AllenNLP allows Java developers to use advanced NLP models.

### 4. TensorFlow Java
- **Overview**: TensorFlow, originally created by Google, offers a Java API that allows Java developers to integrate pre-trained models (including LLMs) into their applications.
- **Use Case**: For Java developers working with TensorFlow models, this API provides the flexibility to load and use models trained in Python and other languages.

---

# Advantages and Disadvantages of LangChain4j

### Advantages:

- **Java Ecosystem Integration**: LangChain4j is designed specifically for Java, making it ideal for Java developers who are already familiar with the Java ecosystem and libraries.
- **LLM Integration**: Supports integration with large language models like OpenAI's GPT, which allows developers to build complex NLP applications in Java.
- **Memory Management**: LangChain4j offers memory management features for context retention in conversational AI, which is crucial for creating persistent, intelligent chatbots.
- **API Integration**: It provides easy integration with external APIs, enabling the creation of multi-tool AI systems where the language model can interact with other services (databases, external APIs, etc.).
- **RAG Support**: Supports Retrieval-Augmented Generation (RAG), allowing it to fetch documents or context before generating responses, improving the accuracy and relevance of the generated content.

### Disadvantages:

- **Smaller Community**: Compared to LangChain (Python), LangChain4j has a smaller community and fewer resources available, making it harder to find support or documentation.
- **Java-Centric**: It may be less flexible than Python-based solutions since Python has a broader ecosystem of libraries for AI, machine learning, and NLP. Some integrations or cutting-edge tools may not be available or as optimized in LangChain4j.
- **Limited Libraries**: While Java has good support for ML and NLP, it is not as extensive or easy-to-use as the libraries available in Python for AI and LLMs.
- **Steeper Learning Curve**: Java is less dynamically evolving in the LLM space compared to Python. LangChain4j might require more setup and configuration than a Python-based equivalent.


# Before LangChain4j

Before LangChain4j, Java developers would typically rely on more traditional Java libraries for natural language processing (like OpenNLP, Stanford NLP, or others) and machine learning frameworks like TensorFlow Java or Deeplearning4j. These libraries provided basic NLP and ML capabilities but lacked the cohesive, end-to-end workflow that LangChain4j offers for integrating LLMs with memory management, document retrieval, and external API services.

# Architecture of LangChain4j

LangChain4j’s architecture follows the general pattern of LangChain but is designed for the Java ecosystem. It consists of several core components that enable efficient use of LLMs, memory management, and integration with external services.

## Key Components:

### 1. Retrievers:
These components fetch relevant documents or data from external sources. In LangChain4j, retrievers can be connected to databases, APIs, or custom sources for document retrieval in a Retrieval-Augmented Generation (RAG) setup.

### 2. Language Models (LLMs):
LangChain4j integrates with powerful LLMs like GPT, enabling them to process user queries and generate natural language responses. These models can be connected via API calls or local instances.

### 3. Memory Management:
Memory is a key component of LangChain4j. It retains user interaction context across multiple exchanges, which is essential for building chatbots or conversational systems that need persistent context.

### 4. Chains:
Chains in LangChain4j allow the combination of different models or tools to form workflows. This can include retrieving documents, processing them, and then generating responses based on the user query and retrieved context.

### 5. APIs and External Tools Integration:
LangChain4j provides integration with external APIs, allowing the system to pull in data from services like databases, document stores, or other web-based APIs.

# Memory Management and Types in LangChain4j

Memory management is crucial in creating personalized or contextually aware applications, such as conversational AI. LangChain4j provides memory management tools that retain context throughout interactions. It allows the system to remember past queries and responses, ensuring that conversations appear more natural and fluid.

## Memory Types:

### 1. Conversation Memory:
This type stores context related to user interactions. It enables the system to remember the details of a conversation across multiple exchanges, improving the quality of interactions.

### 2. Session Memory:
This type of memory persists context only for the duration of a session. Once the session ends, the memory is cleared.

### 3. Persistent Memory:
Persistent memory stores context beyond a single session. This allows the system to remember long-term user preferences, history, and other relevant details over time.

### 4. External Memory:
External memory integrates with external data stores, such as databases or knowledge bases, to provide additional context or knowledge.

# Role Embeddings in LangChain4j

Role embeddings allow the system to incorporate different perspectives, contexts, or user roles into the conversation. This can be used to influence how the system responds based on the role of the user or the specific context of the conversation.

## 1. User Role Embedding:
Distinguishes between different user types or personas in a conversation. This helps tailor responses to specific user needs.

## 2. Bot Role Embedding:
Used for the chatbot's behavior or personality, which might change based on the situation or interaction type (informational, directive, etc.).

## 3. System Role Embedding:
Allows the system to maintain a specific role, such as an assistant, expert, or task-oriented agent, guiding the way it processes and responds to queries.
