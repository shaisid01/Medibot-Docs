## Multi-Turn Context-Aware Medical Assistant
### Introduction
MediBot is an AI-powered educational medical assistant designed to predict diseases, assess symptom severity, provide disease descriptions, and recommend precautions. It leverages multi-turn conversations, persistent personalized memory, RAG (FAISS engine), ReAct-style reasoning, and multi-modal NLP capabilities.
### Key Features
•	Multi-turn user interactions with context preservation
</br>•	Persistent, personalized memory for each user
</br>•	Context-aware decision making with FAISS retrieval
</br>•	LLM fallback for cases with insufficient evidence
</br>•	Structured tool integration using ReAct-style LangChain agents
</br>•	Multi-modal input: text and optional skin images
</br>•	Symptom severity scoring and disease precaution advice
</br>•	Prompt engineering for safe, accurate, and structured responses
### MediBot flowchart
**Context-Aware**  
All responses consider previous AI messages via `merged_context`.

**Retrieval-First Approach**  
FAISS ensures high-confidence disease matches before agent or LLM execution.

**Router-Based Decision**  
LLM decides the next step dynamically: clarify, follow-up, free-flow, or call agent.

**Agent Workflow**  
- Only invoked for actionable cases to produce structured diagnosis.  
- Uses ReAct-style reasoning tools.

**LLM Fallback**  
Ensures users always get educational guidance if no matches are found.

**Session Memory**  
Updated session memory with the user query and AI response, not the whole prompt.

**User-Friendly Markdown Output**  
Structured sections for diseases, severity, descriptions, and precautions.

**Traceable / Debuggable**  
Optional `trace_event()` logging at each step for monitoring or debugging.

```
User Query
   │
   ▼
Merge Previous AI Messages → Create merged_context
   │
   ▼
FAISS Retrieval → Are there matching diseases?
   ├─ Yes
   │    ├─ Router Decision → Determine action:
   │    │    • clarify
   │    │    • llm (free-flow)
   │    │    • follow_up
   │    │    • call_agent
   │    │
   │    └─ Action Handling:
   │         ├─ clarify / llm
   │         │    └─ Generate free-flow educational response
   │         │         • Markdown output
   │         │
   │         ├─ follow_up
   │         │    └─ call_agents_for_followup_query()
   │         │     |    • Format free-flow markdown
   |         |     |
   |         |     | __LLM fallback if no reponse
   │         │
   │         └─ call_agent
   │              ├─ call_agents_for_new_query()
   │              │    | • ReAct agent tools:
   │              │    |    - diagnose_disease
   │              │    |     - symptom_severity
   │              │    |    - disease_description
   │              │    |     - advise_precautions
   |              |    |
   |              |    |___LLM fallback if no reponse
   |              |   
   |              |
   │              ├─ Extract final JSON answer from LLM output
   │              ├─ Update session memory with the user query and AI response
   │              └─ Generate user-friendly markdown:
   │                    🔍 Possible Diseases
   │                    ⚠️ Severity Assessment
   │                    📖 Disease Descriptions
   │                    🛡️ Recommended Precautions
   │
   └─ No
        │
        ▼
    LLM Fallback → Generate educational response:

```
### System Architecture
<img width="1291" height="776" alt="MediBot_System_Architecture" src="https://github.com/user-attachments/assets/55b3ded3-5dfe-4b5b-b7e4-9c0f6567851a" />

1. User input (text + optional image) → FAISS vector search for symptom-disease matches.
2. LLM Router → determines action: call agent, follow-up, clarify, or LLM fallback.
3. Agent Tools → diagnose disease, assess severity, describe disease, advise precautions.
4. Session Memory → maintains multi-turn context and personalized user history.
5. Multi-Modal Fusion → combines text embeddings (SentenceTransformer) with image embeddings (ResNet50).
6. Output → structured JSON + Markdown response to the user.

### Agents Interaction
<img width="1407" height="627" alt="MediBot_Agent_Interaction" src="https://github.com/user-attachments/assets/8b589895-3cb0-47cb-8b31-67d0771a784a" />

### Installation
1. Clone the repository.
2. Install dependencies:
   pip install -r requirements.txt
3. Set your OpenAI API key in environment variables or via getpass.
4. Launch MediBot with Gradio interface:
   python app.py
### Usage
1. Enter your User ID and symptoms/questions.
2. Optionally, upload a skin image for multi-modal analysis.
3. Submit query → receive possible diseases, severity, descriptions, and precautions.
4. Rate AI responses and provide feedback.
5. View conversation summary or persistent memory for context.
### Contribution
Contributions are welcome. Fork the repository, submit a pull request, or report issues.
### License
This project is for educational purposes only. Not a substitute for medical advice. Refer to a licensed medical professional for health concerns.

