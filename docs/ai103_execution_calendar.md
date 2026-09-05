# AI-103 — 31-Day Execution Calendar
## Target: 900+ | 28 Aug 2026 → Exam 28 Sep 2026

> **Companion document.** This tells you *when*.
> `AI-103_Master_Guide` (.md / .pdf) tells you *what*.
> `ai103_setup_and_resources.md` covers environment setup and the resource list.
> Booking confirmed: AI-102 voucher accepted for AI-103. Date locked, no reschedule.

---

## WHAT 900+ ACTUALLY REQUIRES

900/1000 = **90%**. Work the domain weights backwards:

| Scenario | D1+D2 (60%) | D3+D4+D5 (40%) | Total |
|----------|-------------|----------------|-------|
| Triage strategy | 85% → 51 | 55% → 22 | **73** |
| Strong triage | 90% → 54 | 60% → 24 | **78** |
| **900+ target** | **95% → 57** | **82% → 33** | **90** |

**The conclusion is unavoidable: there is no 900+ path that sandbags Domains 3–5.**

You cannot get there by being brilliant on agents and vague on Document Intelligence. 40% of the exam lives in Vision, Language, and Information Extraction, and 900+ requires genuine competence there — not just the service-selection table.

This is the single structural change from the previous plan.

---

## THE HOUR GAP, AND HOW TO CLOSE IT

| | Hours |
|---|---|
| Needed for 900+ | ~95 effective |
| Previously scheduled | 73 scheduled → ~58 effective |
| **Gap** | **~37 hours** |

Three levers, and you need all three:

**Lever 1 — Capstone overlap: +18 hrs**
No longer optional. If the EAGv3 capstone is Azure-scoped, roughly 18 hours of capstone work double-counts as Domain 1 + 2 study. If it isn't, 900+ is off the table on this timeline. **This is the decision that determines whether the target is reachable.**

**Lever 2 — Weekday hours 2 → 3: +16 hrs**
Across ~16 flexible weekdays. Your office is flexible except the first week; this is where that flexibility gets spent.

**Lever 3 — Weekend hours 4 → 6: +12 hrs**
Four weekends, both days.

Total recovered: **+46 hrs** against a 37-hour gap. There's ~9 hours of buffer for slippage — thin but real.

---

## THE CAPSTONE DECISION (make it this weekend)

Scope your EAGv3 capstone as an Azure AI Foundry agentic application. This is now load-bearing.

```
Agent over a document corpus:
  Azure AI Foundry project          → D1: hub/project/connections
  Managed Identity auth             → D1: RBAC, security
  Content Safety on outputs         → D1: responsible AI
  Tracing + evaluation enabled      → D1: monitoring, groundedness
  Azure AI Search hybrid index      → D2 + D5: indexers, skillsets
  Azure OpenAI embeddings + GPT-4o  → D2: RAG
  Agent Service, FileSearch + custom fn → D2: tools, function calling
  Document Intelligence ingestion   → D5: prebuilt + custom models
  Vision OCR on scanned inputs      → D3: Read API
```

Note the last two lines. Adding a document-ingestion path and OCR to your capstone pulls Domains 3 and 5 into the double-count — which is exactly where your 900+ risk sits.

---

## THE RESOURCE STACK

Video replaces Microsoft Learn *reading* time. It does not add to the budget.

| Resource | Cost | Use for | Hours |
|----------|------|---------|-------|
| **MS Learn YouTube playlist** (26 videos, official AI-103T00) | Free | Domains 1–2 + authoritative reference | ~12 |
| **Microsoft Learn modules** (Master Guide §3–§5) | Free | **Domains 3–5 backbone** — no course covers these well | ~10 |
| **Alan Rodrigues** — AI-103 sections only (~15h post-purge) | Udemy Business | Domain 1 core, Domain 5, Domain 2 framing. **Not Domain 3.** | ~8 |
| **Foundry playgrounds** — images and video | Azure credit | **Domain 3 hands-on** — generate, inpaint, submit a Sora job | ~4 |
| **MS Practice Assessment** | Free | Best phrasing match — **check availability by 10 Sep** | ~2 |
| **Scott Duffy** — 4 timed tests, 100 q, 4.4★ | Udemy Business | Timed simulation, score calibration | ~6 |
| **Trevoir Williams** — 1,500 q, unrated | Udemy Business | Volume drilling only | ~8 |

