# Microsoft AI-103 Exam Study Plan
## Developing AI Apps and Agents on Azure
### Passing in 4 Weeks — Complete Self-Study Guide

---

> **Your Profile:** 15 years engineering, conceptual knowledge of Azure OpenAI / AI Search / AI Foundry, Python learner (quick pick-up), studying 7 days/week.
> **Exam:** AI-103 | 40–60 questions | 120 minutes | 700/1000 to pass | $165 USD | Pearson VUE

---

## TABLE OF CONTENTS

1. [Exam Blueprint — Know What You're Fighting](#1-exam-blueprint)
2. [Day 0 — Environment Setup (Do This First)](#2-day-0-setup)
3. [Week 1 — Foundation & Domain 1: Plan and Manage (Days 1–7)](#3-week-1)
4. [Week 2 — Domain 2: Generative AI & Agentic Solutions (Days 8–14)](#4-week-2)
5. [Week 3 — Domains 3, 4, 5: Vision, NLP, Information Extraction (Days 15–21)](#5-week-3)
6. [Week 4 — Integration, Practice Tests & Exam Readiness (Days 22–28)](#6-week-4)
7. [Python Quick Reference — All Services in One Place](#7-python-reference)
8. [Exam Strategy & Day-of Checklist](#8-exam-day)
9. [Master Resource List](#9-resources)

---

## 1. EXAM BLUEPRINT

### Domain Weightings (April 2026 Official)

| # | Domain | Weight | Your Priority |
|---|--------|--------|--------------|
| 1 | Plan and manage an Azure AI solution | 25–30% | HIGH |
| 2 | Implement generative AI and agentic solutions | 30–35% | **HIGHEST** |
| 3 | Implement computer vision solutions | 10–15% | MEDIUM |
| 4 | Implement text analysis solutions | 10–15% | MEDIUM |
| 5 | Implement information extraction solutions | 10–15% | MEDIUM |

**Key insight:** Domains 1 and 2 together are 55–65% of the exam. Nail those first.

### How the Exam Tests You

The exam does NOT ask "what does service X do?" It asks:
- "A customer needs to do Y with constraint Z — which service and configuration?"
- "This code is failing — what is wrong?"
- "Which approach is most cost-effective / secure / scalable?"

**Think in decisions, not definitions.**

### What Changed from AI-102

AI-103 is NOT AI-102 with a refresh. Key shifts:
- **Azure AI Foundry** is the unified platform for everything — not separate cognitive service portals
- **Agentic solutions** are now 30–35% (vs ~15% in AI-102)
- **RAG pipelines** are first-class exam content
- **Semantic Kernel** replaces Bot Framework as the agent SDK focus
- **Content Understanding** is a new service (replaces some Form Recognizer use cases)

---

## 2. DAY 0 — ENVIRONMENT SETUP

Complete this on Day 0 before your Week 1 begins. Budget: ~3 hours.

### Step 1: Azure Free Account

1. Go to: **https://azure.microsoft.com/free**
2. Click "Start free" — requires a Microsoft account + credit card (not charged)
3. You get: $200 credit for 30 days + 12 months of free services
4. After creating: Go to **portal.azure.com** and verify you can log in

> **Important for AI-103 labs:** Azure OpenAI access requires a separate approval.
> Immediately after creating your account, go to:
> **https://aka.ms/oai/access** → fill the form → approval takes 1–3 business days.
> Do this on Day 0 so it's ready by the time you need it in Week 2.

### Step 2: Azure AI Foundry Access

1. Go to: **https://ai.azure.com**
2. Sign in with your Azure account
3. Click "Create project" → you'll be prompted to create a Hub first
4. For the Hub: choose a region with OpenAI availability (e.g., East US, Sweden Central)
5. Create a project inside the hub — name it `ai103-lab`

### Step 3: Python Environment

Install in this order:

```bash
# 1. Install Python 3.11+ from https://python.org
# Verify:
python --version  # Should show 3.11 or higher

# 2. Install VS Code from https://code.visualstudio.com
# Then install these VS Code extensions:
# - Python (Microsoft)
# - Pylance
# - Azure Tools

# 3. Create a project folder and virtual environment
mkdir ai103-labs
cd ai103-labs
python -m venv venv

# Activate (Windows):
venv\Scripts\activate
# Activate (Mac/Linux):
source venv/bin/activate

# 4. Install all Azure AI SDKs you'll need for the exam
pip install azure-ai-projects
pip install azure-ai-inference
pip install azure-ai-textanalytics
pip install azure-ai-vision-imageanalysis
pip install azure-ai-formrecognizer
pip install azure-search-documents
pip install azure-cognitiveservices-speech
pip install openai
pip install azure-identity
pip install python-dotenv
```

### Step 4: Create .env File (Use for All Labs)

Create a file called `.env` in your `ai103-labs` folder:

```
AZURE_OPENAI_ENDPOINT=https://YOUR_RESOURCE.openai.azure.com/
AZURE_OPENAI_KEY=your_key_here
AZURE_OPENAI_DEPLOYMENT=gpt-4o
AZURE_AI_SEARCH_ENDPOINT=https://YOUR_SEARCH.search.windows.net
AZURE_AI_SEARCH_KEY=your_key_here
AZURE_AI_SEARCH_INDEX=ai103-index
LANGUAGE_ENDPOINT=https://YOUR_RESOURCE.cognitiveservices.azure.com/
LANGUAGE_KEY=your_key_here
VISION_ENDPOINT=https://YOUR_RESOURCE.cognitiveservices.azure.com/
VISION_KEY=your_key_here
DOCUMENT_INTELLIGENCE_ENDPOINT=https://YOUR_RESOURCE.cognitiveservices.azure.com/
DOCUMENT_INTELLIGENCE_KEY=your_key_here
SPEECH_KEY=your_key_here
SPEECH_REGION=eastus
AZURE_PROJECT_CONNECTION_STRING=your_foundry_connection_string
```

Load it in every Python file:
```python
from dotenv import load_dotenv
import os
load_dotenv()
```

### Step 5: Install Azure CLI

1. Download from: **https://docs.microsoft.com/cli/azure/install-azure-cli**
2. After install:
```bash
az login                    # Opens browser for auth
az account show             # Verify correct subscription
az account list --output table  # See all subscriptions
```

### Step 6: Bookmark These URLs (Open All Now)

| URL | What It Is |
|-----|------------|
| https://learn.microsoft.com/credentials/certifications/resources/study-guides/ai-103 | Official study guide — your bible |
| https://learn.microsoft.com/training/paths/develop-ai-apps-agents-azure/ | Official Microsoft Learn path |
| https://ai.azure.com | Azure AI Foundry portal |
| https://portal.azure.com | Azure portal |
| https://mscertquiz.com/certifications/ai-103 | 40 free practice questions |
| https://open-exam-prep.com/practice/ai-103 | Free practice questions |

---

## 3. WEEK 1 — FOUNDATION & DOMAIN 1: PLAN AND MANAGE

**Domain 1 weight: 25–30%**
**Goal: Understand Azure AI Foundry architecture, security, responsible AI, monitoring, and model selection.**

**Weekly schedule: 2 hrs weekdays, 3 hrs weekends = ~16 hrs this week**

---

### DAY 1 (2 hrs) — Azure AI Foundry Architecture

**What to read:**
- Microsoft Learn: "Introduction to Azure AI Foundry" → https://learn.microsoft.com/training/modules/introduction-to-azure-ai-studio/
- Microsoft Learn: "Plan and manage Azure AI Foundry" → https://learn.microsoft.com/training/modules/plan-manage-azure-ai-foundry/

**Core concepts to understand:**

**Hub vs Project:**
- **Hub** = the top-level resource. Controls shared infrastructure: networking, keys, storage, compute. One hub can serve many teams.
- **Project** = a workspace inside a hub. Developers work here. Contains deployments, datasets, experiments.
- **Analogy:** Hub = office building (shared utilities). Project = individual team's floor.

**Connections in AI Foundry:**
- A connection links your Foundry project to external services (Azure OpenAI, AI Search, storage).
- Connection types: Azure AI Services, Azure OpenAI, Azure AI Search, Azure Blob Storage, custom.
- Connections can be shared at Hub level (all projects) or local (one project only).

**Model Catalog:**
- AI Foundry's model catalog contains OpenAI models, open-source models (Llama, Mistral, Phi), and fine-tuned variants.
- Models are deployed as "endpoints" within your project.
- Deployment types: Standard (shared compute), Provisioned (dedicated throughput).

**Key exam question type:**
> "A company wants to share an Azure OpenAI connection across 5 development teams without each team managing their own credentials. How should they structure their AI Foundry resources?"
> **Answer: Create one Hub, configure the OpenAI connection at Hub level, create one Project per team.**

**Lab (30 mins):**
1. Log in to https://ai.azure.com
2. Create a Hub → choose East US region
3. Create a Project named `ai103-lab` inside the hub
4. Explore: Connections tab, Model catalog, Deployments

---

### DAY 2 (2 hrs) — Authentication and Security

**What to read:**
- Microsoft Learn: "Secure Azure AI services" → https://learn.microsoft.com/training/modules/secure-ai-services/
- Microsoft Learn: "Authenticate to Azure AI services" → https://learn.microsoft.com/training/modules/authenticate-azure-ai-services/

**Core concepts:**

**Two ways to authenticate:**

1. **API Keys** — simpler, less secure
   - Each Azure AI resource has two keys (key1, key2)
   - Passed in request headers: `Ocp-Apim-Subscription-Key`
   - Suitable for development, not recommended for production

2. **Microsoft Entra ID (formerly Azure AD)** — recommended for production
   - Uses service principals or managed identities
   - No secrets stored in code
   - Requires assigning RBAC roles

**Critical RBAC Roles for AI-103 exam:**

| Role | Can Do |
|------|--------|
| `Cognitive Services User` | Call APIs, run inference |
| `Cognitive Services OpenAI User` | Call Azure OpenAI inference endpoints |
| `Cognitive Services OpenAI Contributor` | Deploy and manage OpenAI models |
| `Azure AI Developer` | Full developer access to AI Foundry resources |
| `Azure AI Administrator` | Admin access including hub management |

**Managed Identity — the preferred production pattern:**

```python
from azure.identity import DefaultAzureCredential, ManagedIdentityCredential
from azure.ai.textanalytics import TextAnalyticsClient

# In production (Azure VM, App Service, Azure Functions):
# Use ManagedIdentityCredential — no keys, no secrets
credential = ManagedIdentityCredential()

# In development (your local machine after `az login`):
# DefaultAzureCredential tries multiple auth methods in order
credential = DefaultAzureCredential()

client = TextAnalyticsClient(
    endpoint=os.getenv("LANGUAGE_ENDPOINT"),
    credential=credential  # No key needed!
)
```

**Network Security:**
- **Private Endpoint:** AI service gets a private IP in your VNet. Traffic never leaves Azure backbone.
- **Service Endpoint:** Restricts traffic to specific Azure VNets (less secure than private endpoint).
- **Firewall rules:** Restrict access to specific public IP ranges.
- **VNet Integration:** Required for AI Foundry when using private endpoints.

**Key exam question type:**
> "A company requires that their Azure OpenAI service is not accessible from the public internet. What should they configure?"
> **Answer: Private endpoint + disable public network access on the resource.**

**Lab (30 mins):**
```python
# test_auth.py — try key-based auth
import os
from azure.ai.textanalytics import TextAnalyticsClient
from azure.core.credentials import AzureKeyCredential
from dotenv import load_dotenv
load_dotenv()

client = TextAnalyticsClient(
    endpoint=os.getenv("LANGUAGE_ENDPOINT"),
    credential=AzureKeyCredential(os.getenv("LANGUAGE_KEY"))
)
result = client.detect_language(["Hello, how are you?"])
print(result[0].primary_language.name)  # Should print: English
```

---

### DAY 3 (2 hrs) — Responsible AI and Content Safety

**What to read:**
- Microsoft Learn: "Fundamentals of Responsible Generative AI" → https://learn.microsoft.com/training/modules/responsible-generative-ai/
- Microsoft Learn: "Detect and mitigate unfairness in AI models" → https://learn.microsoft.com/training/modules/detect-mitigate-unfairness-models-with-azure-machine-learning/

**Microsoft's 6 Responsible AI Principles (memorize these):**

| Principle | What It Means |
|-----------|--------------|
| **Fairness** | AI treats all people equitably; no bias based on race, gender, etc. |
| **Reliability & Safety** | AI performs consistently; fails safely |
| **Privacy & Security** | AI respects data privacy; protects against misuse |
| **Inclusiveness** | AI benefits everyone; accessible to people with disabilities |
| **Transparency** | AI decisions can be explained; users know they're using AI |
| **Accountability** | People are responsible for AI systems; human oversight |

**Azure AI Content Safety Service:**
- Standalone service (also built into AI Foundry) that detects harmful content
- Categories: Hate, Violence, Sexual, Self-harm
- Each category gets a severity score: 0 (safe) to 7 (extremely harmful)
- You set a threshold — content above threshold is blocked

```python
# content_safety_demo.py
from azure.ai.contentsafety import ContentSafetyClient
from azure.ai.contentsafety.models import AnalyzeTextOptions
from azure.core.credentials import AzureKeyCredential
import os
from dotenv import load_dotenv
load_dotenv()

client = ContentSafetyClient(
    endpoint=os.getenv("CONTENT_SAFETY_ENDPOINT"),
    credential=AzureKeyCredential(os.getenv("CONTENT_SAFETY_KEY"))
)

request = AnalyzeTextOptions(text="I want to hurt someone")
response = client.analyze_text(request)

for category in response.categories_analysis:
    print(f"{category.category}: severity={category.severity}")
    # Output: Violence: severity=4
```

**Content Filters in Azure OpenAI:**
- Every Azure OpenAI deployment has default content filters (on by default)
- Can be customized: adjust thresholds per category, add custom blocklists
- In AI Foundry: your Project → Safety + security → Content filters

**Groundedness Detection:**
- Checks if a model's response is grounded in the provided source documents (for RAG)
- Detects hallucinations: model claims something not in the source
- Important for RAG pipelines in exam scenarios

**Key exam question type:**
> "A financial services company is deploying an AI chatbot. They need to ensure the model's answers are based only on their approved documents and not invented. Which Azure AI feature addresses this?"
> **Answer: Groundedness detection in Azure AI Content Safety (or Azure AI Evaluation).**

---

### DAY 4 (2 hrs) — Model Selection and Cost Management

**What to read:**
- Microsoft Learn: "Select and deploy a language model" → https://learn.microsoft.com/training/modules/explore-models-azure-ai-foundry/
- Azure OpenAI pricing page: https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/

**Model Selection — The Exam Loves Scenario Questions:**

| Scenario | Best Model Choice |
|----------|------------------|
| Simple chat, cost-sensitive | GPT-4o-mini or Phi-3-mini |
| Complex reasoning, coding | GPT-4o or o3 |
| Real-time voice conversation | GPT-4o Realtime |
| Embedding/vector search | text-embedding-3-small / text-embedding-3-large |
| Image understanding | GPT-4o (multimodal) |
| Batch processing, not time-sensitive | Use batch API |
| On-premises / air-gapped deployment | Azure AI on edge / Phi family (small models) |
| Open-source preference, avoid vendor lock-in | Llama, Mistral from model catalog |

**Token Pricing Concepts:**
- Azure OpenAI charges per **token** (not per request)
- 1 token ≈ 4 characters in English
- Charged separately: **input tokens** (prompt) and **output tokens** (completion)
- Output tokens cost more than input tokens
- **Cached input tokens** (repeating same system prompt) cost ~50% less

**Provisioned Throughput Units (PTU):**
- Dedicated compute for OpenAI — guaranteed throughput, no rate limits
- More expensive upfront, but predictable for high-volume production
- Exam question: "A company has a consistent high volume of API calls and cannot tolerate rate limiting" → Provisioned throughput

**Monitoring Azure AI Services:**
- Azure Monitor → Diagnostics → Enable diagnostic settings on your AI resource
- Key metrics to monitor: `TotalCalls`, `TotalErrors`, `SuccessfulCalls`, `Latency`
- Set up alerts in Azure Monitor for error rate thresholds
- Costs visible in: Azure Cost Management → Filter by resource

**Lab (30 mins):**
1. In Azure AI Foundry (ai.azure.com):
   - Go to Model catalog → filter by "Chat completion"
   - Click GPT-4o → read the capability summary
   - Click "Deploy" (if OpenAI access is approved) → choose "Standard" deployment
   - Note the TPM (tokens per minute) limit on free tier: 8,000 TPM

---

### DAY 5 (2 hrs) — Container Deployments and Monitoring

**What to read:**
- Microsoft Learn: "Deploy Azure AI services in containers" → https://learn.microsoft.com/training/modules/investigate-container-for-use-with-ai-services/

**Why Containers for AI Services?**
- Run AI services in your own infrastructure (on-prem, edge, other clouds)
- Data never leaves your network (compliance requirement)
- Same REST API as cloud — minimal code changes

**Container Key Facts:**
- Available for: Language, Vision, Speech, Document Intelligence (not all services)
- Containers still call home to Azure for billing/licensing (internet connection required even for on-prem)
- Exception: Disconnected containers exist but require special licensing

**Running a Language service container:**
```bash
# Pull the sentiment analysis container
docker pull mcr.microsoft.com/azure-cognitive-services/textanalytics/sentiment:latest

# Run it (must provide your Azure billing endpoint)
docker run --rm -it -p 5000:5000 \
  mcr.microsoft.com/azure-cognitive-services/textanalytics/sentiment:latest \
  Eula=accept \
  Billing=https://YOUR_RESOURCE.cognitiveservices.azure.com/ \
  ApiKey=YOUR_KEY
```

**After running, call the local container — same API as cloud:**
```python
# Call local container instead of Azure endpoint
client = TextAnalyticsClient(
    endpoint="http://localhost:5000",  # Local container
    credential=AzureKeyCredential("placeholder")  # Any non-empty string
)
```

**Key exam question type:**
> "A hospital processes patient records and cannot send data to Azure due to compliance. They want to use Azure AI Language for sentiment analysis. What should they use?"
> **Answer: Azure AI Language container, deployed on-premises.**

**Lab (30 mins):**
- Read the container list: https://learn.microsoft.com/azure/ai-services/cognitive-services-container-support
- Note which services support disconnected operation vs which require billing callback

---

### DAY 6 (Weekend — 3 hrs) — Domain 1 Deep Practice

**What to do:**

**Hour 1: Review and consolidate**
- Re-read your notes from Days 1–5
- For each service you've seen, answer: What does it do? When would I choose it? What's the security model?

**Hour 2: Microsoft Learn Path (complete the modules)**
- Complete the full Domain 1 learning path:
  https://learn.microsoft.com/training/paths/develop-ai-apps-agents-azure/
  → Do sections: "Plan and manage an Azure AI solution"

**Hour 3: Practice questions — Domain 1 focus**
- Go to: https://mscertquiz.com/certifications/ai-103
- Take the free 40-question test
- For every wrong answer: read the explanation fully, understand WHY
- Target: 70%+ on Domain 1 questions

**Domain 1 Cheat Sheet (memorize before moving on):**
```
Hub = shared infrastructure, connections, network settings
Project = developer workspace inside a hub
Managed Identity = production auth (no keys in code)
Private Endpoint = no public internet access to AI service
Content filters = built into Azure OpenAI deployments
6 Responsible AI principles: Fairness, Reliability, Privacy, Inclusiveness, Transparency, Accountability
Groundedness = model answer must be from documents (for RAG)
Container needs billing callback = still needs internet for licensing
PTU = dedicated compute for high-volume, no rate limits
```

---

### DAY 7 (Weekend — 3 hrs) — Azure AI Foundry Hands-On Deep Dive

**What to do:**

**Hour 1: AI Foundry Portal Exploration**
1. Go to https://ai.azure.com → your project
2. Explore every menu item — know what each section does:
   - **Overview:** Project connection string, hub info
   - **Model catalog:** Browse available models
   - **Deployments:** Your deployed model endpoints
   - **Prompt flow:** Visual pipeline builder
   - **Evaluations:** Model quality metrics
   - **Safety + security:** Content filters, blocklists
   - **Connections:** Linked services (OpenAI, Search, storage)

**Hour 2: Get your connection string and test Python connection**
```python
# test_foundry_connection.py
import os
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential
from dotenv import load_dotenv
load_dotenv()

# Get connection string from AI Foundry portal:
# Project → Overview → Copy "Project connection string"
client = AIProjectClient.from_connection_string(
    conn_str=os.getenv("AZURE_PROJECT_CONNECTION_STRING"),
    credential=DefaultAzureCredential()
)

# List available connections
connections = client.connections.list()
for conn in connections:
    print(f"Connection: {conn.name} | Type: {conn.connection_type}")
```

**Hour 3: Explore AI Foundry Prompt Flow (conceptual for exam)**
- In AI Foundry → Prompt flow → Create → Blank flow
- Understand node types:
  - **LLM node:** Calls a language model
  - **Python node:** Runs custom Python code
  - **Prompt node:** Template for building prompts
- Prompt Flow is used for: building complex AI pipelines, evaluation, deployment
- Exam question: "A team wants to build a multi-step AI pipeline with LLM calls, custom logic, and evaluation — which AI Foundry feature should they use?" → **Prompt Flow**

---

## 4. WEEK 2 — DOMAIN 2: GENERATIVE AI & AGENTIC SOLUTIONS

**Domain 2 weight: 30–35% — THE MOST IMPORTANT WEEK**
**Goal: Build RAG pipelines, AI agents, and understand Azure OpenAI deeply.**

---

### DAY 8 (2 hrs) — Azure OpenAI Service Deep Dive

**What to read:**
- Microsoft Learn: "Get started with Azure OpenAI" → https://learn.microsoft.com/training/modules/get-started-openai/
- Microsoft Learn: "Apply prompt engineering with Azure OpenAI" → https://learn.microsoft.com/training/modules/apply-prompt-engineering-azure-openai/

**Azure OpenAI vs OpenAI (openai.com):**
| Feature | Azure OpenAI | openai.com |
|---------|-------------|-----------|
| Data privacy | Data stays in Azure, not used for training | Used for training by default |
| Compliance | SOC2, HIPAA, GDPR | Less enterprise compliance |
| Authentication | Azure Entra ID, API keys | API keys only |
| Content filtering | Built-in, configurable | Basic |
| Models | GPT-4o, o3, embeddings (subset) | More models available sooner |

**The Chat Completions API:**
```python
# azure_openai_chat.py
import os
from openai import AzureOpenAI
from dotenv import load_dotenv
load_dotenv()

client = AzureOpenAI(
    azure_endpoint=os.getenv("AZURE_OPENAI_ENDPOINT"),
    api_key=os.getenv("AZURE_OPENAI_KEY"),
    api_version="2024-12-01-preview"  # Always use a recent version
)

response = client.chat.completions.create(
    model=os.getenv("AZURE_OPENAI_DEPLOYMENT"),  # Your deployment name, e.g. "gpt-4o"
    messages=[
        {
            "role": "system",
            "content": "You are a helpful assistant that explains technical concepts clearly."
        },
        {
            "role": "user",
            "content": "What is retrieval-augmented generation?"
        }
    ],
    max_tokens=500,
    temperature=0.7  # 0=deterministic, 1=creative. Use low for factual tasks.
)

print(response.choices[0].message.content)
print(f"Tokens used: {response.usage.total_tokens}")
```

**Key Parameters (exam tests these):**

| Parameter | Effect | When to Use |
|-----------|--------|-------------|
| `temperature=0` | Most deterministic, repeatable | Classification, fact extraction |
| `temperature=0.7` | Balanced | General chat |
| `temperature=1.0+` | Creative, varied | Story writing, brainstorming |
| `max_tokens` | Limits response length | Cost control |
| `top_p` | Alternative to temperature (don't use both) | Same as temperature |
| `stream=True` | Response streams token by token | Real-time chat UI |
| `seed` | Reproducible outputs | Testing |

**Embeddings — Required for RAG:**
```python
# embeddings_demo.py
import os
from openai import AzureOpenAI
from dotenv import load_dotenv
load_dotenv()

client = AzureOpenAI(
    azure_endpoint=os.getenv("AZURE_OPENAI_ENDPOINT"),
    api_key=os.getenv("AZURE_OPENAI_KEY"),
    api_version="2024-12-01-preview"
)

# Get embedding vector for a text
response = client.embeddings.create(
    model="text-embedding-3-small",  # Your embedding deployment name
    input="What is the capital of France?"
)

vector = response.data[0].embedding
print(f"Vector dimensions: {len(vector)}")  # 1536 for text-embedding-3-small
print(f"First 5 values: {vector[:5]}")
```

---

### DAY 9 (2 hrs) — Prompt Engineering

**What to read:**
- Microsoft Learn: "Apply prompt engineering with Azure OpenAI" → https://learn.microsoft.com/training/modules/apply-prompt-engineering-azure-openai/

**Core Prompt Engineering Techniques (Exam Tests All of These):**

**1. Zero-shot — No examples given:**
```python
messages = [
    {"role": "system", "content": "You are a sentiment analyzer."},
    {"role": "user", "content": "Classify this review as positive, neutral, or negative: 'The product broke after one day.'"}
]
# Model figures it out with no examples
```

**2. Few-shot — Give examples in the prompt:**
```python
messages = [
    {"role": "system", "content": "You are a sentiment analyzer. Classify reviews."},
    {"role": "user", "content": "The food was amazing!"},
    {"role": "assistant", "content": "Positive"},
    {"role": "user", "content": "It was okay, nothing special."},
    {"role": "assistant", "content": "Neutral"},
    {"role": "user", "content": "Terrible experience, never going back."},
    {"role": "assistant", "content": "Negative"},
    {"role": "user", "content": "The product broke after one day."}  # Actual question
]
```

**3. Chain-of-thought — Ask model to reason step-by-step:**
```python
messages = [
    {"role": "system", "content": "Solve problems step by step. Show your reasoning."},
    {"role": "user", "content": "If a train travels 120km in 2 hours, and then 80km in 1 hour, what is the average speed for the whole journey?"}
]
# Model will work through it rather than guess → more accurate
```

**4. System prompt — Sets model persona and constraints:**
```python
system_prompt = """
You are a customer service agent for Contoso Electronics.
- Only answer questions about Contoso products
- If asked about competitors, politely decline
- Always be professional and empathetic
- If you don't know an answer, say so — never make up information
"""
messages = [{"role": "system", "content": system_prompt}, ...]
```

**Key exam question type:**
> "A company deploys a chatbot but users are getting inconsistent answers for the same questions. They want deterministic responses. What should they change?"
> **Answer: Set `temperature=0` (and optionally `seed=<value>` for reproducibility).**

---

### DAY 10 (2 hrs) — RAG Pipelines (Retrieval-Augmented Generation)

**What to read:**
- Microsoft Learn: "Implement RAG with Azure OpenAI" → https://learn.microsoft.com/training/modules/use-own-data-azure-openai/
- Microsoft Learn: "Create a search solution" → https://learn.microsoft.com/training/modules/create-azure-cognitive-search-solution/

**Why RAG?**
LLMs have a training cutoff and don't know your private data. RAG solves this by:
1. Storing your documents in a searchable index
2. When user asks a question → search the index for relevant chunks
3. Pass those chunks + the question to the LLM
4. LLM answers using your documents (not its training data)

**RAG Architecture:**

```
User Question
     ↓
[Query Embedding] → vector(question)
     ↓
[Azure AI Search] → finds top-K similar document chunks
     ↓
[Context Builder] → "Answer this question: {question}\n\nUsing these documents:\n{chunks}"
     ↓
[Azure OpenAI LLM] → generates answer grounded in documents
     ↓
Answer to User
```

**Step-by-step RAG Implementation:**

```python
# rag_pipeline.py
import os
from openai import AzureOpenAI
from azure.search.documents import SearchClient
from azure.search.documents.models import VectorizedQuery
from azure.core.credentials import AzureKeyCredential
from dotenv import load_dotenv
load_dotenv()

# Setup clients
openai_client = AzureOpenAI(
    azure_endpoint=os.getenv("AZURE_OPENAI_ENDPOINT"),
    api_key=os.getenv("AZURE_OPENAI_KEY"),
    api_version="2024-12-01-preview"
)

search_client = SearchClient(
    endpoint=os.getenv("AZURE_AI_SEARCH_ENDPOINT"),
    index_name=os.getenv("AZURE_AI_SEARCH_INDEX"),
    credential=AzureKeyCredential(os.getenv("AZURE_AI_SEARCH_KEY"))
)

def get_embedding(text: str) -> list[float]:
    """Convert text to embedding vector."""
    response = openai_client.embeddings.create(
        model="text-embedding-3-small",
        input=text
    )
    return response.data[0].embedding

def search_documents(query: str, top_k: int = 3) -> list[str]:
    """Search index for relevant document chunks."""
    query_vector = get_embedding(query)
    
    vector_query = VectorizedQuery(
        vector=query_vector,
        k_nearest_neighbors=top_k,
        fields="content_vector"  # Name of the vector field in your index
    )
    
    results = search_client.search(
        search_text=query,           # Also do keyword search
        vector_queries=[vector_query], # AND vector search (hybrid)
        select=["title", "content"],
        top=top_k
    )
    
    return [doc["content"] for doc in results]

def rag_answer(user_question: str) -> str:
    """Full RAG pipeline: search → augment → generate."""
    # Step 1: Retrieve relevant documents
    docs = search_documents(user_question)
    context = "\n\n".join(docs)
    
    # Step 2: Augment prompt with context
    messages = [
        {
            "role": "system",
            "content": """Answer questions ONLY using the provided documents.
If the answer is not in the documents, say 'I don't have that information.'
Do not use your training knowledge."""
        },
        {
            "role": "user",
            "content": f"Documents:\n{context}\n\nQuestion: {user_question}"
        }
    ]
    
    # Step 3: Generate answer
    response = openai_client.chat.completions.create(
        model=os.getenv("AZURE_OPENAI_DEPLOYMENT"),
        messages=messages,
        temperature=0  # Deterministic for factual RAG
    )
    
    return response.choices[0].message.content

# Test it
answer = rag_answer("What is our refund policy?")
print(answer)
```

**Azure AI Search — Search Types (Exam Critical):**

| Search Type | How It Works | Best For |
|-------------|-------------|---------|
| **Keyword** | BM25 text matching | Exact terms, filters |
| **Vector** | Cosine similarity of embeddings | Semantic meaning, paraphrases |
| **Hybrid** | Combines keyword + vector | Best overall accuracy |
| **Semantic** | Re-ranks using language model | Rerank hybrid results for precision |

**Hybrid + Semantic = The Gold Standard for RAG:**
```python
from azure.search.documents.models import VectorizedQuery, QueryType

results = search_client.search(
    search_text=query,              # Keyword
    vector_queries=[vector_query],  # Vector
    query_type=QueryType.SEMANTIC,  # Semantic reranking on top
    semantic_configuration_name="my-semantic-config",
    top=5
)
```

---

### DAY 11 (2 hrs) — Azure AI Agent Service

**What to read:**
- Microsoft Learn: "Build agents with Azure AI Agent Service" → https://learn.microsoft.com/training/modules/build-language-solution-azure-openai/
- Azure AI Agent Service docs: https://learn.microsoft.com/azure/ai-services/agents/

**What is an AI Agent?**
An agent is an AI system that:
1. Takes a user goal
2. **Plans** steps to achieve it
3. **Uses tools** (search, code execution, APIs) to gather information
4. **Iterates** until the goal is achieved

**Key concepts:**

**Thread:** A conversation session. Stores message history. Persists between turns.

**Message:** A single user or assistant turn in a thread.

**Run:** When the agent executes on a thread. The agent reads the thread, uses tools, and produces a response.

**Tool:** What the agent can use. Built-in tools:
- `FileSearchTool` — searches uploaded documents (RAG)
- `CodeInterpreterTool` — executes Python code
- `BingGroundingTool` — searches the web
- Custom function tools — your own APIs

```python
# ai_agent_demo.py
import os
import time
from azure.ai.projects import AIProjectClient
from azure.ai.projects.models import (
    Agent, Thread, MessageRole,
    FileSearchTool, ToolSet
)
from azure.identity import DefaultAzureCredential
from dotenv import load_dotenv
load_dotenv()

# Create project client
project_client = AIProjectClient.from_connection_string(
    conn_str=os.getenv("AZURE_PROJECT_CONNECTION_STRING"),
    credential=DefaultAzureCredential()
)

# Step 1: Create an agent with file search capability
agent = project_client.agents.create_agent(
    model="gpt-4o",
    name="Document Assistant",
    instructions="""You are a helpful assistant. Answer questions using 
    the uploaded documents. Always cite your sources.""",
    tools=FileSearchTool().definitions,  # Enable file search
)
print(f"Agent created: {agent.id}")

# Step 2: Upload a document for the agent to search
with open("product_manual.pdf", "rb") as f:
    uploaded_file = project_client.agents.upload_file_and_poll(
        file=f,
        purpose="assistants"
    )

# Step 3: Create a vector store with the document
vector_store = project_client.agents.create_vector_store_and_poll(
    file_ids=[uploaded_file.id],
    name="product-docs"
)

# Attach vector store to agent
project_client.agents.update_agent(
    agent_id=agent.id,
    tool_resources={"file_search": {"vector_store_ids": [vector_store.id]}}
)

# Step 4: Create a thread (conversation)
thread = project_client.agents.create_thread()

# Step 5: Add user message
project_client.agents.create_message(
    thread_id=thread.id,
    role=MessageRole.USER,
    content="What is the warranty period for the product?"
)

# Step 6: Run the agent
run = project_client.agents.create_and_process_run(
    thread_id=thread.id,
    agent_id=agent.id
)
print(f"Run status: {run.status}")

# Step 7: Get the response
messages = project_client.agents.list_messages(thread_id=thread.id)
for msg in messages.data:
    if msg.role == MessageRole.ASSISTANT:
        print(f"Agent: {msg.content[0].text.value}")
```

**Function Calling (Custom Tools):**
```python
# Define a custom tool (your own API)
import json

def get_weather(location: str, unit: str = "celsius") -> str:
    """Simulate a weather API call."""
    # In real usage, call an actual weather API here
    return json.dumps({"location": location, "temperature": 22, "unit": unit})

# Define the tool schema for the agent
weather_tool_definition = {
    "type": "function",
    "function": {
        "name": "get_weather",
        "description": "Get the current weather for a location",
        "parameters": {
            "type": "object",
            "properties": {
                "location": {
                    "type": "string",
                    "description": "City and country, e.g. 'Bangalore, India'"
                },
                "unit": {
                    "type": "string",
                    "enum": ["celsius", "fahrenheit"]
                }
            },
            "required": ["location"]
        }
    }
}
```

---

### DAY 12 (2 hrs) — Semantic Kernel and Multi-Agent Orchestration

**What to read:**
- Microsoft Learn: "Develop AI agents with Semantic Kernel" → https://learn.microsoft.com/training/modules/develop-ai-agents-semantic-kernel/
- Semantic Kernel docs: https://learn.microsoft.com/semantic-kernel/overview/

**What is Semantic Kernel (SK)?**
- Microsoft's open-source SDK for building AI applications
- Orchestrates LLM calls, plugins (tools), memory, and planning
- Language support: Python, C#, Java
- Think of it as "middleware" between your app and AI services

**Core SK Concepts:**

| Concept | Description |
|---------|-------------|
| **Kernel** | Central orchestrator. Manages AI services and plugins |
| **Plugin** | Collection of functions the AI can call (tools) |
| **Function** | A single capability (Python function or prompt) |
| **Memory** | Stores and retrieves context (embeddings-based) |
| **Planner** | Lets AI autonomously choose which functions to call |

```python
# semantic_kernel_demo.py
import asyncio
import os
from semantic_kernel import Kernel
from semantic_kernel.connectors.ai.open_ai import AzureChatCompletion
from semantic_kernel.functions import kernel_function
from dotenv import load_dotenv
load_dotenv()

# Create kernel
kernel = Kernel()

# Add Azure OpenAI service
kernel.add_service(AzureChatCompletion(
    deployment_name=os.getenv("AZURE_OPENAI_DEPLOYMENT"),
    endpoint=os.getenv("AZURE_OPENAI_ENDPOINT"),
    api_key=os.getenv("AZURE_OPENAI_KEY")
))

# Define a plugin (tool the AI can use)
class EmailPlugin:
    @kernel_function(description="Send an email to a recipient")
    def send_email(self, recipient: str, subject: str, body: str) -> str:
        # In real usage, call email API here
        print(f"Sending email to {recipient}: {subject}")
        return f"Email sent to {recipient}"
    
    @kernel_function(description="Get emails from inbox")
    def get_emails(self) -> str:
        return "You have 3 unread emails."

# Register plugin with kernel
kernel.add_plugin(EmailPlugin(), plugin_name="email")

# Use the kernel in a chat
async def main():
    result = await kernel.invoke_prompt(
        "Check my emails and summarize what I need to do today",
        # SK automatically determines when to call get_emails()
    )
    print(result)

asyncio.run(main())
```

**Multi-Agent Patterns:**

| Pattern | When to Use |
|---------|-------------|
| **Sequential** | Agent A → Agent B → Agent C (pipeline) |
| **Parallel** | Multiple agents work simultaneously, results merged |
| **Supervisor** | One orchestrator agent delegates to specialist agents |
| **Debate** | Multiple agents critique each other's outputs |

**Key exam question type:**
> "A company wants to build a system where one AI agent triages customer requests and routes them to specialist agents for billing, technical support, or returns. Which pattern is this?"
> **Answer: Supervisor / orchestrator pattern.**

---

### DAY 13 (2 hrs) — Azure AI Foundry Evaluation and Tracing

**What to read:**
- Microsoft Learn: "Evaluate AI model responses with Azure AI Foundry" → https://learn.microsoft.com/training/modules/evaluate-models-azure-ai-foundry/

**Why Evaluate?**
Before deploying AI to production, you must verify quality. The exam tests which metrics you'd use.

**Built-in Evaluation Metrics:**

| Metric | What It Measures | Scale |
|--------|-----------------|-------|
| **Groundedness** | Is the response based on retrieved documents? | 1–5 |
| **Relevance** | Does response address the question? | 1–5 |
| **Coherence** | Is the response logical and well-structured? | 1–5 |
| **Fluency** | Is the language natural? | 1–5 |
| **Similarity** | How close to a reference answer? | 0–1 |
| **F1 Score** | Overlap between generated and reference | 0–1 |
| **Violence/Hate/Sexual** | Content safety scores | 0–7 |

**Tracing — for debugging agents:**
```python
# Enable tracing in AI Foundry
from azure.ai.projects import AIProjectClient
from azure.identity import DefaultAzureCredential

client = AIProjectClient.from_connection_string(
    conn_str=os.getenv("AZURE_PROJECT_CONNECTION_STRING"),
    credential=DefaultAzureCredential()
)

# Enable Application Insights tracing
client.telemetry.enable()  # Auto-instruments all SDK calls

# Now all agent runs, tool calls, LLM calls are traced
# View in AI Foundry portal → Tracing tab
```

**Key exam question type:**
> "A RAG chatbot is giving answers not supported by the source documents. Which evaluation metric helps detect this?"
> **Answer: Groundedness**

---

### DAY 14 (Weekend — 3 hrs) — Week 2 Consolidation and Practice

**Hour 1: Build a complete RAG chatbot (end-to-end lab)**
1. Create an Azure AI Search resource (free tier) in Azure portal
2. Create a simple text file with sample content (product FAQ, etc.)
3. Index it into Azure AI Search
4. Run the `rag_pipeline.py` from Day 10

**Hour 2: Domain 2 Microsoft Learn completion**
- Complete remaining Domain 2 modules:
  https://learn.microsoft.com/training/paths/develop-ai-apps-agents-azure/
  → Sections: "Implement generative AI solutions" and "Build agents"

**Hour 3: Practice test — focus Domain 2**
- Go to: https://open-exam-prep.com/practice/ai-103
- Take practice questions
- Target: 75%+ on generative AI/agents questions

**Domain 2 Cheat Sheet:**
```
RAG = Retrieve docs from search → Augment prompt → Generate answer
Hybrid search = keyword + vector (use semantic ranking on top for best results)
Temperature=0 → deterministic. Temperature=1 → creative.
Few-shot → examples in prompt. Chain-of-thought → step by step reasoning.
Agent tools: FileSearch, CodeInterpreter, BingGrounding, custom functions
Semantic Kernel: Kernel → Plugin → Function → Planner
Groundedness = answer must come from documents (not LLM imagination)
Supervisor pattern = one orchestrator routes to specialist agents
PTU = dedicated compute for high volume
```

---

## 5. WEEK 3 — DOMAINS 3, 4, 5: VISION, NLP, INFORMATION EXTRACTION

**Combined weight: 30–45%**
**Goal: Know which service to use for which problem, and write basic code for each.**

---

### DAY 15 (2 hrs) — Computer Vision: Image Analysis and OCR

**What to read:**
- Microsoft Learn: "Analyze images with Azure AI Vision" → https://learn.microsoft.com/training/modules/analyze-images/
- Microsoft Learn: "Read text with Azure AI Vision" → https://learn.microsoft.com/training/modules/read-text-images-documents-with-azure-ai-vision/

**Azure AI Vision 4.0 — Key Capabilities:**

| Feature | What It Does | API Call |
|---------|-------------|----------|
| Caption | One sentence description of image | `CAPTION` |
| Dense captions | Captions for objects within image | `DENSE_CAPTIONS` |
| Tags | Keywords describing image content | `TAGS` |
| Object detection | Bounding boxes around objects | `OBJECTS` |
| People detection | Detect people in image | `PEOPLE` |
| Smart crop | Suggest best crop region | `SMART_CROPS` |
| OCR (Read) | Extract text from image | `READ` |

```python
# vision_analysis.py
import os
from azure.ai.vision.imageanalysis import ImageAnalysisClient
from azure.ai.vision.imageanalysis.models import VisualFeatures
from azure.core.credentials import AzureKeyCredential
from dotenv import load_dotenv
load_dotenv()

client = ImageAnalysisClient(
    endpoint=os.getenv("VISION_ENDPOINT"),
    credential=AzureKeyCredential(os.getenv("VISION_KEY"))
)

# Analyze an image from URL
result = client.analyze_from_url(
    image_url="https://upload.wikimedia.org/wikipedia/commons/thumb/4/47/PNG_transparency_demonstration_1.png/280px-PNG_transparency_demonstration_1.png",
    visual_features=[
        VisualFeatures.CAPTION,
        VisualFeatures.TAGS,
        VisualFeatures.OBJECTS,
        VisualFeatures.READ  # OCR
    ],
    language="en"
)

# Access results
if result.caption:
    print(f"Caption: {result.caption.text} (confidence: {result.caption.confidence:.2f})")

if result.tags:
    for tag in result.tags.list:
        print(f"Tag: {tag.name} (confidence: {tag.confidence:.2f})")

if result.objects:
    for obj in result.objects.list:
        print(f"Object: {obj.tags[0].name} at {obj.bounding_box}")

# OCR — read text from image
if result.read:
    for block in result.read.blocks:
        for line in block.lines:
            print(f"Text: {line.text}")
```

**OCR vs Document Intelligence — Exam Critical Distinction:**

| Use Case | Service |
|----------|---------|
| Read text from a photo/screenshot | Azure AI Vision (Read/OCR) |
| Extract structured data from a form/invoice/receipt | Document Intelligence |
| Extract text + layout from a scanned document | Document Intelligence (Layout model) |

**Custom Vision:**
- Train your own image classifier or object detector
- Two types:
  - **Classification:** "Is this image a cat or a dog?"
  - **Object Detection:** "Where are the cats in this image?" (with bounding boxes)
- Use when pre-built models don't cover your specific domain

---

### DAY 16 (2 hrs) — Face API and Video Analysis

**What to read:**
- Microsoft Learn: "Detect, analyze, and recognize faces" → https://learn.microsoft.com/training/modules/detect-analyze-recognize-faces/

**Face API — Restricted Access:**
- Face identification (who is this person?) requires Microsoft approval
- Basic face detection (is there a face?) is unrestricted
- Exam context: know what operations are restricted vs open

**Face Detection capabilities:**
```python
# face_detection.py
from azure.cognitiveservices.vision.face import FaceClient
from azure.cognitiveservices.vision.face.models import FaceAttributeType
from msrest.authentication import CognitiveServicesCredentials
import os
from dotenv import load_dotenv
load_dotenv()

face_client = FaceClient(
    os.getenv("FACE_ENDPOINT"),
    CognitiveServicesCredentials(os.getenv("FACE_KEY"))
)

# Detect faces in an image
faces = face_client.face.detect_with_url(
    url="https://example.com/group-photo.jpg",
    return_face_attributes=[
        FaceAttributeType.age,
        FaceAttributeType.gender,
        FaceAttributeType.emotion
    ]
)

for face in faces:
    print(f"Age: {face.face_attributes.age}")
    print(f"Emotion: {face.face_attributes.emotion.happiness}")
    print(f"Location: {face.face_rectangle}")
```

**Content Understanding (New in AI Foundry):**
- New service replacing some older Form Recognizer + Video Indexer scenarios
- Processes: images, video, audio, documents in a unified way
- Used via AI Foundry → Content Understanding
- Exam question: "Extract insights from customer service call recordings and written transcripts in one pipeline" → **Content Understanding**

---

### DAY 17 (2 hrs) — Language Service: NLP and Text Analysis

**What to read:**
- Microsoft Learn: "Analyze text with Azure AI Language" → https://learn.microsoft.com/training/modules/analyze-text-with-text-analytics-service/
- Microsoft Learn: "Build a question answering solution" → https://learn.microsoft.com/training/modules/build-qna-solution-qna-maker/

**Azure AI Language — All Capabilities:**

```python
# language_service_demo.py
import os
from azure.ai.textanalytics import TextAnalyticsClient
from azure.core.credentials import AzureKeyCredential
from dotenv import load_dotenv
load_dotenv()

client = TextAnalyticsClient(
    endpoint=os.getenv("LANGUAGE_ENDPOINT"),
    credential=AzureKeyCredential(os.getenv("LANGUAGE_KEY"))
)

documents = ["Sundar Pichai is the CEO of Google, headquartered in Mountain View, California."]

# 1. Named Entity Recognition (NER)
ner_result = client.recognize_entities(documents)
for doc in ner_result:
    for entity in doc.entities:
        print(f"NER: {entity.text} | Category: {entity.category} | Confidence: {entity.confidence_score:.2f}")
# Output: Sundar Pichai | Person | 0.99
#         Google | Organization | 0.99
#         Mountain View | Location | 0.85

# 2. Sentiment Analysis
sentiment_result = client.analyze_sentiment(["This product is terrible! It broke in one day."])
for doc in sentiment_result:
    print(f"Sentiment: {doc.sentiment}")  # negative
    print(f"Scores: positive={doc.confidence_scores.positive:.2f}, negative={doc.confidence_scores.negative:.2f}")

# 3. Key Phrase Extraction
keyphrases_result = client.extract_key_phrases(["The quick brown fox jumps over the lazy dog on a sunny afternoon."])
for doc in keyphrases_result:
    print(f"Key phrases: {doc.key_phrases}")

# 4. Language Detection
lang_result = client.detect_language(["Bonjour, comment allez-vous?", "Hola, ¿cómo estás?"])
for doc in lang_result:
    print(f"Language: {doc.primary_language.name}")  # French, Spanish

# 5. PII Detection
pii_result = client.recognize_pii_entities(["My SSN is 859-98-0987 and my email is john@example.com"])
for doc in pii_result:
    print(f"Redacted: {doc.redacted_text}")  # My SSN is *** and my email is ***
    for entity in doc.entities:
        print(f"PII: {entity.text} | Category: {entity.category}")
```

**Conversational Language Understanding (CLU):**
- Build custom intent classification and entity extraction
- Example: "Book me a flight to Paris next Tuesday" → Intent: BookFlight, Entity: Paris, next Tuesday
- Replaces older LUIS service

**Question Answering:**
- Upload documents/FAQ → creates a knowledge base
- Ask questions → returns best answer with confidence score
- Use case: customer service bots, FAQ chatbots

**Key exam distinction:**
| Scenario | Service |
|----------|---------|
| Classify text into your own categories | Custom Text Classification |
| Extract named entities from your domain | Custom NER |
| Understand user intent in conversation | CLU |
| Answer questions from a FAQ document | Question Answering |
| Detect PII and redact it | PII Entity Recognition |
| Summarize a long document | Extractive/Abstractive Summarization |

---

### DAY 18 (2 hrs) — Speech Services

**What to read:**
- Microsoft Learn: "Transcribe speech input with Azure AI Speech" → https://learn.microsoft.com/training/modules/transcribe-speech-input-text/
- Microsoft Learn: "Synthesize speech output with Azure AI Speech" → https://learn.microsoft.com/training/modules/synthesize-speech-azure-ai-speech/

**Azure AI Speech — Four Core Capabilities:**

| Service | Direction | What It Does |
|---------|-----------|-------------|
| **Speech-to-Text (STT)** | Audio → Text | Transcription |
| **Text-to-Speech (TTS)** | Text → Audio | Synthesize voice |
| **Speech Translation** | Audio → Text (different language) | Real-time translation |
| **Speaker Recognition** | Audio → Identity | Who is speaking? |

```python
# speech_demo.py
import os
import azure.cognitiveservices.speech as speechsdk
from dotenv import load_dotenv
load_dotenv()

speech_config = speechsdk.SpeechConfig(
    subscription=os.getenv("SPEECH_KEY"),
    region=os.getenv("SPEECH_REGION")
)

# 1. Speech-to-Text (from microphone)
def transcribe_from_mic():
    audio_config = speechsdk.AudioConfig(use_default_microphone=True)
    recognizer = speechsdk.SpeechRecognizer(speech_config=speech_config, audio_config=audio_config)
    
    print("Listening... speak now")
    result = recognizer.recognize_once()
    
    if result.reason == speechsdk.ResultReason.RecognizedSpeech:
        print(f"Recognized: {result.text}")
    elif result.reason == speechsdk.ResultReason.NoMatch:
        print("No speech could be recognized")

# 2. Text-to-Speech
def synthesize_speech(text: str, output_file: str = "output.wav"):
    speech_config.speech_synthesis_voice_name = "en-US-AriaNeural"  # Natural AI voice
    audio_config = speechsdk.AudioConfig(filename=output_file)
    
    synthesizer = speechsdk.SpeechSynthesizer(speech_config=speech_config, audio_config=audio_config)
    result = synthesizer.speak_text_async(text).get()
    
    if result.reason == speechsdk.ResultReason.SynthesizingAudioCompleted:
        print(f"Saved to {output_file}")

# 3. Speech Translation (Hindi audio → English text)
def translate_speech():
    translation_config = speechsdk.translation.SpeechTranslationConfig(
        subscription=os.getenv("SPEECH_KEY"),
        region=os.getenv("SPEECH_REGION")
    )
    translation_config.speech_recognition_language = "hi-IN"  # Source: Hindi
    translation_config.add_target_language("en")              # Target: English
    
    recognizer = speechsdk.translation.TranslationRecognizer(translation_config=translation_config)
    result = recognizer.recognize_once()
    
    if result.reason == speechsdk.ResultReason.TranslatedSpeech:
        print(f"Original (Hindi): {result.text}")
        print(f"Translation (English): {result.translations['en']}")
```

---

### DAY 19 (2 hrs) — Document Intelligence

**What to read:**
- Microsoft Learn: "Extract data from forms with Document Intelligence" → https://learn.microsoft.com/training/modules/work-form-recognizer/

**Azure AI Document Intelligence (formerly Form Recognizer):**

**Pre-built models (know all of these for the exam):**

| Model | What It Extracts |
|-------|-----------------|
| `prebuilt-invoice` | Vendor, invoice number, line items, totals |
| `prebuilt-receipt` | Merchant, items, totals, date |
| `prebuilt-idDocument` | Name, DOB, ID number from passports/licenses |
| `prebuilt-tax.us.w2` | US W2 tax form fields |
| `prebuilt-businessCard` | Name, email, phone from business cards |
| `prebuilt-layout` | Text, tables, and their layout/position |
| `prebuilt-read` | Just the text (like OCR) |

**Custom models:**
- **Template model:** For fixed-format forms (same layout every time)
- **Neural model:** For variable-layout forms (different vendors, different layouts)
- **Composed model:** Multiple custom models behind one endpoint

```python
# document_intelligence_demo.py
import os
from azure.ai.formrecognizer import DocumentAnalysisClient
from azure.core.credentials import AzureKeyCredential
from dotenv import load_dotenv
load_dotenv()

client = DocumentAnalysisClient(
    endpoint=os.getenv("DOCUMENT_INTELLIGENCE_ENDPOINT"),
    credential=AzureKeyCredential(os.getenv("DOCUMENT_INTELLIGENCE_KEY"))
)

# Analyze an invoice
with open("sample_invoice.pdf", "rb") as f:
    poller = client.begin_analyze_document(
        model_id="prebuilt-invoice",
        document=f
    )

result = poller.result()

for invoice in result.documents:
    # Access specific fields
    vendor = invoice.fields.get("VendorName")
    invoice_id = invoice.fields.get("InvoiceId")
    total = invoice.fields.get("InvoiceTotal")
    
    if vendor:
        print(f"Vendor: {vendor.value} (confidence: {vendor.confidence:.2f})")
    if invoice_id:
        print(f"Invoice ID: {invoice_id.value}")
    if total:
        print(f"Total: {total.value}")
    
    # Access line items
    items = invoice.fields.get("Items")
    if items:
        for item in items.value:
            desc = item.value.get("Description")
            amount = item.value.get("Amount")
            if desc and amount:
                print(f"  Item: {desc.value} = {amount.value}")
```

---

### DAY 20 (2 hrs) — Azure AI Search Deep Dive

**What to read:**
- Microsoft Learn: "Create an Azure AI Search solution" → https://learn.microsoft.com/training/modules/create-azure-cognitive-search-solution/
- Microsoft Learn: "Enrich a search index using Azure Machine Learning custom skills" → https://learn.microsoft.com/training/modules/enrich-search-index-using-custom-skills/

**Azure AI Search Architecture:**

```
Data Sources → Indexers → Skillsets → Index → Query
```

**Components:**

**Data Source:** Where your content lives (Azure Blob, SQL, Cosmos DB, SharePoint)

**Indexer:** Pulls content from data source and feeds it into the index. Can run on a schedule.

**Skillset:** AI enrichment pipeline. Applied during indexing.
- Built-in cognitive skills: OCR, entity extraction, key phrase extraction, translation, image analysis
- Custom skills: Your own Azure Function or ML model endpoint

**Index:** The searchable store. Contains fields (text, numeric, geo, vectors).

**Index field attributes:**
| Attribute | Meaning |
|-----------|---------|
| `searchable` | Full-text indexed, can be queried |
| `filterable` | Can use in filter expressions (`$filter`) |
| `sortable` | Can sort results by this field |
| `facetable` | Can generate facet counts (like category counts in e-commerce) |
| `retrievable` | Returned in search results |
| `key` | Unique identifier field |

**Knowledge Store:**
- Side-output of a skillset
- Saves enriched content to Azure Storage (blobs or tables)
- Use for: analysis in Power BI, training data, audit trail

**Key exam question type:**
> "A company wants to index their SharePoint document library so employees can search it using natural language. The documents contain images with text. Which Azure AI Search feature extracts text from the images during indexing?"
> **Answer: A skillset with the OCR cognitive skill (built-in).**

---

### DAY 21 (Weekend — 3 hrs) — Week 3 Consolidation

**Hour 1: Service decision matrix — practice**

For each scenario below, write the service you'd use:
1. Extract invoice totals from PDFs → `Document Intelligence (prebuilt-invoice)`
2. Detect customer sentiment in chat logs → `Azure AI Language (Sentiment Analysis)`
3. Find all mentions of people and companies in news articles → `Azure AI Language (NER)`
4. A user says "Book a table for 2 at an Italian restaurant" — understand intent → `CLU`
5. Search company documents semantically + exact keyword → `Azure AI Search (hybrid)`
6. Transcribe customer service call recordings → `Azure AI Speech (STT)`
7. Detect if a product photo contains a defect (custom) → `Custom Vision`
8. Extract all text + tables from scanned PDF preserving layout → `Document Intelligence (layout model)`
9. Answer questions from an employee handbook → `Question Answering`
10. PII in customer emails needs to be redacted → `PII Entity Recognition`

**Hour 2: Microsoft Learn — complete Domain 3, 4, 5 modules**
Path: https://learn.microsoft.com/training/paths/develop-ai-apps-agents-azure/
→ Complete the Vision, Language, and Information Extraction sections

**Hour 3: Hands-on labs**
- Create an Azure AI Language resource (free tier) in portal.azure.com
- Run the `language_service_demo.py` code from Day 17
- Try all 5 operations: NER, Sentiment, Key phrases, Language detection, PII

---

## 6. WEEK 4 — INTEGRATION, PRACTICE TESTS & EXAM READINESS

**Goal: Move from knowledge to exam performance. Find and fix gaps. Build test stamina.**

---

### DAY 22 (2 hrs) — End-to-End Integration Scenarios

The exam presents complex scenarios spanning multiple services. Practice thinking in solutions.

**Scenario 1: Intelligent Document Processing Pipeline**
```
Customer uploads invoices (PDF) to Azure Blob Storage
→ Blob trigger fires Azure Function
→ Document Intelligence extracts fields
→ Results stored in Azure Cosmos DB
→ Azure AI Language analyzes vendor names (NER)
→ Power BI dashboard shows spending by vendor
```

**Scenario 2: Enterprise Knowledge Assistant**
```
Company documents in SharePoint
→ Azure AI Search indexer (with OCR skillset for scanned docs)
→ Vector index built with text-embedding-3-small
→ RAG chatbot: user asks question
→ Hybrid search finds relevant chunks
→ GPT-4o generates grounded answer
→ Groundedness evaluation before showing to user
```

**Scenario 3: Multi-language Customer Support**
```
Customer sends voice message (Hindi)
→ Azure AI Speech: STT (Hindi → text)
→ Azure AI Language: Translation (Hindi → English)
→ Azure AI Language: Sentiment Analysis
→ CLU: Intent classification (complaint/inquiry/praise)
→ If complaint: Route to human agent
→ Otherwise: AI agent handles using RAG on FAQ knowledge base
```

**For each scenario, know:**
- Which Azure services are involved
- What connects them
- What authentication model applies
- What monitoring/logging you'd enable

---

### DAY 23 (2 hrs) — Common Exam Traps

**Trap 1: API version matters**
- The exam uses specific API versions. Know that `2024-12-01-preview` is current for Azure OpenAI.
- Some features only exist in certain versions.

**Trap 2: Managed Identity ≠ automatically configured**
- You must assign the RBAC role AND configure the service to use managed identity.
- Both steps required — missing one = 403 error.

**Trap 3: Azure OpenAI "On Your Data" shortcut**
```python
# This is a SHORTCUT for RAG built into Azure OpenAI API
# No separate search code needed — Azure OpenAI calls search internally
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "What is our refund policy?"}],
    extra_body={
        "data_sources": [{
            "type": "azure_search",
            "parameters": {
                "endpoint": os.getenv("AZURE_AI_SEARCH_ENDPOINT"),
                "index_name": os.getenv("AZURE_AI_SEARCH_INDEX"),
                "authentication": {
                    "type": "api_key",
                    "key": os.getenv("AZURE_AI_SEARCH_KEY")
                }
            }
        }]
    }
)
```
> **When to use this vs manual RAG:** This shortcut is fine for basic use. Manual RAG gives more control (reranking, filtering, hybrid search tuning).

**Trap 4: Semantic Kernel planner vs manual function calling**
- Planner: AI decides which functions to call (more autonomous, less predictable)
- Manual function calling: You define exactly when tools are called (more control)
- Exam: "deterministic tool selection" → manual. "autonomous task completion" → planner.

**Trap 5: Document Intelligence vs Azure AI Vision OCR**
- Vision Read: Text extraction from natural images, quick jobs
- Document Intelligence Read model: Better for documents, preserves structure
- Document Intelligence Layout: Best for tables, forms, complex structure
- Rule of thumb: If it's a document (not a random photo) → Document Intelligence

**Trap 6: Content Safety vs Content Filters**
- **Content Safety:** Standalone service, call explicitly, returns category scores
- **Content Filters:** Built into Azure OpenAI deployments, automatic, blocks/flags before response

---

### DAY 24 (2 hrs) — Full Practice Test 1

**Instructions:**
1. Go to: https://mscertquiz.com/certifications/ai-103 (40 questions, free)
2. Set a 90-minute timer
3. Simulate real exam conditions: no notes, no internet search during the test
4. After completing, review every single wrong answer
5. For each wrong answer, go to the relevant Microsoft Learn page and read it

**Track your score by domain:**
```
Domain 1 (Plan & Manage):     ___/XX  = ___%
Domain 2 (GenAI & Agents):    ___/XX  = ___%
Domain 3 (Vision):            ___/XX  = ___%
Domain 4 (NLP):               ___/XX  = ___%
Domain 5 (Info Extraction):   ___/XX  = ___%
Total:                        ___/40  = ___%
```

**Target for today: 65%+**
If below 65% in any domain, add 1 extra study hour for that domain tomorrow.

---

### DAY 25 (2 hrs) — Weak Area Targeted Review

Based on your Practice Test 1 results, focus today on your two weakest domains.

**Additional resources by domain:**

**Domain 1 (Plan & Manage):**
- https://learn.microsoft.com/training/modules/plan-manage-azure-ai-foundry/
- Key topics: Hub vs Project, RBAC roles, Managed Identity, Private Endpoint

**Domain 2 (GenAI & Agents):**
- https://learn.microsoft.com/training/modules/build-language-solution-azure-openai/
- https://learn.microsoft.com/training/modules/use-own-data-azure-openai/
- Key topics: RAG architecture, Agent tools, Semantic Kernel plugins

**Domain 3 (Vision):**
- https://learn.microsoft.com/training/modules/analyze-images/
- Key topics: VisualFeatures enum, OCR vs Document Intelligence, Custom Vision

**Domain 4 (NLP):**
- https://learn.microsoft.com/training/modules/analyze-text-with-text-analytics-service/
- Key topics: NER categories, CLU vs Question Answering, STT vs Translation

**Domain 5 (Info Extraction):**
- https://learn.microsoft.com/training/modules/work-form-recognizer/
- https://learn.microsoft.com/training/modules/create-azure-cognitive-search-solution/
- Key topics: Prebuilt models, index attributes, skillsets, Knowledge Store

---

### DAY 26 (Weekend — 3 hrs) — Full Practice Test 2

**Instructions:**
1. Use: https://open-exam-prep.com/practice/ai-103
2. Set timer: 90 minutes, strict
3. After: analyze wrong answers as before

**This time, also practice:**
- **Flagging questions:** In real exam, flag uncertain questions and return to them
- **Time management:** Average 2–3 minutes per question. If a question takes 5+ minutes, flag and move on.

**Target for today: 72%+**

---

### DAY 27 (Weekend — 3 hrs) — Final Consolidation

**Hour 1: The Master Cheat Sheet — Write It Yourself**

Write (don't type) a 1-page summary for each domain covering:
- 3 most important services
- 2 tricky decision points
- 1 code pattern to remember

The act of writing it yourself is more valuable than reading a pre-made one.

**Hour 2: Scenario Gauntlet — 20 Questions**

For each scenario, pick the service(s):
1. Extract text from a photo of a handwritten note → `Azure AI Vision (Read/OCR)`
2. A chatbot that answers from a 500-page policy document → `RAG with Azure AI Search + Azure OpenAI`
3. Route customer inquiries by topic (billing/tech/returns) → `CLU`
4. Translate customer emails from Japanese to English at scale → `Azure AI Translator`
5. Detect if a new employee's selfie matches their ID photo → `Face API (verification)`
6. Run Azure AI Language on-premises in a hospital → `Language container`
7. Index PDFs in SharePoint + enable natural language search → `AI Search indexer + Azure OpenAI embedding`
8. Extract fields from 10 different vendor invoice layouts → `Document Intelligence (neural custom model)`
9. User needs voice interface for a chatbot → `Speech STT → GPT-4o → Speech TTS`
10. Ensure chatbot never reveals competitors' names → `Content filters (custom blocklist)`
11. Track which documents the chatbot cites for each answer → `Citations in Azure OpenAI On Your Data`
12. Agent that can search the web for current information → `BingGroundingTool`
13. Block content with severity 3+ for violence → `Content Safety + threshold configuration`
14. Multiple AI agents that debate to improve answer quality → `Multi-agent debate pattern`
15. Cache repeated system prompts to reduce cost → `Azure OpenAI prompt caching`
16. Need guaranteed response time, high volume of calls → `Provisioned Throughput (PTU)`
17. Build an image search feature for e-commerce catalog → `Azure AI Vision embeddings + AI Search vector index`
18. Audit all API calls to Azure OpenAI for compliance → `Diagnostic logs → Azure Monitor`
19. AI that executes Python code to analyze uploaded data files → `CodeInterpreterTool in AI Agent`
20. Five AI agents share the same Azure OpenAI resource → `Connections at Hub level in AI Foundry`

**Hour 3: Book your exam**
- Go to: https://learn.microsoft.com/certifications/exams/ai-103
- Click "Schedule exam" → Pearson VUE
- Choose online proctored exam
- Pick a date 3–5 days from now (gives buffer for final review)

---

### DAY 28 (2 hrs) — Final Review and Exam Eve Preparation

**What to do:**

**Hour 1: Speed review — your own cheat sheets from Day 27**
- Run through your written notes
- Do NOT try to learn new topics
- Focus on things you're least confident about

**Hour 2: Light practice (15–20 questions only)**
- Take 15–20 questions from any practice test
- Stop at 70 minutes regardless
- Target: 75%+

**Final mental checklist:**
```
☐ I can explain Hub vs Project in AI Foundry
☐ I know the 5 RBAC roles and what each can do
☐ I can write a RAG pipeline from memory (conceptually)
☐ I know keyword vs vector vs hybrid search differences
☐ I can name all prebuilt Document Intelligence models
☐ I know when to use CLU vs Question Answering
☐ I know the 6 Responsible AI principles
☐ I understand agent tools: FileSearch, CodeInterpreter, BingGrounding
☐ I know temperature=0 → deterministic
☐ I know PTU vs standard deployment
```

---

## 7. PYTHON QUICK REFERENCE

### All Services — Authentication Pattern (Use This Every Time)

```python
# auth.py — reuse across all files
import os
from azure.core.credentials import AzureKeyCredential
from azure.identity import DefaultAzureCredential
from dotenv import load_dotenv
load_dotenv()

# For development (uses `az login` credentials)
dev_credential = DefaultAzureCredential()

# For key-based auth (simpler, for labs)
def get_key_credential(env_var: str) -> AzureKeyCredential:
    return AzureKeyCredential(os.getenv(env_var))
```

### Service Client Initialization Patterns

```python
# All service clients follow the same pattern:
# Client(endpoint, credential)

from azure.ai.textanalytics import TextAnalyticsClient
from azure.ai.vision.imageanalysis import ImageAnalysisClient
from azure.ai.formrecognizer import DocumentAnalysisClient
from azure.search.documents import SearchClient
from azure.ai.projects import AIProjectClient
from openai import AzureOpenAI

# Language
lang_client = TextAnalyticsClient(os.getenv("LANGUAGE_ENDPOINT"), AzureKeyCredential(os.getenv("LANGUAGE_KEY")))

# Vision
vision_client = ImageAnalysisClient(os.getenv("VISION_ENDPOINT"), AzureKeyCredential(os.getenv("VISION_KEY")))

# Document Intelligence
doc_client = DocumentAnalysisClient(os.getenv("DOCUMENT_INTELLIGENCE_ENDPOINT"), AzureKeyCredential(os.getenv("DOCUMENT_INTELLIGENCE_KEY")))

# AI Search
search_client = SearchClient(os.getenv("AZURE_AI_SEARCH_ENDPOINT"), os.getenv("AZURE_AI_SEARCH_INDEX"), AzureKeyCredential(os.getenv("AZURE_AI_SEARCH_KEY")))

# Azure OpenAI
openai_client = AzureOpenAI(azure_endpoint=os.getenv("AZURE_OPENAI_ENDPOINT"), api_key=os.getenv("AZURE_OPENAI_KEY"), api_version="2024-12-01-preview")

# AI Projects (AI Foundry)
project_client = AIProjectClient.from_connection_string(os.getenv("AZURE_PROJECT_CONNECTION_STRING"), DefaultAzureCredential())
```

### Error Handling Template

```python
from azure.core.exceptions import HttpResponseError, ResourceNotFoundError

try:
    result = client.some_operation(...)
except HttpResponseError as e:
    if e.status_code == 401:
        print("Authentication failed — check your key or managed identity role assignment")
    elif e.status_code == 403:
        print("Authorization failed — check RBAC role assignment")
    elif e.status_code == 429:
        print("Rate limit hit — add retry logic or switch to PTU")
        time.sleep(e.retry_after)  # Wait suggested time
    elif e.status_code == 404:
        print("Resource not found — check endpoint URL")
    else:
        print(f"HTTP error {e.status_code}: {e.message}")
except Exception as e:
    print(f"Unexpected error: {str(e)}")
```

### Retry Logic (Important for Rate Limits)

```python
import time
import random
from openai import RateLimitError

def call_with_retry(fn, max_retries=3, base_delay=1):
    """Exponential backoff retry for Azure OpenAI rate limits."""
    for attempt in range(max_retries):
        try:
            return fn()
        except RateLimitError:
            if attempt == max_retries - 1:
                raise
            delay = base_delay * (2 ** attempt) + random.uniform(0, 1)
            print(f"Rate limited. Retrying in {delay:.1f}s...")
            time.sleep(delay)
```

---

## 8. EXAM STRATEGY & DAY-OF CHECKLIST

### Before Exam Day

**3 days before:**
- Complete system check: https://home.pearsonvue.com/op/pearsonvue-testing-experience-overview-tech-specs
- Download Pearson VUE secure browser if taking online
- Practice with the browser lockdown tool — make sure no extensions block it

**Night before:**
- Do NOT study new material
- Review your written cheat sheets (30 minutes max)
- Prepare your workspace: clear desk, remove second monitor or cover it, good lighting
- Get 8 hours sleep — more valuable than last-minute cramming
- Eat a proper meal the day of

### During the Exam — Tactics

**Time Management:**
- 120 minutes ÷ 50 questions = ~2.4 minutes per question
- Set internal checkpoints: at 30 min, should be done with ~12 questions
- Flag and skip questions taking >3 minutes — return later
- Reserve last 15 minutes for flagged questions and review

**Question Approach:**
1. Read the last sentence first (the actual question, not the scenario)
2. Identify the constraint (cost-sensitive, compliance requirement, high volume, etc.)
3. Eliminate obviously wrong answers
4. Between two similar answers: look for the constraint that distinguishes them

**Microsoft Learn Access:**
- You CAN open Microsoft Learn docs during the exam
- Only use it for specific lookups (API names, feature names)
- Do NOT use it for conceptual learning — too slow
- Have these pages mentally bookmarked: AI Foundry overview, Azure OpenAI models, AI Search query types

**Flag Strategy:**
- Flag: You know it but need to double-check
- Flag: Scenario too complex, need to return with fresh eyes
- Skip outright: You have zero idea (answer anyway, then flag — no penalty for wrong answers)

### Day-of Checklist

```
ENVIRONMENT
☐ Closed all background apps (Teams, Slack, browser, antivirus notifications)
☐ Phone in another room or face-down, silenced
☐ Clear desk — only water bottle allowed
☐ Good lighting, no one in the room
☐ Stable internet (use ethernet cable if possible)
☐ Government-issued ID matching your registered name

TECHNICAL
☐ Pearson VUE secure browser installed and tested
☐ Webcam working and clear
☐ Microphone working
☐ External monitors disconnected or turned off

MINDSET
☐ Remember: 700/1000 to pass — you do not need to get everything right
☐ You can flag and skip — do not get stuck
☐ No negative marking — always make a guess before flagging
☐ Your background in agentic AI gives you real advantage on Domain 2
```

---

## 9. MASTER RESOURCE LIST

### Official Microsoft Sources (Always Current)

| Resource | URL |
|----------|-----|
| AI-103 Official Study Guide | https://learn.microsoft.com/credentials/certifications/resources/study-guides/ai-103 |
| Official Microsoft Learn Path | https://learn.microsoft.com/training/paths/develop-ai-apps-agents-azure/ |
| AI-103 Certification Page | https://learn.microsoft.com/credentials/certifications/azure-ai-apps-and-agents-developer/ |
| Azure AI Foundry Portal | https://ai.azure.com |
| Azure AI Foundry Docs | https://learn.microsoft.com/azure/ai-foundry/ |
| Azure OpenAI Docs | https://learn.microsoft.com/azure/ai-services/openai/ |
| Azure AI Search Docs | https://learn.microsoft.com/azure/search/ |
| Azure AI Language Docs | https://learn.microsoft.com/azure/ai-services/language-service/ |
| Document Intelligence Docs | https://learn.microsoft.com/azure/ai-services/document-intelligence/ |
| Azure AI Vision Docs | https://learn.microsoft.com/azure/ai-services/computer-vision/ |
| Azure AI Speech Docs | https://learn.microsoft.com/azure/ai-services/speech-service/ |
| Semantic Kernel Docs | https://learn.microsoft.com/semantic-kernel/overview/ |
| AI Agent Service Docs | https://learn.microsoft.com/azure/ai-services/agents/ |

### Free Practice Tests

| Resource | Questions | Notes |
|----------|-----------|-------|
| https://mscertquiz.com/certifications/ai-103 | 40 | Aligned to April 2026 objectives |
| https://open-exam-prep.com/practice/ai-103 | Free sample set | Good for Domain 2 |
| https://mscertquiz.com/blog/ai-103-study-guide | N/A | Best free study guide |

### Udemy Courses (Paid, Recommended)

| Course | Best For |
|--------|----------|
| AI-103: Azure AI App & Agent Developer — Complete Course | Full course with hands-on code walkthroughs |
| AI-103: Azure AI App & Agent Developer Practice Exams 2026 | 600 practice questions, 6 full-length tests |
| AI-103: Azure AI App and Agent Developer — 1000+ Questions | Largest question bank if you want more practice |

> **Note:** For Udemy, always filter by "Updated April 2026 or later" to ensure content matches current exam objectives. Avoid any course last updated before April 2026.

### Study Community

| Community | URL |
|-----------|-----|
| r/AzureCertifications | https://reddit.com/r/AzureCertifications |
| Microsoft Q&A — AI-103 | https://learn.microsoft.com/answers/topics/azure-ai-foundry.html |
| Microsoft Tech Community | https://techcommunity.microsoft.com |

---

## APPENDIX: 4-WEEK CALENDAR AT A GLANCE

```
WEEK 1: FOUNDATION & DOMAIN 1
Mon D1  Azure AI Foundry Architecture (Hub/Project/Connections)
Tue D2  Authentication & Security (Managed Identity, RBAC, Private Endpoints)
Wed D3  Responsible AI & Content Safety
Thu D4  Model Selection & Cost Management
Fri D5  Container Deployments & Monitoring
Sat D6  Domain 1 Deep Practice + Microsoft Learn modules
Sun D7  AI Foundry Hands-on Lab

WEEK 2: GENERATIVE AI & AGENTS (DOMAIN 2)
Mon D8  Azure OpenAI Deep Dive (Chat API, Embeddings, Parameters)
Tue D9  Prompt Engineering (Zero-shot, Few-shot, CoT, System prompts)
Wed D10 RAG Pipelines (Hybrid search, vector indexing, groundedness)
Thu D11 Azure AI Agent Service (Threads, Runs, Tools, Function calling)
Fri D12 Semantic Kernel & Multi-Agent Patterns
Sat D13 AI Foundry Evaluation & Tracing
Sun D14 Week 2 Consolidation + Full RAG Lab + Practice Test

WEEK 3: VISION, NLP, INFORMATION EXTRACTION (DOMAINS 3-5)
Mon D15 Computer Vision (Image Analysis, OCR)
Tue D16 Face API & Content Understanding
Wed D17 Language Service (NER, Sentiment, CLU, Question Answering)
Thu D18 Speech Services (STT, TTS, Translation, Speaker Recognition)
Fri D19 Document Intelligence (Prebuilt models, Custom models)
Sat D20 Azure AI Search (Indexers, Skillsets, Knowledge Store)
Sun D21 Week 3 Consolidation + Hands-on Language Lab

WEEK 4: INTEGRATION & EXAM READINESS
Mon D22 End-to-End Integration Scenarios
Tue D23 Common Exam Traps & Edge Cases
Wed D24 Full Practice Test 1 + Wrong Answer Review
Thu D25 Weak Area Targeted Review
Fri D26 Full Practice Test 2 (timed, strict)
Sat D27 Master Cheat Sheet + Scenario Gauntlet + BOOK EXAM
Sun D28 Final Review (light) + Exam Eve Prep
```

---

*Document version: July 2026 | Aligned to AI-103 official objectives dated April 16, 2026*
*Always verify with official study guide before exam: https://learn.microsoft.com/credentials/certifications/resources/study-guides/ai-103*
