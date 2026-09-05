# AI-103 — Setup and Resources

> ### ⚠️ THIS DOCUMENT NO LONGER TEACHES CONTENT
>
> An earlier version of this file contained a full 28-day syllabus. **That content is withdrawn.** It was written before the April 2026 objectives were properly checked, and it taught:
>
> - Semantic Kernel as the current agent SDK — superseded by **Microsoft Agent Framework 1.0**
> - Image Analysis, OCR, Custom Vision, and Face API as the core of Domain 3 — the objectives centre on **image and video generation, editing, multimodal understanding, and visual safety**
> - The Language service SDK as the core of Domain 4 — the objectives lead with **generative prompting and Foundry Tools**
>
> Following it would send you back into exactly the legacy material the Master Guide was rebuilt to remove.
>
> **Your three documents now have one job each:**
>
> | Document | Job |
> |----------|-----|
> | **`AI-103_Master_Guide`** (.md / .pdf) | **All content.** The single knowledge source. |
> | **`ai103_execution_calendar.md`** | **When** to study what, mapped to dates. |
> | **This file** | Environment setup and the validated resource list. Nothing else. |

---

## 1. Day 0 — Environment Setup

Complete before your first study session. Budget ~2.5 hours.

### 1.1 Lead-time items first

```
☐ AZURE OPENAI ACCESS REQUEST   ← 1–3 DAY LEAD TIME
    https://aka.ms/oai/access
    Blocks every generative lab. Submit before anything else.

☐ GPT IMAGE MODEL ACCESS         ← separate approval
    Image generation models are access-gated.
    Required for Domain 3 labs (§3.2–3.3 of the Master Guide).
    Apply at the same time as OpenAI access.

☐ AZURE FREE ACCOUNT
    https://azure.microsoft.com/free
    $200 credit / 30 days. Card required, not charged.
```

### 1.2 Foundry project

1. Go to **https://ai.azure.com**
2. Management center → **+ New hub** → region with model availability (East US, Sweden Central)
3. Inside the hub → **+ New project** → name it `ai103-lab`
4. Project → **Overview** → copy the *project connection string* into your `.env`

### 1.3 Python environment

```bash
# Python 3.11+ from python.org, VS Code + Python/Pylance/Azure Tools extensions

mkdir ai103-labs && cd ai103-labs
python -m venv venv
source venv/bin/activate          # Windows: venv\Scripts\activate

# Core SDKs
pip install openai azure-identity python-dotenv
pip install azure-ai-projects azure-ai-inference azure-ai-evaluation
pip install azure-ai-contentsafety
pip install agent-framework                    # Microsoft Agent Framework 1.0

# Domain 3-5 SDKs
pip install azure-ai-vision-imageanalysis
pip install azure-ai-textanalytics
pip install azure-ai-formrecognizer
pip install azure-search-documents
pip install azure-cognitiveservices-speech
pip install requests pillow                    # image/video lab helpers
```

### 1.4 `.env` template

```
# Foundry
AZURE_PROJECT_CONNECTION_STRING=
AZURE_AI_PROJECT_ENDPOINT=

# Azure OpenAI
AZURE_OPENAI_ENDPOINT=
AZURE_OPENAI_KEY=
AZURE_OPENAI_DEPLOYMENT=gpt-4o
AZURE_OPENAI_EMBEDDING_DEPLOYMENT=text-embedding-3-small
AZURE_OPENAI_IMAGE_DEPLOYMENT=gpt-image-2

# AI Search
AZURE_AI_SEARCH_ENDPOINT=
AZURE_AI_SEARCH_KEY=
AZURE_AI_SEARCH_INDEX=ai103-index

# Language / Vision / Document Intelligence / Speech / Content Safety
LANGUAGE_ENDPOINT=
LANGUAGE_KEY=
VISION_ENDPOINT=
VISION_KEY=
DOCUMENT_INTELLIGENCE_ENDPOINT=
DOCUMENT_INTELLIGENCE_KEY=
SPEECH_KEY=
SPEECH_REGION=eastus
CONTENT_SAFETY_ENDPOINT=
CONTENT_SAFETY_KEY=
```

### 1.5 Provision every resource on day 0

Create all of these in the Azure portal now, free tier, and fill the `.env` completely. At three study hours a day you cannot afford to lose twenty minutes of a session to portal navigation.

```
☐ Azure OpenAI          ☐ Azure AI Search        ☐ Azure AI Language
☐ Azure AI Vision       ☐ Document Intelligence  ☐ Azure AI Speech
☐ Content Safety        ☐ Content Understanding (Foundry Tools resource)
```

