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

Conversational Threads
Many LLM applications have a chatbot-like interface in which the user and the LLM application engage in a multi-turn conversation. In order to track these conversations, you can use the Threads feature in LangSmith.

This is relevant to our RAG application, which should maintain context from prior conversations with users.

Setup
# You can set them inline
import os
os.environ["OPENAI_API_KEY"] = ""
os.environ["LANGSMITH_API_KEY"] = ""
os.environ["LANGSMITH_TRACING"] = "true"
os.environ["LANGSMITH_PROJECT"] = "langsmith-academy"  # If you don't set this, traces will go to the Default project
# Or you can use a .env file
from dotenv import load_dotenv
load_dotenv(dotenv_path="../../.env", override=True)
Group traces into threads
A Thread is a sequence of traces representing a single conversation. Each response is represented as its own trace, but these traces are linked together by being part of the same thread.

To associate traces together, you need to pass in a special metadata key where the value is the unique identifier for that thread.

The key value is the unique identifier for that conversation. The key name should be one of:

session_id
thread_id
conversation_id.
The value should be a UUID.

import uuid
thread_id = uuid.uuid4()
from langsmith import traceable
from openai import OpenAI
from typing import List
import nest_asyncio
from utils import get_vector_db_retriever

openai_client = OpenAI()
nest_asyncio.apply()
retriever = get_vector_db_retriever()

@traceable(run_type="chain")
def retrieve_documents(question: str):
    return retriever.invoke(question)

@traceable(run_type="chain")
def generate_response(question: str, documents):
    formatted_docs = "\n\n".join(doc.page_content for doc in documents)
    rag_system_prompt = """You are an assistant for question-answering tasks. 
    Use the following pieces of retrieved context to answer the latest question in the conversation. 
    If you don't know the answer, just say that you don't know. 
    Use three sentences maximum and keep the answer concise.
    """
    messages = [
        {
            "role": "system",
            "content": rag_system_prompt
        },
        {
            "role": "user",
            "content": f"Context: {formatted_docs} \n\n Question: {question}"
        }
    ]
    return call_openai(messages)

@traceable(run_type="llm")
def call_openai(
    messages: List[dict], model: str = "gpt-4o-mini", temperature: float = 0.0
) -> str:
    return openai_client.chat.completions.create(
        model=model,
        messages=messages,
        temperature=temperature,
    )

This module taught how to group multi-turn LLM conversations into Threads in LangSmith, letting each chat stay context-aware across turns.
We used a thread_id (UUID) to link related traces and track conversation history.
Learned how to use traceable decorators to log retrieval, generation, and LLM calls.
Finally, ran a simple RAG pipeline twice within the same thread to see connected traces in LangSmith.
