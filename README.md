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
