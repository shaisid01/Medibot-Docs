## MediBot: Multi-Turn Context-Aware Medical Assistant
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