**Why Rodrigues over the other five:** most-reviewed by a wide margin, and its granular lecture structure lets you cherry-pick. Use it for **Domain 1 and Domain 5**, and for framing on Domain 2.

⚠️ **Do not lean on Rodrigues for Domain 3.** His vision section predates the generation-first scope — it teaches Image Analysis, Custom Vision, and Face. Master Guide §3 plus hands-on work in the Foundry images and video playgrounds is your Domain 3 source. The same caution applies to his Domain 4 section, which is Language-service-shaped rather than generative-prompting-shaped.

**Why the official playlist isn't enough alone:** AI-103T00 is scoped to generative AI, agents, and tool integration — Domains 1–2, your existing strength. Domains 3–5 get light treatment, and that's where 900 is won or lost.

**The uncomfortable truth about Domain 3:** no video course on the market covers image and video generation at the weight the objectives give it. That material comes from Master Guide §3, Microsoft Learn, and actually generating and editing images yourself.

**Trust hierarchy when sources conflict:** official study guide → Microsoft Learn docs → MS Learn playlist → **Master Guide** → Rodrigues → practice tests. Third-party AI-103 content is under six months old and some of it is AI-102 re-labelled.

---

## DAY-BY-DAY CALENDAR

### 🔴 TODAY — Friday 28 Aug (2.5 hrs)

Lead-time items first. Everything downstream blocks on these.

```
☐ AZURE FREE ACCOUNT (30 min)
    https://azure.microsoft.com/free

☐ AZURE OPENAI ACCESS REQUEST (15 min)  ← 1–3 DAY LEAD TIME
    https://aka.ms/oai/access
    Blocks all Week 2 labs. Submit before you sleep.

☐ PYTHON ENVIRONMENT (60 min)
    §1.3 of the setup document. Python 3.11+, VS Code, venv, all SDKs.

☐ AI FOUNDRY HUB + PROJECT (20 min)
    https://ai.azure.com → hub (East US) → project "ai103-lab"

☐ PROVISION ALL SERVICE RESOURCES NOW (25 min)
    Language, Vision, Document Intelligence, AI Search, Speech.
    All free tier. Populate .env completely today.
    → Removes provisioning friction from every future lab session.

☐ DOWNLOAD RODRIGUES AI-102 SECTIONS (30 min)  ← REMOVED THIS WEEKEND
    Udemy mobile app → offline download:
      AI-102 computer vision / NLP / knowledge mining
    Insurance only. Skip if Udemy Business blocks download.
```

That last item is new and it matters. At 900+ pace you cannot lose 20 minutes of a study block to portal navigation.

---

### 🟢 Weekend 1 — Sat 29 + Sun 30 Aug (6 hrs each = 12 hrs)

**Saturday 29 Aug — Domain 1A**
| Time | What | Ref |
|------|------|-----|
| 1.5 hr | AI Foundry: hub, project, connections, model catalog | §1.1 |
| 1.5 hr | Auth: Managed Identity, all 5 RBAC roles, private endpoints | §1.4 |
| 1 hr | Lab: `test_auth.py` both key-based and DefaultAzureCredential | §1.4.4 |
| 1 hr | Responsible AI: 6 principles, Content Safety, groundedness | §1.6 |
| 1 hr | **Commit capstone scope in writing.** One paragraph, Azure-based. | — |

**Sunday 30 Aug — Domain 1B**
| Time | What | Ref |
|------|------|-----|
| 1.5 hr | Model selection: GPT-4o vs mini vs o3 vs Phi, PTU vs standard | §1.2–1.3 |
| 1.5 hr | Containers, monitoring, diagnostic logs, cost management | §1.8–1.9 |
| 1 hr | Lab: Content Safety API, deliberately trigger each category | §1.6 |
| 1 hr | **Active recall:** close notes, explain Hub-vs-Project aloud | — |
| 1 hr | Domain 1 cheat sheet, handwritten | §1.11 |

> **Active recall is a 900+ requirement, not a nicety.** Recognition gets you to 700. Recall gets you to 900. From here, every session ends with 15 minutes of explaining the material with notes closed.

