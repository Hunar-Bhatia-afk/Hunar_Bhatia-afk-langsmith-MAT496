In module 0, we're going to set up a simple RAG application that we'll be using as we learn more about LangSmith. We set this up in the form of a notebook named Notebook1.

## *Visibility while building with Tracing*

Tracing can help you pinpoint issues and track how each part of your application contributes to the output.

**Lesson 1-: Tracing Basics**

If a trace is an end-to-end execution of your application, then each unit of work or logic within your trace is a Run. In a RAG application, we have two main runs-: 

- Retrieve Documents
- Generate  response

In order to set up tracing, we need to use the traceable decorator.

In this lesson, I learned the basics of tracing and how to use the @traceable decorator.
