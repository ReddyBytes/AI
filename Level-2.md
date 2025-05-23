
### **Level 2 – Prompt Engineering, RAGs & Tuning(The Art of Robot Whispering )**

> **Our Goal:** Now that we know the basics of LLM models and they work, let's learn how to talk to the robots like a pro to get exactly what we want, and even give them new books to read!
> 

You're no longer just randomly talking to robots. You're becoming a "Robot Whisperer," someone who knows the secret language to get them to do amazing, specific things.

🔹 **What We'll Discover:**

1. ### **Prompt Frameworks (Super Instruction Manuals):**   
    These are special ways to structure your prompts to get better results.
    *   **ReAct (Reasoning + Acting):** 
        - The model thinks first **("Reason")** and then takes an action **("Act")**
        - You tell the robot to: 
            1. Think about the problem. 
            2. Decide an action. 
            3. Take the action (e.g., search for info). 
            4. Observe the result. 
            5. Repeat until solved. It's like teaching it to plan!
            >**Example:**  
            Question: What’s the weather in Hyderabad today?  
            Thought: I need to get the current date, then call the weather tool.  
            Action: Call weather API for Hyderabad on [current date].  
            Observation: It’s 21°C and sunny.  
            Answer: It's sunny and 21°C in Hyderabad today.

    *   **Memory:** 
        - For longer tasks, you need to help the robot remember what happened earlier.
        - Include past facts/chat in your new prompt so the AI “remembers.”
        - Some tools (like ChatGPT with memory turned on) automatically store facts.
    *   **CoT (Chain of Thought):**   
        - Ask the model to “think step-by-step”.  
        - Helps with math, logic, and multi-part questions.
    *   **Output Control:** 
        -    Sometimes you don't want a long paragraph. You want the robot to give you information in a super organized way, like filling out a form. JSON is a way to structure data that computers love.  

        *   *Example:* "Robot, tell me about a lion. Give me its name, habitat, and diet in JSON format."
        The robot might reply:
        `{ "name": "Lion", "habitat": "African Savanna", "diet": "Carnivore" }`

    
`IMP :` To learn more prompting techniques and examples please take a look [**at this chapter**](/Prompt-Engineering.md) as well
        
---
2. ### **Retrieval-Augmented Generation (RAG's) (Giving the Robot a New Book):**  
     - Imagine your talking robot knows a lot about the world from all the internet books it read. But it *doesn't* know about *your* secret clubhouse rules or the notes from *your* dairy.

    *   With RAG, you can give the robot *your* specific documents (like your personal/external notes). When you ask a question, the robot first *retrieves* (finds) the relevant information from *your* notes and *then* uses that to *generate* an answer. So, its answers are "grounded" in your information.  

    *RAG** is an architecture that combines:
    1. **Retrieval**: Pulling in relevant documents or data from an external knowledge source (e.g., a vector database, search engine, or document store).
    2. **Generation**: Using a language model (LLM) to synthesize a coherent and contextually relevant response based on the retrieved documents.

    This technique helps overcome the limitations of static knowledge embedded in LLMs, especially for:
    - Dynamic or time-sensitive information
    - Specialized or private domains (e.g., enterprise data)
    - Long documents and context limitations

    ### 🔧 How RAG Works – Step-by-Step

    1. **Query Input**  
    The user asks a question or gives a prompt.

    2. **Retrieval Phase**  
    - The system uses a **retriever** (A retriever is a system or component whose job is to find the most relevant pieces of information from a large collection of documents, based on a user’s query.) to search an external knowledge base (e.g., documents, database, FAQs).  

    - This may use `vector search`(is a modern, powerful technique used by retrievers to find relevant documents based on meaning, not just keywords.) to find the top-k relevant documents.
        -  **How does RAG find the right page in your document?** It uses "embeddings." Imagine every word or sentence can be turned into a secret code of numbers. Words with similar meanings will have similar number codes.
        *   When you ask a question, your question is also turned into a number code. The system then looks for pieces of your document that have number codes most similar to your question's code. That's how it finds the relevant info!

    3. **Augmentation Phase**  
    - The top documents (contexts) are **appended** to the original query or prompt. This extended prompt now includes both the user's input and the retrieved context.

    4. **Generation Phase**  
    - The **generator** (e.g., GPT-4, LLaMA, Claude) receives the augmented input and generates a coherent, informed response.

    
    *Example:* You upload your "Clubhouse Rules" document. Then you ask, "Robot, what is rule #3 for the clubhouse?" It will find that rule in *your* document and tell you.

**Vector Database Comparison for RAG Systems**

| Name       | Open Source | Scalable      | Metadata Filtering | Best For                    |
|------------|-------------|---------------|---------------------|-----------------------------|
| FAISS      | ✅ Yes      | ❌ Local only | ❌ No              | Research/prototype         |
| Pinecone   | ❌ No       | ✅ Yes       | ✅ Yes              | Production                 |
| Weaviate   | ✅ Yes      | ✅ Yes       | ✅ Yes              | Flexible apps              |
| Qdrant     | ✅ Yes      | ✅ Yes       | ✅ Yes              | Fast + flexible            |
| Milvus     | ✅ Yes      | ✅ Yes       | ✅ Yes              | Enterprise scale           |
| ChromaDB   | ✅ Yes      | ❌ Local     | ✅ Yes              | Prototyping                |
| Elastic    | ✅ Yes      | ✅ Yes       | ✅ Yes              | Hybrid keyword + vector    |



---
3.  **API Calls (The Secret Robot Hotline):**
    - **API Prompting** refers to interacting with a large language model (LLM) like GPT programmatically using an **Application Programming Interface (API)** instead of a chat interface.

    - It enables developers to send prompts and receive responses directly through code, allowing for automation, scalability, and integration into applications.

   ```json
{
  "model": "gpt-4",
  "messages": [
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "Explain relativity in simple terms."}
  ],
  "temperature": 0.7
}

```

4.  **Fine-tuning Basics (Robot Special School):**
    *   **Story:** Imagine you have a generally smart robot (like ChatGPT). Fine-tuning is like sending that robot to a special school to become an expert in *one specific subject* by showing it lots of examples.  

    *   For example, if you want a robot that's amazing at writing poems in the style of Dr. Seuss, you could "fine-tune" a general AI by feeding it hundreds of Dr. Seuss poems. It's more advanced than just prompting.


🔧 **Tools for this Land:** `LangChain` (a popular toolbox for building with LLMs, RAG, and agents), `OpenAI Playground` (a place to experiment with API calls and settings directly), `Vector DBs` (special databases for storing those "embeddings" or number codes, like `Pinecone`), `VectorShift` (a platform that might help build RAG).

✨ **Extra Topics for Level 2:**
*   **Iterative Prompting:**   
The first prompt you write is rarely perfect. You'll try a prompt, see the result, change your prompt, and try again. It's like tuning an instrument.  
    1. Sending a prompt
    2. Evaluating the response
    3. Refining the prompt based on that evaluation
    4. Repeating until the desired output is achieved
*   **Prompt Hacking/Jailbreaking (and why to be careful):**  
 Some people try to trick AIs into saying things they're not supposed to. It's important to understand this exists but also to use AI responsibly.

*   **Temperature & Other Parameters:**   
When using APIs, you can change settings like "temperature." High temperature = more creative/random answers. Low temperature = more focused/predictable answers.