---

### 🟡 TIGHT WEEK — Mon 31 Aug → Fri 4 Sep (1.5 hrs/day = 7.5 hrs)

Office is tight. **This is the week for the official Microsoft Learn YouTube playlist** — video demands less focus than labs, and it runs on mobile during commutes.

Work through the 26 videos in order. They map to Domains 1–2, consolidating Weekend 1 and front-loading Week 3.

| Day | Focus | Ref |
|-----|-------|-----|
| Mon 31 | MS playlist videos 1–5 + Azure OpenAI chat API params | §2.1 |
| Tue 1 Sep | MS playlist 6–10 + embeddings, dimensions | §2.1 |
| Wed 2 Sep | MS playlist 11–15 + prompt engineering, all four techniques | §2.2 |
| Thu 3 Sep | MS playlist 16–20 + RAG architecture end to end | §2.3–2.4 |
| Fri 4 Sep | MS playlist 21–26 + search types and when each wins | §2.3–2.4 |

Even at reduced focus, aim to finish the playlist this week. It is the only fully exam-aligned video resource you have.

---

### 🟢 Weekend 2 — Sat 5 + Sun 6 Sep (6 hrs each = 12 hrs)

**Saturday 5 Sep — RAG built, not read**
| Time | What |
|------|------|
| 1 hr | AI Search: create index with vector field, load sample docs |
| 2 hr | Build the RAG pipeline from Master Guide §2.4.4 — **type every line** |
| 1 hr | Break it: wrong key (401), wrong role (403), wrong index (404), flood it (429). Read each error. |
| 1 hr | Convert to hybrid + semantic ranking, compare result quality |
| 1 hr | Capstone: repo scaffold, connection test green |

**Sunday 6 Sep — Agents**

> ⚠️ **Corrected scope.** An earlier version of this plan scheduled Semantic Kernel here. **Microsoft Agent Framework 1.0** is the current path — build with MAF, not SK.

| Time | What | Ref |
|------|------|-----|
| 1.5 hr | Agent Service: agent, thread, message, run; FileSearch, CodeInterpreter, `requires_action` | §2.6 |
| 1 hr | Custom function tool — write one end to end | §2.5 |
| 1.5 hr | **MAF hands-on:** `pip install agent-framework`; create a ChatAgent; register a function tool; run it async | §2.7 |
| 1 hr | **MAF orchestration:** sequential and concurrent; then Workflows — executors, edges, human-in-the-loop | §2.7.4, §2.8 |
| 0.5 hr | Memory strategies and approval/oversight controls | §2.13, §2.15 |
| 0.25 hr | **Legacy terminology only:** Semantic Kernel (kernel/plugin/function/planner) and AutoGen — recognise, don't build | §2.7.6 |
| 0.25 hr | Capstone: first agent responding over your documents | — |

---

### 🟢 Week 3 — Mon 7 → Fri 11 Sep (3 hrs/day = 15 hrs)

| Day | Focus | Ref |
|-----|-------|-----|
| Mon 7 | Evaluation metrics (all 7) + tracing setup | §2.9–2.10 |
| Tue 8 | "On Your Data" vs manual RAG, when each is correct | §6.2 |
| Wed 9 | **Domain 1+2 question set — 40 questions.** Target 80%+ | §2.17 |
| Thu 10 | Wrong-answer review + capstone build | — |
| Fri 11 | Capstone build + Domain 2 gap fill | — |

**Checkpoint Fri 11 Sep: Domains 1+2 at 85%+.** For a 900+ run these must be near-finished by now, because Weeks 4 and 5 belong to Domains 3–5 — which is where your target actually gets decided.

---

### 🟢 Weekend 3 — Sat 12 + Sun 13 Sep (6 hrs each = 12 hrs)

**This is the weekend that separates a 750 from a 900.** Previous plan gave Domains 3–5 a speed run. Now they get full treatment.

**Domains 3–5 strategy: Microsoft Learn is primary, video is supplementary.**

Rodrigues is removing all AI-102 lectures the weekend of 29–30 Aug. Download the AI-102 computer vision, NLP, and knowledge mining sections before then as insurance — but do not build around them.

