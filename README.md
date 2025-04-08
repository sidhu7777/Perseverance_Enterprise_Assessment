

# LangGraph Travel-Sales Agent

This project demonstrates a modular conversational assistant built using LangGraph and LangChain. It features two specialized agents—Travel Consultant and Sales Consultant—that collaboratively respond to user queries about travel packages. The routing logic ensures that questions are directed to the appropriate expert based on their intent.

## Overview

The LangGraph Travel-Sales Agent simulates a real-world travel inquiry system where customers can ask questions about destinations, attractions, durations, prices, and package details. The system intelligently decides whether a question should be handled by the Travel Consultant, the Sales Consultant, or both.

# Data Preparation Flow
```

Faker + Templates
   ↓
Travel Packages Dataset (5,000 rows)
   ↓
Combined Text
   ↓
Embedding via HuggingFace Model
   ↓
Saved to Pickle + Uploaded to Pinecone

```


###  System Architecture Diagram


![System Architecture](https://github.com/sidhu7777/Perseverance_Enterprise_Assessment/raw/main/images/Assesment.png)




## Key Features

- **Agent Routing with LangGraph**  
  Uses LangGraph to build a conditional conversational flow that routes user input to the correct node based on the type of question.

- **Specialized Agent Roles**  
  The Travel Consultant handles questions about destinations, attractions, itineraries, and the best time to visit.  
  The Sales Consultant handles questions about pricing, inclusions, exclusions, durations, and cost comparisons.

- **Conversational Memory**  
  Each agent uses `ConversationBufferMemory` to retain context across interactions within its domain.

- **Custom Prompt Engineering**  
  Prompts are carefully designed to keep each agent within its role, improving answer accuracy and domain separation.

- **Multi-Agent Handling**  
  For queries involving both travel and sales aspects (e.g., "What are the packages available for Rome and how much do they cost?"), the system activates both agents and merges their answers appropriately.

## Technologies Used

- LangGraph for managing the conversational graph flow
- LangChain for chaining LLM calls and memory integration
- OpenAI GPT-3.5-Turbo as the language model
- Python for backend logic and orchestration

## How It Works

1. The user's question is first passed to a router powered by a language model.
2. Based on the detected intent, the router selects one of four paths:
   - Travel Agent
   - Sales Agent
   - Multi-Agent (both travel and sales)
   - Fallback (unrecognized or unsupported queries)
3. Each agent runs a `ConversationalRetrievalChain` over travel package data and responds within its defined scope.
4. The final answer is returned and printed to the user.

# LangGraph Flow Diagram

                [ Start / User Query ]
                          ↓
                    [ Router Node ]
             ┌──────────┼───────────┐
             ↓          ↓           ↓
        [Travel]    [Sales]     [Multi]
             ↓          ↓           ↓
           [END]      [END]       [END]
                          ↓
                    [Fallback]

# Retrieval Chain Diagram (for each agent)

```

User Query
   ↓
Prompt + Retriever
   ↓
Relevant Embeddings from Pinecone
   ↓
Context + Query to LLM
   ↓
Final Answer

```




## Example Interaction

**User:** What are the packages available for Paris?  
**Travel Consultant:**  
The Paris packages available are:  
1. Budget-Friendly Paris Trip (ROM-P-2922) - 5N/3D trip during Autumn  
2. Budget-Friendly Paris Trip (WLD-P-4471) - 2N/6D trip during Spring  
3. Budget-Friendly Paris Trip (ADV-P-7710) - 3N/5D trip during Autumn  
4. Budget-Friendly Paris Trip (REL-P-4089) - 2N/5D trip during Summer  

Please let me know if you would like more information on any specific package.

**User:** What is the cost for the Budget-Friendly Paris Trip (ROM-P-2922)?  
**Sales Consultant:**  
The total cost for the Budget-Friendly Paris Trip (ROM-P-2922) is 28,900.

## Design Considerations

- Clear separation of domain responsibilities between agents
- Use of modular helper functions to avoid duplicated logic
- Clean and readable agent prompts to prevent role confusion
- Fallback logic to handle unsupported or ambiguous questions gracefully
- Avoidance of redundant or duplicated responses in multi-agent outputs

## Submission Notes

- The codebase is organized and ready to run.
- A sample interaction is included in this README.
- Please review the prompt definitions and `multi_node` logic for clarity on response flow and routing.

## How to Run

1. Install dependencies listed in `requirements.txt`
2. Set up your OpenAI API key in a `.env` file
3. Run the script using Python
4. Type your questions in the console to interact with the agent

## Contact

Vineeth Raja Banala  
Recent MSc Data Science Graduate  
For questions, feel free to reach out via GitHub or email (bvineeth76@gmail.com).

---