### 1.6 Azure CLI

```bash
az login
az account show
```

Needed for `DefaultAzureCredential` and `AzureCliCredential` to work locally.

---

## 2. Validated Resource List

> Every entry below has been checked against the current exam scope. Resources marked ⛔ are listed specifically so you avoid them.

### 2.1 Official — highest trust

| Resource | URL |
|----------|-----|
| **AI-103 official study guide** — the authority | `learn.microsoft.com/credentials/certifications/resources/study-guides/ai-103` |
| Certification page | `learn.microsoft.com/credentials/certifications/azure-ai-apps-and-agents-developer/` |
| **MS Learn YouTube playlist** — 26 official videos | `youtube.com/playlist?list=PLWGIg_TYLeEQ` |
| Microsoft Foundry portal | `ai.azure.com` |
| Foundry documentation | `learn.microsoft.com/azure/foundry/` |
| Image generation how-to | `learn.microsoft.com/azure/foundry/openai/how-to/dall-e` |
| Sora 2 video generation | `learn.microsoft.com/azure/foundry/openai/concepts/video-generation` |
| Agent Service tools | `learn.microsoft.com/azure/foundry/agents/` |
| Microsoft Agent Framework | `github.com/microsoft/agent-framework` |
| Content Understanding | `learn.microsoft.com/azure/ai-services/content-understanding/` |
| Azure AI Search | `learn.microsoft.com/azure/search/` |

### 2.2 Video course

**Alan Rodrigues — AI-103 sections only.** The AI-102 sections were unpublished at the end of August 2026.

| Watch | Skip |
|-------|------|
| Foundation Models, Tools, Developer Workflow | LangChain / LangGraph / MCP section — not exam-weighted |
| Prompts to Agents, RAG, Agentic (skim at 2× if strong) | Any remaining AI-102 material |
| Production-Ready Memory, Workflows, Monitoring, Safety | |
| Practice Section | |

⚠️ **His Domain 3 and 4 sections predate the scope correction in this guide.** Watch them for framing, but treat Master Guide §3 and §4 as authoritative where they differ. In particular, no third-party course covers image/video generation to the depth the objectives require.

### 2.3 Question banks

| Source | Use |
|--------|-----|
| **Microsoft Practice Assessment** | *Check availability by 10 Sep.* May not exist yet — practice assessments typically appear after an exam leaves beta. |
| **Scott Duffy** — 4 timed tests | Timed simulation and score calibration |
| **Trevoir Williams** — 1,500 questions | Volume drilling. Unrated at time of purchase — treat divergence from Duffy's scores as noise in Trevoir's bank, not signal. |
| **Master Guide §§0–6** | 45 worked scenarios with full wrong-answer analysis |

⚠️ **Validate any question bank against the current scope.** Banks assembled early in AI-103's life may contain AI-102-derived questions on Custom Vision and Face API, and are unlikely to test image/video generation at its true weight. A bank that never mentions inpainting or Sora is testing the wrong exam.

### 2.4 ⛔ Do not use

| Source | Why |
|--------|-----|
| Any AI-102 material | Retired 30 June 2026. Different domain structure. |
| Semantic Kernel tutorials as the agent path | Superseded by Microsoft Agent Framework 1.0 |
| DALL-E 3 image tutorials | Model retired 4 March 2026 |
| LUIS documentation | Replaced by CLU |
| Face emotion/age/gender guides | Attributes retired for Responsible AI |
| The withdrawn syllabus in this file's earlier version | See the banner above |

---

## 3. Pre-Exam Checklist

```
THREE DAYS BEFORE
☐ Pearson VUE secure browser installed and tested
☐ System check passed
☐ Government photo ID matches registration name

DAY BEFORE
☐ Master Guide §6.2 (trap list) and §6.3 (answer key) — 45 min, then stop
☐ Desk cleared, second monitor disconnected
☐ 8 hours sleep

EXAM DAY
☐ 700/1000 passes — you do not need everything
☐ ~2 min per question; flag anything over 3
☐ Always answer before flagging — no negative marking
☐ Microsoft Learn available in-exam: 1–2 lookups maximum
```

---

*Companion to `AI-103_Master_Guide` (content) and `ai103_execution_calendar.md` (schedule).*
*Teaching content withdrawn 31 Aug 2026 following a scope validation against the 16 April 2026 objectives.*