**The market problem:** every AI-103 course is agent- and RAG-heavy, because that is the new and marketable content. Vision, text analysis, and information extraction are the unglamorous 40% nobody builds a course around. Rodrigues' new Domains 3–5 sections total ~4 hours. No video course will carry you to 82% here.

**Order of sources for Domains 3–5:**
| Priority | Source | Why |
|---|---|---|
| 1 | Microsoft Learn modules (Master Guide §3–§5) | The actual backbone. Official, complete, current. |
| 2 | Hands-on labs — every one typed and run | Where 82% comes from |
| 3 | Rodrigues NEW sections (~4h) | Current framing, Content Understanding |
| 4 | Downloaded AI-102 sections | Only if practice tests show a gap |

**Watch from Rodrigues (new sections only):**
| Section | Runtime |
|---|---|
| NEW — Computer vision | 42m |
| NEW — Text analysis | 1h 49m |
| NEW — Information extraction | 1h 34m |
| NEW — Practice Section | 1h 29m |

**Content Understanding** — unified processing of images, video, audio, documents — is genuinely new and appears in no AI-102 material. Get it from the new sections and the official Microsoft playlist.

**Saturday 12 Sep — Domain 3: generation and multimodal**

> ⚠️ **Scope correction.** AI-103 Domain 3 is image/video **generation**, editing, multimodal understanding, and visual safety — not the AI-102 Custom Vision and Face syllabus. Rodrigues' Domain 3 section and the downloaded AI-102 vision material are largely **out of scope**. Work from Master Guide §3 and Microsoft Learn instead.

| Time | What | Ref |
|------|------|-----|
| 1.5 hr | Image generation: gpt-image models, parameters, text-to-image, image-to-image | §3.2 |
| 1.5 hr | Editing: masks, inpainting, outpainting; **run these in the Foundry images playground** | §3.3 |
| 1 hr | Video generation: Sora 2, the async job pattern, video editing concepts | §3.4 |
| 1 hr | Multimodal understanding, alt text, visual prompt injection | §3.6, §3.8 |
| 1 hr | Legacy vision skim — recognition only, do not over-invest | §3.9 |

**Sunday 13 Sep — Domain 4: generative text analysis + speech**

> ⚠️ **Same correction.** Domain 4 leads with **generative prompting and Foundry Tools** — structured JSON extraction, tone and safety detection, LLM translation, audio multimodal reasoning. Classic Language service operations are the specialist tools, not the syllabus.

| Time | What | Ref |
|------|------|-----|
| 1.5 hr | Structured extraction with `json_schema`; the LLM-vs-service decision | §4.1, §4.2 |
| 1 hr | Tone, safety, sensitive content; LLM vs Translator | §4.2.3–4 |
| 0.5 hr | Multimodal audio reasoning vs transcription | §4.3 |
| 1 hr | Language service operations — where they still win | §4.4 |
| 1 hr | Speech: STT, TTS, SSML — run all three | §4.5 |
| 1 hr | Active recall: 20 service-selection scenarios, notes closed | §6.3 |

---

### 🟢 Week 4 — Mon 14 → Fri 18 Sep (3 hrs/day = 15 hrs)

| Day | Focus | Ref |
|-----|-------|-----|
| Mon 14 | Document Intelligence: all 7 prebuilt models, run 3 of them | §5.1 |
| Tue 15 | Custom DI models: template vs neural vs composed | §5.1 |
| Wed 16 | AI Search deep: indexers, skillsets, index attributes, Knowledge Store | §5.3 |
| Thu 17 | **PRACTICE TEST 1** — 90 min strict + full review | §6.4 |

> **Source for Test 1:** Microsoft's official Practice Assessment (AI Skills Navigator) **if it is available** — as of now Microsoft's certification page has indicated it may not be, since practice assessments typically appear after an exam leaves beta. **Check availability by 10 Sep.** If it isn't live, use Scott Duffy timed test 1 here and shift the Duffy tests forward one slot, with Trevoir Williams questions filling the final week.
| Fri 18 | Weakest-domain repair from Test 1 | §6.6 |

**Test 1 targets (17 Sep) — 900+ calibration:**
```
Overall:      75%+     (was 60% on the pass-oriented plan)
Domain 1:     85%+
Domain 2:     85%+
Domains 3-5:  65%+     ← the number that decides your ceiling
```

