In module 0, we're going to set up a simple RAG application that we'll be using as we learn more about LangSmith. We set this up in the form of a notebook named Notebook1.

## *Visibility while building with Tracing*

Tracing can help you pinpoint issues and track how each part of your application contributes to the output.

**Lesson 1-: Tracing Basics**

If a trace is an end-to-end execution of your application, then each unit of work or logic within your trace is a Run. In a RAG application, we have two main runs-: 

- Retrieve Documents
- Generate  response

In order to set up tracing, we need to use the traceable decorator.

In this lesson, I learned the basics of tracing and how to use the @traceable decorator.

**Lesson 2-:Types of Runs**

We have several different types of runs in langsmith. Some of these are-:

1. LLM: Invokes an LLM.
2. Retriever: Retrieves documents from databases and other sources.
3. Tool: Executes actions with function calls.
4. Chain: Default type; combines multiple runs into a larger process.
5. Prompt: Hydrates a prompt to be used with an LLM.
6. Parser: Extracts structured data.

If we have a decorated tracable function with the run type of LLM and with the specific suitable input and output formats, then the langsmith would be able to render the input and outputs nicely. Each input should have a role and content specified.

When we had our run type as basic, the output still looked like a raw JSON file and when we changed it to llm, it gave a proper output with the help of ai.

Similarly, we tried the other types of runs within the  lesson.

**Lesson-:3 Alternate ways to Trace**

As of now, we have only used the @traceable decorator to perform tracing but now, we’ll explore other methods.

We used these 4 methods in total till now-:

1. @traceable
2. Langchain/Langgraph
3. with trace()
4. wrap_openai()  

**Lesson-:4 Conversational Threads**

This module taught how to group multi-turn LLM conversations into Threads in LangSmith, letting each chat stay context-aware across turns.
We used a thread_id (UUID) to link related traces and track conversation history.
Learned how to use traceable decorators to log retrieval, generation, and LLM calls.
Finally, ran a simple RAG pipeline twice within the same thread to see connected traces in LangSmith.

## ***Testing And Evaluation***

**Lesson 1:Datasets**

This module taught how to keep a chatbot’s memory across conversations using Threads in LangSmith.
Each chat turn is tracked with a unique thread_id, keeping related traces linked.
We used traceable functions to log retrieval, generation, and LLM activity.
Finally, we built a small RAG chatbot and saw its connected traces inside LangSmith.
