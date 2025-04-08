

# LangGraph Travel-Sales Agent

This project demonstrates a modular conversational assistant built using LangGraph and LangChain. It features two specialized agents—Travel Consultant and Sales Consultant—that collaboratively respond to user queries about travel packages. The routing logic ensures that questions are directed to the appropriate expert based on their intent.

## Overview

The LangGraph Travel-Sales Agent simulates a real-world travel inquiry system where customers can ask questions about destinations, attractions, durations, prices, and package details. The system intelligently decides whether a question should be handled by the Travel Consultant, the Sales Consultant, or both.

# Data Preparation Flow
```


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
```

LangGraph Travel-Sales Agent is live. Type 'exit' to quit.
[TRAVEL NODE]
Question: what are best destination in italy ?

Final Answer: Some of the best destinations in Italy are Rome, Florence, Venice, Milan, and the Amalfi Coast.


[TRAVEL NODE]
Question: what are the packages available for rome ? 

Final Answer: The packages available for Rome are:
1) Budget-Friendly Rome Trip (ADV-R-1592)
2) Budget-Friendly Rome Trip (ROM-R-9076)
3) Budget-Friendly Rome Trip (ADV-R-6591)
4) Budget-Friendly Rome Trip (WLD-R-2153)


[SALES NODE]
Question: what is the duration For Budget-Friendly Rome Trip (ADV-R-1592)?

Final Answer: The duration of the Budget-Friendly Rome Trip (ADV-R-1592) is 2 nights and 6 days.


[SALES NODE]
Question: what is the price for it?

Final Answer: The total cost for the Budget-Friendly Rome Trip (ADV-R-1592) is 17889.


[SALES NODE]
Question: what are exclusions and inclusion for it ?

Final Answer: For the Budget-Friendly Rome Trip (ADV-R-1592):
- **Inclusions**: Bus, Guided Tours, Dinner
- **Exclusions**: Entry tickets, Lunch


[SALES NODE]
Question: what is the cheapest pakage available for rome?

Final Answer: The cheapest package available for Rome is 'Budget-Friendly Rome Trip (ADV-R-1592)' with a total cost of 17889.


[SALES NODE]
Question: what is the costliest package avaolable for rome ?

Final Answer: The costliest package available for Rome is 'Budget-Friendly Rome Trip (WLD-R-7572)' with a total cost of 93935.


[MULTI NODE]

Final Answer: The duration of the Budget-Friendly Rome Trip (ROM-R-9076) is 3 nights/6 days. The main attractions included in this package are Duomo Cathedral, Hagia Sophia, and Table Mountain.

The duration is 6N/3D and the main attractions included in the costliest package are Duomo Cathedral, Opera House, Christ the Redeemer.

Ending chat.

```

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