If Domains 3–5 come in under 60%, that is the signal to reallocate — not Domain 2.

---

### 🟢 Weekend 4 — Sat 19 + Sun 20 Sep (6 hrs each = 12 hrs)

**Saturday 19 Sep**
| Time | What | Ref |
|------|------|-----|
| 2 hr | Integration scenarios — trace 5 end-to-end architectures | §6.1 |
| 1.5 hr | All 6 exam traps, worked through | §6.2 |
| 1.5 hr | Capstone finish |
| 1 hr | 20-question scenario gauntlet, notes closed | §6.3 |

**Sunday 20 Sep**
| Time | What | Ref |
|------|------|-----|
| 1.5 hr | **PRACTICE TEST 2** — Scott Duffy, timed test 1 of 4 | §6.4 |
| 1.5 hr | Full wrong-answer review, read Learn page for every miss |
| 2 hr | Second pass on the two weakest domains |
| 1 hr | Rewrite all 5 cheat sheets by hand | §6.3 |

**Test 2 target: 85%+.**

---

### 🟢 Final Week — Mon 21 → Sun 27 Sep (2.5 hrs/day = 15 hrs)

| Day | Focus |
|-----|-------|
| Mon 21 | Domain 1 + 2: cheat sheets, then 30 Trevoir questions, target 90% |
| Tue 22 | Domains 3–5: cheat sheets, then 30 Trevoir questions, target 85% |
| Wed 23 | **PRACTICE TEST 3** — Scott Duffy, timed test 2 of 4 |
| Thu 24 | Wrong-answer review. **New material stops here.** |
| Fri 25 | Full active recall: explain all 5 domains aloud, notes closed |
| Sat 26 | Light — 20 questions, cheat sheet skim. Pearson VUE tech check. |
| Sun 27 | Exam eve. 45 min skim. Nothing else. Sleep 8 hours. |

**Test 3 target (23 Sep): 88%+.**

---

### 🎯 Monday 28 Sep — EXAM

§6.4 of the Master Guide has the full checklist. For a 900+ run specifically:

- **Pace: 2 min/question, not 2.4.** You want 20+ minutes at the end, not 10 — a 900 is won in the review pass, catching two or three misreads.
- **Microsoft Learn: one lookup maximum.** At this level of prep, if you need the docs you've likely misread the question. Re-read it instead.
- Flag anything under 90% certain. Answer it first, then flag.
- No negative marking. Never leave one blank.

---

## HOUR BUDGET

| Block | Hours |
|-------|-------|
| Today | 2.5 |
| Weekend 1 | 12 |
| Tight week | 7.5 |
| Weekend 2 | 12 |
| Week 3 | 15 |
| Weekend 3 | 12 |
| Week 4 | 15 |
| Weekend 4 | 12 |
| Final week | 15 |
| **Scheduled** | **103** |
| Capstone double-count | +18 effective |
| Less ~15% slippage | −15 |
| **Effective** | **~106** |

Against the ~95 needed for 900+. **The target is reachable on these numbers.**

---

## WHAT THE 900+ TARGET COSTS YOU

Being direct about the trade, since you should choose it knowingly:

- **Three hours on flexible weekdays, six on weekend days, for a month.** Not two and four. The plan has ~9 hours of buffer total; two lost weekend days consumes it.
- **The capstone must be Azure.** If EAGv3 requires a different stack, you lose 18 effective hours and the realistic ceiling drops to roughly 800.
- **Domains 3–5 get built, not skimmed.** Every lab in Weekend 3 and Week 4 gets typed and run. This is the part most candidates skip and it's precisely why most land at 750 rather than 900.
- **Active recall every session.** Fifteen minutes, notes closed, explaining aloud. Tedious, and it's the difference between recognising an answer and producing one under time pressure.

One thing outside your control: AI-103 has been live under five months, so practice-test scores are a noisier signal than they'd be for a mature exam. Treat the score targets as directional. If you're consistently above them and your active recall is genuinely fluent, you're ready regardless of what any single practice test says.

---

*Companion to: `AI-103_Master_Guide` (content) and `ai103_setup_and_resources.md` (setup).*
*Rebuilt for 900+ target: 28 Aug 2026 | Exam: 28 Sep 2026*
