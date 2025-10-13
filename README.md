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

This lesson taught how to keep a chatbot’s memory across conversations using Threads in LangSmith.
Each chat turn is tracked with a unique thread_id, keeping related traces linked.
We used traceable functions to log retrieval, generation, and LLM activity.
Finally, we built a small RAG chatbot and saw its connected traces inside LangSmith.

**Lesson 2:Evaluators**

This lesson taught how to use Evaluators in LangSmith to measure the quality of LLM outputs.
We learned to compare model predictions with expected answers using built-in evaluators.
It also showed how to create custom evaluators for specific tasks.
Finally, we saw how to log results and analyze model performance automatically.

**Lesson 3:Experiments**

This lesson taught how to create and manage Experiments in LangSmith to compare different LLM runs.
We learned how to run multiple model versions or prompts and log their results automatically.
It showed how to analyze metrics and see which setup performs best.
Finally, we understood how experiments help in iterating and improving model quality systematically.


_______________________________________________________________________________________________________________________________________

# ***MODULE - 3***

## ***Playground***

In this video, we talk about the playground environment in LangSmith which is used  for prompt engineering. When we think about prompts, we think about the hard-coded strings that tell the LLM exactly what to do. The playground is specifically made for quickly iterating prompts and prompt templates.

On opening the lesson, we can see that we have the prompting section and a brief list of messages.
Let’s start with a simple question→ “What is the meaning of Life?”.
On clicking Start button( or cmd+Enter) we see that our LLM has a pretty decent answer of its own.
On the left side we can add messages to fully mimic a conversation with a human.

Now, let’s go ahead and use the output to the last question as the new message and ask a follow-up question→ “Where can I learn about philosophy?”
The responses generated further would now answer the questions in a conversational format.

We also see that when we change our system message prompt to “You are a pirate from the 1600s.”, it makes that chatbot behave like a pirate in its responses. Hence, we can see that changing the system prompt dramatically changes the output.

Note that we can switch models from the right side of the message heading and we can also change different model based attributes like temperature, presence penalty and frequency penalty.

Also note that we can see the response metrics pop-up there like the response time, latency and token usage and then further make observations like *the response time of Claude-3.5o Sonnet is lesser than that of GPT - 4o- mini*.

In the prompts tab on the top, we can click on the *+Compare* button to compare different models at once in a much easier way.

So far, we’ve seen our response come back in a streaming format but we can also run them in a non- streaming way by just turning off streaming from the run options. Now that we’ve turned streaming off, we can also run the code with repetitions in order to get multiple responses at once.

Let’s go ahead and add an output schema. An output schema will compare the output from the model with the schema that you’ve defined.

In addition to the output schema, we have tool calling which would help us know how it would respond if it had access to a certain number of tools.

Now, we’ll see how we can run an example on an interface over an entire dataset of examples.

After the video, here’s how I did a little experimenting of my own from my own dataset on the playground interface-:

<img width="864" height="474" alt="image" src="https://github.com/user-attachments/assets/1f99c9f6-71c7-4f99-812a-d697b0e72658" />

## ***Prompt Hub***

It is a solution for iterating, storing and versioning on your prompts over time.
Langsmith’s prompt_hub is a great way of storing your prompt templates. In this, you can store a list of messages which includes system message and typically also human message that’s passed to the chatbot. We can use the prompt templates quickly via the playground and we can also use them in our own code using sdk.
This is what the prompt hub looks like -:
<img width="850" height="344" alt="image" src="https://github.com/user-attachments/assets/f1b41946-cd96-48bb-8c4d-a785f0d04296" />
By default, we create the chat-style-prompt but we can also create the instruction style prompts.
Now, let’s go ahead and create our chat-style prompts→ This takes us to the playground interface.
We’ll change the system prompt to that of a bot who is a character from the Peaky Blinders.

We’ll add the output schema as follows-:
<img width="855" height="494" alt="image" src="https://github.com/user-attachments/assets/45ab9754-dd95-4a16-a730-059bdaf8fe90" />

Now, we’ll go ahead and save this prompt by clicking on the save button on the right side of the messages label.
<img width="779" height="281" alt="image" src="https://github.com/user-attachments/assets/be2bc654-4afc-418e-a63d-3e9a4b308df4" />
We can either make the prompt private or public. If it is private, it means only the users in our workspace can see it and if it is public it means that everyone can see it. Let’s keep ours private for now.

When we save this prompt, it takes us back to the prompt_hub. Let’s see what information we have about our prompt.
<img width="851" height="475" alt="image" src="https://github.com/user-attachments/assets/de5d2550-7703-4b1d-9404-57b076706ebd" />
We also have our chatmodel configurations in it. We can see the provider and model that we are using. Moreover, all of our hyperparameters are stored here.

One of the coolest parts about prompt_hub is that wer can actually use this prompt and save it in our codebase.
Let’s go ahead and copy this code snippet here-:
<img width="850" height="157" alt="image" src="https://github.com/user-attachments/assets/245b9538-a408-4727-ad22-184d734f80d1" />
Now, let’s navigate over to our prompt_hub notebook in module 3.
On invoking the prompt and asking the questions, we get our output as follows-:
<img width="872" height="82" alt="image" src="https://github.com/user-attachments/assets/5881c6d9-6e09-4cf1-92ca-ec35c1af99d0" />
And this later on when we change our prompt using runnable binding→

<img width="866" height="63" alt="image" src="https://github.com/user-attachments/assets/81db1b66-45c3-48fb-bb69-060c09968870" />
We can also commit changes and navigate to all the versions of our prompt.

Now, we’ll see how to push the prompts programmatically to the prompt_hub using the sdk.
Here, we define a simple RAG prompt-:

<img width="854" height="257" alt="image" src="https://github.com/user-attachments/assets/9d6ec9a2-6988-4b8d-8d98-b2ead1a2c153" />
