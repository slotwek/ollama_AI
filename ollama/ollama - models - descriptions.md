---
date: 2026-09-21
aliases:
relates_to:
---
# For coding:
Yes. If your constraint is **≤7B parameters** and you're interested in **local coding models**, the field is actually fairly manageable.

## My shortlist

|Model|Size|My use case|Approx. Q4 RAM/VRAM*|
|---|--:|---|--:|
|**Qwen2.5-Coder 7B Instruct**|7.6B|⭐ General coding / debugging|~5–6 GB|
|**Qwen3 Coder 7B**|7B|⭐ Newer coding/agent workflows|~5–6 GB|
|**DeepSeek-Coder 6.7B Instruct**|6.7B|Coding + code completion|~5 GB|
|**Qwen2.5-Coder 3B**|3.1B|Fast laptop coding|~2–3 GB|
|**Qwen2.5-Coder 1.5B**|1.5B|Very lightweight autocomplete|~1–2 GB|
|**CodeLlama 7B**|7B|Legacy/compatibility|~5 GB|

*Actual memory use depends heavily on quantisation, context length and runtime.

### 1. Qwen2.5-Coder 7B — my first recommendation

Alibaba Cloud's **Qwen2.5-Coder-7B-Instruct** is probably the first model I'd install on a modest machine.

It has **7.61B parameters**, a **128K context window**, and was specifically trained for code generation, reasoning, fixing and completion. The model supports a very broad range of programming languages. ([Hugging Face](https://huggingface.co/Qwen/Qwen2.5-Coder-7B?utm_source=chatgpt.com "Qwen/Qwen2.5-Coder-7B · Hugging Face"))

For your use, I'd particularly consider it for:

- Python
    
- SQL/PostgreSQL
    
- FastAPI
    
- Docker
    
- Bash/Linux
    
- PowerShell
    
- JavaScript/TypeScript
    
- debugging
    
- explaining unfamiliar code
    
- generating tests
    
- refactoring
    

And importantly, you've already got **Ollama + Open WebUI** running, so it's trivial to experiment with.

For Ollama:

```bash
ollama pull qwen2.5-coder:7b
```

Then:

```bash
ollama run qwen2.5-coder:7b
```

I'd start with **Q4** rather than trying to squeeze a higher-precision version into limited RAM/VRAM.

---

### 2. Qwen3 Coder 7B — worth testing

This is the newer generation I'd investigate before settling on Qwen2.5-Coder.

Current 2026 comparisons generally put the newer Qwen3 Coder family ahead of older 7B coding models for more complex coding and agent-style tasks. ([Run Local AI Models](https://runlocalmodel.com/best-local-coding-llm-2026.html?utm_source=chatgpt.com "Best Local LLM for Coding in 2026: Qwen Coder, DeepSeek Coder V3 & More | RunLocalModel"))

The interesting distinction is:

**Qwen2.5-Coder 7B**  
→ excellent lightweight coding assistant

**Qwen3 Coder 7B**  
→ more interesting for reasoning, multi-step coding and agent workflows

So if your objective is something like:

> "Here is my FastAPI repository. Understand it, modify three files, add tests and explain what you changed."

I'd lean toward **Qwen3 Coder**.

For simple:

> "Write a Python function that does X."

the difference may be much less noticeable.

---

### 3. DeepSeek-Coder 6.7B

DeepSeek's original **DeepSeek-Coder 6.7B** remains interesting.

It was trained specifically around programming, with 2T training tokens and a large proportion of code, and supports fill-in-the-middle/code completion. ([GitHub](https://github.com/deepseek-ai/DeepSeek-Coder?utm_source=chatgpt.com "GitHub - deepseek-ai/DeepSeek-Coder: DeepSeek Coder: Let the Code Write Itself · GitHub"))

It's particularly interesting if you're using an IDE where **code completion** is more important than conversational interaction.

However, I wouldn't make it my first installation today. Qwen's newer coding models have largely displaced it for general local coding assistance.

---

### 4. Qwen2.5-Coder 3B — don't underestimate this one

This is the model I'd consider if you're running on a **CPU-only laptop**.

It's only ~3.1B parameters, so you sacrifice some reasoning ability but gain considerably better responsiveness.

For example:

> "Explain this SQL query."

> "Fix this Python error."

> "Write a PostgreSQL query to calculate monthly revenue."

> "Convert this Python function to use pandas."

A 3B model can be perfectly usable.

It could actually be **more pleasant than a 7B model running painfully slowly on CPU**.

---

## What I'd use on your hardware

From our previous discussions, you've got machines such as the **Lenovo V15-ADA**, your HP laptops, and you've been experimenting with Ollama/Open WebUI.

I'd think about it like this:

### 16 GB RAM, CPU only

**Qwen2.5-Coder 3B Q4**

→ probably the sensible everyday model.

You can try 7B, but generation speed may become frustrating.

### 16 GB RAM + decent integrated GPU

**Qwen2.5-Coder 7B Q4**

→ my preferred experiment.

Your Iris Xe isn't really a "coding LLM GPU" in the conventional sense, but Ollama/llama.cpp can potentially make use of supported GPU acceleration.

### 32 GB RAM

**Qwen3 Coder 7B Q4/Q5**

→ this is where I'd start experimenting seriously.

You can also keep several models installed simultaneously:

```text
qwen2.5-coder:3b
qwen2.5-coder:7b
qwen3-coder:7b
```

and choose depending on the task.

---

## One important distinction: coding vs autocomplete

This is easy to overlook.

There are really **three different jobs**:

### A. "Chat with my code"

For example:

> Here's my FastAPI project. Why am I getting this error?

→ **Qwen3 Coder 7B / Qwen2.5-Coder 7B**

### B. "Write a complete piece of code"

> Build me a FastAPI endpoint with PostgreSQL and Pydantic validation.

→ **Qwen3 Coder 7B**

### C. "Autocomplete while I'm typing"

```python
def calculate_customer_
```

→ you want a model optimised for **FIM (Fill-in-the-Middle)** and low latency.

That's a slightly different optimisation problem. Qwen2.5-Coder explicitly supports FIM and long-context coding workflows. ([Hugging Face](https://huggingface.co/Qwen/Qwen2.5-Coder-7B?utm_source=chatgpt.com "Qwen/Qwen2.5-Coder-7B · Hugging Face"))

---

## What I would _not_ bother with

For a new setup, I wouldn't prioritise **CodeLlama 7B**.

It's an older generation, and newer coding-specific models have substantially moved on. Current comparisons likewise put Qwen2.5-Coder ahead of CodeLlama for this sort of local coding workload. ([InsiderLLM](https://insiderllm.com/guides/codellama-vs-deepseek-coder-vs-qwen-coder/?utm_source=chatgpt.com "CodeLlama vs DeepSeek Coder vs Qwen Coder: Best Local Coding Models Compared | InsiderLLM"))

Likewise, I wouldn't automatically assume that **more parameters = better coding**. A well-trained 7B coding model can be substantially more useful for programming than a generic 13B/14B model.

---

## My practical recommendation for you

Since you're already experimenting with **Ollama + Open WebUI**, I'd actually install **three models** and compare them on the _same real tasks from your own projects_:

```bash
ollama pull qwen2.5-coder:7b
ollama pull qwen2.5-coder:3b
```

and then, if your Ollama version/repository exposes it:

```bash
ollama pull qwen3-coder:7b
```

Then give each exactly the same 5 tasks:

1. **Python debugging**
    
2. **FastAPI implementation**
    
3. **PostgreSQL/SQL problem**
    
4. **Docker troubleshooting**
    
5. **Refactor an existing piece of code**
    

I'd particularly test them against the kind of **FastAPI + PostgreSQL + Docker** work you've been doing. That's much more meaningful than relying on HumanEval scores alone.

**If I had to pick only one ≤7B model for you today: I'd start with Qwen3 Coder 7B, with Qwen2.5-Coder 7B as the comparison model.**


# For Data Engineering work:
Yes — but there's an important distinction: **there aren't many genuinely “Data Engineering LLMs” under 7B**. Most specialised models focus on **SQL/Text-to-SQL**, rather than the whole DE stack (Python, PySpark, dbt, Airflow, Azure, Synapse, dimensional modelling, pipelines, etc.).

For your background, I'd actually use a **general coding model + a SQL specialist**, rather than looking for one model that claims to be a Data Engineering model.

### Models I'd look at

|Model|Size|Specialisation|My take|
|---|--:|---|---|
|**Qwen2.5-Coder 7B**|7.6B|Coding + SQL + Python|⭐ Best general DE model|
|**Qwen3-Coder 7B**|~7B|Coding/reasoning/agents|⭐ Very interesting for pipelines|
|**OmniSQL 7B**|~8B|**Text-to-SQL**|⭐ SQL specialist|
|**XiYanSQL-QwenCoder 7B**|~7B|**Text-to-SQL**|⭐ SQL specialist|
|**SQLCoder-7B-2**|7B|SQL generation|Good specialised SQL option|
|**DuckDB-NSQL-7B**|7B|**DuckDB SQL**|Excellent if DuckDB is central|
|**GaussDB SQL Expert 7B**|7.6B|SQL tuning/diagnostics|Interesting specialist|

There are currently several 7B/8B SQL-specialised models available, including OmniSQL and XiYanSQL-QwenCoder. ([Hugging Face API Inference](https://api-inference.huggingface.co/models?other=Text-to-SQL&utm_source=chatgpt.com "Models – Hugging Face"))

### For _your_ Data Engineering work

I'd divide the tasks like this:

**Qwen3-Coder / Qwen2.5-Coder**

```text
Python
PySpark
Pandas
Polars
Azure Functions
Azure Data Factory
Synapse pipelines
Docker
Bash
PowerShell
dbt
Airflow
Terraform
Git
CI/CD
Data modelling
ETL/ELT architecture
```

Then use a SQL-specialist for:

```text
complex SQL
query optimisation
execution plans
SQL dialect conversion
Text → SQL
schema → SQL
SQL debugging
```

That's actually a pretty powerful combination.

For example, **GaussDB SQL Expert 7B** is specifically fine-tuned from Qwen2.5-Coder-7B and targets SQL generation, optimisation, migration and database troubleshooting. Its model card reports support for PostgreSQL, SQL Server, MySQL, Oracle and several other databases. ([Hugging Face](https://huggingface.co/lanfers/gaussdb-sql-expert-7b?utm_source=chatgpt.com "lanfers/gaussdb-sql-expert-7b · Hugging Face"))

---

## The interesting part for you: SQL + Data Engineering

I wouldn't dismiss the general coding models for DE.

A recent 2026 evaluation of open models on SQL/analytics tasks found **Qwen2.5-Coder** particularly strong: it achieved the highest single-agent execution accuracy in that evaluation and a 90.14% semantic score on the custom SQL suite. ([ScienceDirect](https://www.sciencedirect.com/org/science/article/pii/S1546221826005047?utm_source=chatgpt.com "Evaluating Open-Source LLM Agents for SQL Generation and Structured Analytics on Relational Databases - ScienceDirect"))

And a 2026 on-premise BIRD evaluation found that **Qwen2.5-Coder 7B substantially outperformed CodeLlama 7B** on Text-to-SQL under the same evaluation setup (39.1 vs 20.9 execution accuracy). ([arXiv](https://arxiv.org/abs/2606.29733?utm_source=chatgpt.com "How Far Do On-Prem Open LLMs Get on Text-to-SQL? A Cross-Family Size x Technique Frontier on BIRD"))

So I wouldn't automatically replace Qwen2.5-Coder with a model labelled "SQL".

---

# I'd build your local DE setup like this

Given that you're already running **Ollama + Open WebUI**, I'd try:

### 🧠 Main DE assistant

**Qwen2.5-Coder 7B**

Use it for:

> "Write a PySpark transformation that..."

> "Design a medallion architecture for this dataset."

> "Why is my Synapse pipeline doing this?"

> "Convert this pandas transformation to PySpark."

> "Create a dbt incremental model."

> "Write an Airflow DAG."

> "Review this ETL code."

### 🗄️ SQL specialist

**OmniSQL 7B** or **XiYanSQL-QwenCoder 7B**

Use it for:

> "Generate SQL from this schema."

> "Optimise this query."

> "Convert this SQL Server query to PostgreSQL."

> "Explain why this query is producing duplicates."

### 🦆 DuckDB specialist

**DuckDB-NSQL-7B**

This one is particularly interesting if you're playing with your **Parquet/CSV + local analytics** environment.

DuckDB-NSQL-7B was specifically fine-tuned for DuckDB SQL rather than merely being a general coding model. ([GitHub](https://github.com/huggingface/blog/blob/main/duckdb-nsql-7b.md?utm_source=chatgpt.com "blog/duckdb-nsql-7b.md at main · huggingface/blog · GitHub"))

---

## But there's an even better approach

For **Data Engineering**, the model itself is only half the story.

I'd rather have:

**Qwen2.5-Coder 7B**

**your actual documentation/schema/code**

**tool access**

than a supposedly "Data Engineering 7B" model with no knowledge of your environment.

For example:

```text
                    ┌─────────────────────┐
                    │ Qwen2.5-Coder 7B    │
                    │                     │
                    │ DE reasoning        │
                    │ Python / PySpark     │
                    │ SQL / dbt            │
                    └──────────┬──────────┘
                               │
              ┌────────────────┼────────────────┐
              ↓                ↓                ↓
          PostgreSQL       DuckDB          Git repo
              │                │                │
          schema + SQL     Parquet/CSV      Python code
```

Then the model can work with **your actual schemas, pipelines and code**, instead of guessing.

This is especially relevant because Text-to-SQL systems have a fundamental problem with **schema linking and dialect differences** — e.g. knowing whether a function or column actually exists in PostgreSQL vs SQL Server vs Snowflake. ([Hugging Face Forums](https://discuss.huggingface.co/t/system-prompts-llm/173290?utm_source=chatgpt.com "System Prompts & LLM - Models - Hugging Face Forums"))

### One thing I'd change from my previous recommendation

Given that you're specifically interested in **Data Engineering**, I would now test **Qwen2.5-Coder 7B vs Qwen3-Coder 7B vs a SQL specialist**, rather than simply picking the best general coding model.

If you want, I can also put together a **“local Data Engineer LLM stack” under 7B**, specifically covering **SQL + PySpark + Azure/Synapse + dbt + Airflow + Docker + data modelling**, including which models are available directly through Ollama and roughly how much RAM each needs.

# Learning Italian:
Yes. If your goal is **a local LLM that feels like an Italian conversation partner**, rather than merely one that can answer Italian questions, I'd choose somewhat differently from a coding model.

Since you're looking at **≤7B-ish models for local use**, there are two categories worth considering:

### My picks

|Model|Size|Italian quality|Conversation|Recommendation|
|---|--:|---|---|---|
|**Qwen2.5-7B-Instruct**|~7B|⭐⭐⭐⭐⭐|⭐⭐⭐⭐⭐|**My first choice**|
|**Gemma 3 4B IT**|4B|⭐⭐⭐⭐½|⭐⭐⭐⭐½|Excellent lightweight option|
|**LLaMAntino-3-ANITA 8B**|~8B|⭐⭐⭐⭐⭐|⭐⭐⭐⭐|Italian specialist|
|**Zefiro-7B**|7B|⭐⭐⭐⭐⭐|⭐⭐⭐⭐|Italian specialist|
|**Cerbero-7B**|7B|⭐⭐⭐⭐⭐|⭐⭐⭐⭐|Italian specialist|
|**Minerva-7B**|7B|⭐⭐⭐⭐|⭐⭐⭐|Interesting Italian-native model|
|**Mistral 7B Instruct**|7B|⭐⭐⭐⭐|⭐⭐⭐⭐|Good general alternative|

There is actually a dedicated Italian-model ecosystem that's quite interesting. A current Italian QA leaderboard has **Gemma_QA_ITA_v3, Zefiro-7B, Cerbero-7B and Saiga-7B** near the top of its tracked models. ([The Aggregate](https://theaggregate.ai/benchmark?slug=open-italian-llm-leaderboard&utm_source=chatgpt.com "Open Italian LLM Leaderboard Leaderboard · The Aggregate"))

## 🥇 I'd start with Qwen2.5-7B-Instruct

This might sound surprising given that we were discussing coding models, but **Qwen2.5-7B-Instruct is particularly good for multilingual conversation**.

Qwen reports support for 29+ languages including Italian, and its multilingual benchmarks are strong. ([Qwen](https://qwen.ai/blog?id=qwen2.5-llm&utm_source=chatgpt.com "Qwen"))

More importantly for **language learning**, I find a general multilingual model preferable to a model trained exclusively on Italian if you want to do things like:

> "Parlami della tua giornata."

> "Correggi i miei errori, ma non interrompermi."

> "Fammi una domanda alla volta."

> "Parliamo come due amici italiani."

It can maintain the conversation while switching between Italian and English when you need an explanation.

For Ollama:

```bash
ollama pull qwen2.5:7b
```

Then I'd give it a system prompt along the lines of:

```text
You are my Italian conversation partner.

Speak primarily in Italian at approximately B1 level.

I am learning Italian and want to improve my conversational ability.

Do not correct every small mistake immediately. Keep the conversation natural.
When I make an important grammatical or vocabulary mistake:
1. briefly correct it,
2. explain the correction in English,
3. continue the conversation in Italian.

Ask me questions and encourage me to give longer answers.
Occasionally introduce useful Italian expressions and vocabulary.
```

For your **~B1 Italian**, that should work particularly well.

---

## 🇮🇹 But there are some fascinating Italian-specific models

### Zefiro-7B

This is one I'd definitely experiment with.

It's an Italian-focused 7B model and appears near the top of current Italian QA evaluations. ([The Aggregate](https://theaggregate.ai/benchmark?slug=open-italian-llm-leaderboard&utm_source=chatgpt.com "Open Italian LLM Leaderboard Leaderboard · The Aggregate"))

The advantage is that it has been specifically adapted toward Italian rather than relying primarily on multilingual pretraining.

I'd test it against Qwen with:

> "Raccontami una storia breve ambientata a Bologna."

and

> "Facciamo una conversazione informale. Io sono un turista polacco che visita l'Italia."

The important thing isn't just whether the grammar is correct. You want to see whether it produces **natural Italian rather than translated English**.

---

## 🇮🇹 LLaMAntino / ANITA

Another interesting family is **LLaMAntino**, developed specifically for Italian.

The newer **LLaMAntino-3-ANITA-8B** appears in Italian-language benchmarks alongside models such as Qwen2.5-7B, Mistral and Gemma. ([ACL Anthology](https://aclanthology.org/2025.clicit-1.61.pdf?utm_source=chatgpt.com "A Leaderboard for Benchmarking LLMs on Italian"))

It's slightly above your 7B limit, though, so I wouldn't make it your first choice if you're strict about the parameter limit.

---

## Gemma 3 4B IT is particularly interesting for you

This is probably the **small model I'd test first**.

You get a much smaller model than 7B while retaining very good multilingual capability.

There's also a dedicated Italian evaluation showing that **Gemma 3 4B-it** was included among the small multilingual models evaluated for Italian. ([Springer](https://link.springer.com/article/10.1007/s10579-026-09926-8?utm_source=chatgpt.com "Do you understand Italian? Evaluating LVLMs on Italian visual question-answering | Language Resources and Evaluation | Springer Nature Link"))

So I'd have:

```text
Qwen2.5 7B
      ↓
main Italian conversation partner

Gemma 3 4B
      ↓
fast / lightweight Italian conversation
```

If you're running on one of your 16 GB machines, this could make a surprisingly good setup.

---

## What about Minerva?

**Minerva 7B** is particularly interesting because it was developed specifically for Italian.

Its creators describe it as an Italian-language model and compare it against Mistral 7B, Llama 3.1 8B and LLaMAntino. ([Minerva LLM](https://minerva-ai.org/en/docs/tech-page?utm_source=chatgpt.com "Minerva AI LLM: Technical Documentation"))

However, I wouldn't automatically assume that "Italian-specific" means better conversation.

That's something I'd **test rather than assume**.

---

### And there's an important trick for language learning

I'd actually use **two different modes**.

#### Mode 1 — Immersion

```text
100% Italian
No translations
B1 vocabulary
Natural conversation
Correct only significant mistakes
```

This helps you develop fluency.

#### Mode 2 — Tutor

```text
Italian conversation
↓
your answer
↓
correction
↓
short explanation in English
↓
next question
```

This helps accuracy.

And I'd explicitly tell the model:

> **Don't make your Italian artificially perfect. Speak like a normal Italian person, but keep vocabulary around B1/B2.**

Otherwise small local models tend to produce things like:

> _"È un piacere discorrere con te riguardo alle tue esperienze..."_

which is grammatically fine but **not how you want your conversation partner to sound.** 😂

---

## One more thing: voice

For **your particular use case**, voice could change the recommendation considerably.

If you're planning:

**Ollama + Open WebUI + microphone → Italian conversation**

then I'd prioritise:

1. **Qwen2.5 7B**
    
2. **Gemma 3 4B**
    
3. **Zefiro 7B**
    

rather than obsessing over Italian benchmark scores.

The model needs to generate **short, natural responses quickly**. A slightly less capable model that responds in 1–2 seconds is much more useful for speaking practice than a "better" model that takes 10 seconds to answer.

And if you eventually want a completely local setup, you can combine:

**Whisper → LLM → Italian TTS**

to get a genuinely useful private Italian conversation partner.

Given your existing **Ollama/Open WebUI setup**, that's actually a very achievable project.

# Spanish
Yes. For **Spanish conversation practice**, I'd actually broaden the shortlist compared with Italian because Spanish is much better represented in multilingual models.

Since you're interested in **local models ≤7B**, my shortlist would be:

|Model|Size|Spanish|Conversation|I'd use it for|
|---|--:|---|---|---|
|**Qwen2.5-7B-Instruct**|7B|⭐⭐⭐⭐⭐|⭐⭐⭐⭐⭐|**Best all-rounder**|
|**Qwen3-8B**|8B|⭐⭐⭐⭐⭐|⭐⭐⭐⭐⭐|If you relax the 7B limit|
|**Teuken-7B-Instruct**|7B|⭐⭐⭐⭐⭐|⭐⭐⭐⭐½|**European-language specialist**|
|**Salamandra-7B-Instruct**|7B|⭐⭐⭐⭐⭐|⭐⭐⭐⭐½|**Spanish/Catalan + European languages**|
|**Gemma 3 4B**|4B|⭐⭐⭐⭐½|⭐⭐⭐⭐⭐|Lightweight conversational partner|
|**Aya-23 8B**|8B|⭐⭐⭐⭐⭐|⭐⭐⭐⭐⭐|Excellent multilingual alternative|

### My recommendation for you

I'd test **three models**:

**1. Qwen2.5-7B-Instruct**  
Best starting point if you want one model that can also handle your Italian, Portuguese and English.

**2. Teuken-7B-Instruct**  
This is particularly interesting for you because it's designed around **European languages**. It was evaluated specifically across Spanish, Italian, Portuguese, Polish and other European languages. In a recent evaluation, Teuken-7B-Instruct scored **58.5% average across ten common European languages**, ahead of Aya-23 8B and Salamandra-7B-Instruct on that aggregate. ([Sage Journals](https://journals.sagepub.com/doi/10.3233/FAIA251328?utm_source=chatgpt.com "Teuken-7B-Base & Teuken-7B-Instruct: Towards European LLMs, 2026"))

**3. Salamandra-7B-Instruct**  
I'd definitely try this one if you want something more explicitly oriented toward European/Spanish-language use. Salamandra was trained on **35 languages**, and its instruction model was trained using instructions in English, Spanish and Catalan. ([Sage Journals](https://journals.sagepub.com/doi/10.3233/FAIA251328?utm_source=chatgpt.com "Teuken-7B-Base & Teuken-7B-Instruct: Towards European LLMs, 2026"))

---

### Something particularly relevant to you

Because you speak **Spanish around B2**, I'd actually prefer a model that can do **natural conversation rather than simply Spanish QA**.

I'd give it a prompt like:

```text
You are my Spanish conversation partner.

I am approximately B2 level in Spanish.

Speak naturally, like a Spanish-speaking friend, rather than like a language textbook.

Keep the conversation mostly in Spanish.

When I make a significant grammatical or vocabulary mistake:
- briefly show my corrected sentence
- explain the mistake in English
- continue the conversation in Spanish

Don't correct every tiny mistake because I want to develop fluency.

Use natural conversational expressions and occasionally introduce useful vocabulary.

Ask follow-up questions so that the conversation doesn't stop.
```

Then I'd create **three modes**:

**🇪🇸 Casual conversation**

> Talk to me as a Spanish friend. Don't correct me unless I make a significant mistake.

**🎓 B2 tutor**

> Correct my mistakes and explain why, but keep the conversation flowing.

**🔥 Immersion**

> Spanish only. No English unless I explicitly ask for an explanation.

---

### One model I'd particularly investigate: Teuken

For your situation, **Teuken-7B-Instruct is more interesting than it initially looks**.

The published evaluation specifically includes **Spanish, Italian and Portuguese**, which makes it attractive if you want one local model for your European-language practice. Its authors report particularly strong multilingual robustness compared with similarly sized models. ([Sage Journals](https://journals.sagepub.com/doi/10.3233/FAIA251328?utm_source=chatgpt.com "Teuken-7B-Base & Teuken-7B-Instruct: Towards European LLMs, 2026"))

So you could potentially have:

```text
                    Teuken 7B
                       │
       ┌───────────────┼───────────────┐
       ↓               ↓               ↓
    Spanish          Italian       Portuguese
      B2               B1              A2
```

That is probably more useful to you than maintaining a completely different LLM for every language.

### If you want the fastest model

I'd try **Gemma 3 4B**. It should be considerably easier to run on your 16 GB machines while still being capable of natural multilingual conversation.

### If you want the best quality and don't mind >7B

I'd move to **Qwen3-8B** or **Aya-23 8B**. The extra 1B parameter isn't enormous, and for conversational language practice it can be worthwhile.

**My personal testing order for your setup would be:**

**Teuken-7B-Instruct → Qwen2.5-7B-Instruct → Salamandra-7B-Instruct → Gemma 3 4B**

That would also give you a nice experiment: **European-language specialist vs general multilingual model vs Spanish/Catalan-oriented model vs small efficient model.**

# Brazilian Portuguese
For **Brazilian Portuguese specifically**, I'd change the shortlist a little compared with Spanish and Italian. There are some genuinely interesting **PT-BR-focused models**, but some of the older ones are no longer the best conversational models.

### My shortlist for you

|Model|Size|PT-BR|Conversation|My use|
|---|--:|---|---|---|
|**Qwen3 8B**|8B|⭐⭐⭐⭐⭐|⭐⭐⭐⭐⭐|**Best general choice**|
|**Teuken-7B-Instruct**|7B|⭐⭐⭐⭐⭐|⭐⭐⭐⭐½|Best ≤7B multilingual option|
|**Sabiá-7B**|7B|⭐⭐⭐⭐⭐|⭐⭐⭐|PT-BR specialist, but old|
|**Qwen2.5-7B-Instruct**|7B|⭐⭐⭐⭐⭐|⭐⭐⭐⭐½|Excellent fallback|
|**Manacá-1B**|1.7B|⭐⭐⭐⭐|⭐⭐⭐|Very lightweight PT-BR experiment|
|**Tucano-2.4B**|2.4B|⭐⭐⭐⭐|⭐⭐⭐|Lightweight Brazilian model|

### 🥇 If you're willing to go slightly above 7B: Qwen3 8B

This is probably what I'd use for **actual conversation practice**.

A recent 2026 comparison specifically focused on local LLMs for Brazilian Portuguese and identifies **Qwen3 8B** as a strong local PT-BR choice, with good Brazilian vocabulary and grammar. ([PromptQuorum](https://www.promptquorum.com/pt/local-llms/best-local-llms-portuguese-language-2026?utm_source=chatgpt.com "Melhores LLMs locais para português do Brasil 2026: Qwen3, Sabiá e mais"))

The 1B difference from your ≤7B requirement is relatively insignificant in practical terms. If your machine can comfortably run a 7B Q4 model, it should be worth trying the 8B Q4 version too.

For Ollama, assuming the model is available in your current Ollama catalogue:

```bash
ollama pull qwen3:8b
```

---

## 🇧🇷 If you want to stay strictly ≤7B: Teuken-7B

This is actually the model I'd be most interested in **for you personally**, because you are learning several European languages.

Teuken-7B-Instruct is designed specifically for European languages and its evaluation includes **Portuguese, Spanish, Italian and Polish**, among others. In its published comparison across ten European languages, Teuken-7B-Instruct had a **58.5% average**, ahead of Aya-23 8B and Salamandra-7B-Instruct on that particular benchmark. ([Sage Journals](https://journals.sagepub.com/doi/10.3233/FAIA251328?utm_source=chatgpt.com "Teuken-7B-Base & Teuken-7B-Instruct: Towards European LLMs, 2026"))

That makes it potentially very useful as a **single language-learning LLM**:

```text
             Teuken 7B
                 │
      ┌──────────┼──────────┐
      ↓          ↓          ↓
 Portuguese    Spanish    Italian
   A2            B2          B1
```

I particularly like that setup for you because you don't need a separate 7B model for every language.

---

## 🇧🇷 Sabiá-7B — interesting, but I'd treat it as an experiment

**Sabiá** is one of the most important Brazilian Portuguese-specific open models. It was developed by Maritaca AI and is specifically trained for Portuguese. Its published Portuguese evaluation substantially outperformed LLaMA-1 7B and LLaMA-2 7B on its Poeta benchmark. ([Hugging Face](https://huggingface.co/maritaca-ai/sabia-7b/blob/main/README.md?utm_source=chatgpt.com "README.md · maritaca-ai/sabia-7b at main"))

However, there's an important catch:

**Sabiá-7B is an older model and is a base model rather than a modern instruction/chat model.** Its own model card explicitly says it was trained solely with a language-modelling objective rather than instruction tuning. ([Hugging Face](https://huggingface.co/maritaca-ai/sabia-7b/blob/refs%2Fpr%2F5/README.md?utm_source=chatgpt.com "README.md · maritaca-ai/sabia-7b at refs/pr/5"))

So I wouldn't choose it over Qwen3/Teuken for a conversational tutor.

It's still fascinating to try if you're interested in seeing how a **Brazilian-native language model** behaves.

---

# 🇧🇷 There is also a really interesting tiny model: Manacá

This one caught my attention because you're interested in running models on relatively modest hardware.

**Manacá-1B** is an open Brazilian-Portuguese model developed by LNCC. Despite being only around **1.72B parameters**, its August 2026 evaluation reports a **60.63% CALAME-PT score**, compared with 63.23% for Sabiá-7B. ([GitHub](https://github.com/Instituto-IA-LNCC/manaca-1b-base/blob/main/docs/evaluation/manaca-1b-base-eval-pt.md?utm_source=chatgpt.com "manaca-1b-base/docs/evaluation/manaca-1b-base-eval-pt.md at main · Instituto-IA-LNCC/manaca-1b-base · GitHub"))

That's not a conversational benchmark, so I wouldn't conclude that it's a better chatbot. But it's impressive evidence that a much smaller model can have very good **Brazilian Portuguese language modelling**.

For a low-powered laptop, I'd definitely experiment with it.

---

# What I'd actually install

Given your existing **Ollama + Open WebUI** setup, I'd make a little language-learning collection:

```text
Qwen3 8B
   ↓
Best overall conversation

Teuken 7B
   ↓
European-language conversation

Manacá 1.7B
   ↓
Very lightweight Brazilian Portuguese
```

And then compare them using **your actual A2-level conversations**, rather than benchmark scores.

For example, give all three:

> _Oi! Meu nome é Lukasz. Estou aprendendo português brasileiro e quero praticar conversação. Hoje trabalhei bastante e estou cansado. E você, como foi seu dia?_

Then see which one:

- responds naturally in **Brazilian**, not European Portuguese
    
- uses appropriate A2 vocabulary
    
- doesn't constantly switch to English
    
- asks sensible follow-up questions
    
- understands imperfect Portuguese
    
- corrects mistakes without killing the conversation
    
- uses natural Brazilian expressions
    

That last point is particularly important.

---

## I'd configure your tutor differently for A2

Since your Brazilian Portuguese is around **A2**, I wouldn't ask it to simply "speak Brazilian Portuguese."

I'd use:

```text
You are my Brazilian Portuguese conversation partner.

I am an A2 learner of Brazilian Portuguese.

Speak naturally but keep your vocabulary mostly within A1-A2.
Occasionally introduce one useful B1 expression.

Use Brazilian Portuguese, not European Portuguese.

Keep your responses relatively short so I have plenty of opportunity to speak.

Ask me questions and keep the conversation moving.

When I make a mistake:
1. Let me finish my thought.
2. Give me the corrected version briefly.
3. Explain the mistake in English only when necessary.
4. Continue speaking Portuguese.

Do not correct every minor mistake.
Prioritise mistakes that would sound unnatural or cause misunderstanding.

Do not translate everything into English.
```

For A2, **short responses are particularly important**. Otherwise you'll end up spending more time reading the LLM than actually producing Portuguese yourself.

### One additional thought

For **Brazilian Portuguese specifically**, I'd actually put **Qwen3 8B vs Teuken 7B** at the top of your test.

And because you're also learning Spanish and Italian, I'd be tempted to use **one Teuken model for all three languages**, then compare it against Qwen3. That could give you a very nice **local multilingual language tutor** without needing three separate models. ([Sage Journals](https://journals.sagepub.com/doi/10.3233/FAIA251328?utm_source=chatgpt.com "Teuken-7B-Base & Teuken-7B-Instruct: Towards European LLMs, 2026"))

# my installations:
PS C:\Users\slotw> ollama pull mistral:7b
pulling manifest
pulling f5074b1221da: 100% ▕██████████████████████████████████████████████████████████▏ 4.4 GB
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama pull  qwen3:1.7b
pulling manifest
pulling 3d0b790534fe: 100% ▕██████████████████████████████████████████████████████████▏ 1.4 GB
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama pull  qwen3:4b qwen3:8b
Error: accepts 1 arg(s), received 2
PS C:\Users\slotw> ollama pull  qwen3:4b
pulling manifest
pulling 3e4cb1417446: 100% ▕█████████████████████████████████████████████████████████ ▏ 2.5 GB/2.5 GB   72 MB/s      0s
pulling d18a5cc71b84: 100% ▕██████████████████████████████████████████████████████████▏  11 KB
pulling cff3f395ef37: 100% ▕██████████████████████████████████████████████████████████▏  120 B
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama pull  qwen3:8b
pulling manifest
pulling a3de86cd1c13: 100% ▕██████████████████████████████████████████████████████████▏ 5.2 GB
pulling ae370d884f10: 100% ▕██████████████████████████████████████████████████████████▏ 1.7 KB
pulling d18a5cc71b84: 100% ▕██████████████████████████████████████████████████████████▏  11 KB
pulling cff3f395ef37: 100% ▕██████████████████████████████████████████████████████████▏  120 B
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama pull qwen2.5-coder:3b
pulling manifest
pulling 4a188102020e: 100% ▕██████████████████████████████████████████████████████████▏ 1.9 GB
pulling 66b9ea09bd5b: 100% ▕██████████████████████████████████████████████████████████▏   68 B
pulling 1e65450c3067: 100% ▕██████████████████████████████████████████████████████████▏ 1.6 KB
pulling 45fc3ea7579a: 100% ▕██████████████████████████████████████████████████████████▏ 7.4 KB
pulling bb967eff3bda: 100% ▕██████████████████████████████████████████████████████████▏  487 B
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama pull qwen2.5-coder:7b
pulling manifest
pulling 60e05f210007: 100% ▕██████████████████████████████████████████████████████████▏ 4.7 GB
pulling 66b9ea09bd5b: 100% ▕██████████████████████████████████████████████████████████▏   68 B
pulling 1e65450c3067: 100% ▕██████████████████████████████████████████████████████████▏ 1.6 KB
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama pull qwen2.5-coder:1.5b
pulling manifest
pulling 29d8c98fa6b0: 100% ▕█████████████████████████████████████████████████████████ ▏ 982 MB/986 MB   80 MB/s      0s
pulling 66b9ea09bd5b: 100% ▕██████████████████████████████████████████████████████████▏   68 B
pulling 1e65450c3067: 100% ▕██████████████████████████████████████████████████████████▏ 1.6 KB
pulling 832dd9e00a68: 100% ▕██████████████████████████████████████████████████████████▏  11 KB
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama pull qwen2.5:1.5b
pulling manifest
pulling 183715c43589: 100% ▕██████████████████████████████████████████████████████████▏ 986 MB
pulling 66b9ea09bd5b: 100% ▕██████████████████████████████████████████████████████████▏   68 B
pulling eb4402837c78: 100% ▕██████████████████████████████████████████████████████████▏ 1.5 KB
pulling 832dd9e00a68: 100% ▕██████████████████████████████████████████████████████████▏  11 KB
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama pull qwen2.5:3b
pulling manifest
pulling 5ee4f07cdb9b: 100% ▕██████████████████████████████████████████████████████████▏ 1.9 GB
pulling 66b9ea09bd5b: 100% ▕██████████████████████████████████████████████████████████▏   68 B
pulling eb4402837c78: 100% ▕██████████████████████████████████████████████████████████▏ 1.5 KB
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama pull qwen2.5:7b
pulling manifest
pulling 2bada8a74506: 100% ▕██████████████████████████████████████████████████████████▏ 4.7 GB
pulling 66b9ea09bd5b: 100% ▕██████████████████████████████████████████████████████████▏   68 B
pulling eb4402837c78: 100% ▕██████████████████████████████████████████████████████████▏ 1.5 KB
pulling 832dd9e00a68: 100% ▕██████████████████████████████████████████████████████████▏  11 KB
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama list
NAME                  ID              SIZE      MODIFIED
qwen2.5:7b            845dbda0ea48    4.7 GB    18 seconds ago
qwen2.5:3b            357c53fb659c    1.9 GB    About a minute ago
qwen2.5:1.5b          65ec06548149    986 MB    2 minutes ago
qwen2.5-coder:1.5b    d7372fd82851    986 MB    2 minutes ago
qwen2.5-coder:7b      dae161e27b0e    4.7 GB    4 minutes ago
qwen2.5-coder:3b      f72c60cabf62    1.9 GB    5 minutes ago
qwen3:8b              500a1f067a9f    5.2 GB    8 minutes ago
qwen3:4b              359d7dd4bcda    2.5 GB    9 minutes ago
qwen3:1.7b            8f68893c685c    1.4 GB    11 minutes ago
mistral:7b            6577803aa9a0    4.4 GB    13 minutes ago
gemma4:latest         c6eb396dbd59    9.6 GB    7 days ago
mario:latest          ee525fe529e2    2.0 GB    2 weeks ago
llama3.2:latest       a80c4f17acd5    2.0 GB    2 weeks ago
llama2:latest         78e26419b446    3.8 GB    2 weeks ago
PS C:\Users\slotw> ollama pull gemma4:e2b
pulling manifest
pulling 4e30e2665218: 100% ▕█████████████████████████████████████████████████████████ ▏ 7.2 GB/7.2 GB  7.5 MB/s      0s
pulling 7339fa418c9a: 100% ▕██████████████████████████████████████████████████████████▏  11 KB
pulling 56380ca2ab89: 100% ▕██████████████████████████████████████████████████████████▏   42 B
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama pull gemma4:e4b
pulling manifest
pulling 4c27e0f5b5ad: 100% ▕██████████████████████████████████████████████████████████▏ 9.6 GB
pulling 7339fa418c9a: 100% ▕██████████████████████████████████████████████████████████▏  11 KB
pulling 56380ca2ab89: 100% ▕██████████████████████████████████████████████████████████▏   42 B
pulling f0988ff50a24: 100% ▕██████████████████████████████████████████████████████████▏  473 B
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama list
NAME                  ID              SIZE      MODIFIED
gemma4:e4b            c6eb396dbd59    9.6 GB    12 seconds ago
gemma4:e2b            7fbdbf8f5e45    7.2 GB    20 seconds ago
qwen2.5:7b            845dbda0ea48    4.7 GB    5 minutes ago
qwen2.5:3b            357c53fb659c    1.9 GB    6 minutes ago
qwen2.5:1.5b          65ec06548149    986 MB    7 minutes ago
qwen2.5-coder:1.5b    d7372fd82851    986 MB    7 minutes ago
qwen2.5-coder:7b      dae161e27b0e    4.7 GB    8 minutes ago
qwen2.5-coder:3b      f72c60cabf62    1.9 GB    10 minutes ago
qwen3:8b              500a1f067a9f    5.2 GB    12 minutes ago
qwen3:4b              359d7dd4bcda    2.5 GB    14 minutes ago
qwen3:1.7b            8f68893c685c    1.4 GB    15 minutes ago
mistral:7b            6577803aa9a0    4.4 GB    18 minutes ago
gemma4:latest         c6eb396dbd59    9.6 GB    7 days ago
llama3.2:latest       a80c4f17acd5    2.0 GB    2 weeks ago
mario:latest          ee525fe529e2    2.0 GB    2 weeks ago
llama2:latest         78e26419b446    3.8 GB    2 weeks ago
PS C:\Users\slotw> ollama pull LLaMAntino-3-ANITA:8b
pulling manifest
Error: pull model manifest: file does not exist
PS C:\Users\slotw> ollama run mannix/llamax3-8b-alpaca
pulling manifest
pulling fd08dd84c687: 100% ▕██████████████████████████████████████████████████████████▏ 4.7 GB
pulling ec8a066fd4f1: 100% ▕██████████████████████████████████████████████████████████▏  110 B
verifying sha256 digest
writing manifest
success
>>> /quit
Unknown command '/quit'. Type /? for help
>>> /exit
PS C:\Users\slotw> ollama pull hf.co/mradermacher/zefiro-7b-sft-qlora-ITA-v0.5-GGUF:Q4_K_M
pulling manifest
pulling e923957a7afe: 100% ▕██████████████████████████████████████████████████████████▏ 4.4 GB
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama list
NAME                                                           ID              SIZE      MODIFIED
hf.co/mradermacher/zefiro-7b-sft-qlora-ITA-v0.5-GGUF:Q4_K_M    9ca59c24ad06    4.4 GB    9 minutes ago
mannix/llamax3-8b-alpaca:latest                                9ef0a226d383    4.7 GB    15 minutes ago
gemma4:e4b                                                     c6eb396dbd59    9.6 GB    16 hours ago
gemma4:e2b                                                     7fbdbf8f5e45    7.2 GB    16 hours ago
qwen2.5:7b                                                     845dbda0ea48    4.7 GB    16 hours ago
qwen2.5:3b                                                     357c53fb659c    1.9 GB    16 hours ago
qwen2.5:1.5b                                                   65ec06548149    986 MB    16 hours ago
qwen2.5-coder:1.5b                                             d7372fd82851    986 MB    16 hours ago
qwen2.5-coder:7b                                               dae161e27b0e    4.7 GB    16 hours ago
qwen2.5-coder:3b                                               f72c60cabf62    1.9 GB    16 hours ago
qwen3:8b                                                       500a1f067a9f    5.2 GB    16 hours ago
qwen3:4b                                                       359d7dd4bcda    2.5 GB    16 hours ago
qwen3:1.7b                                                     8f68893c685c    1.4 GB    16 hours ago
mistral:7b                                                     6577803aa9a0    4.4 GB    16 hours ago
gemma4:latest                                                  c6eb396dbd59    9.6 GB    8 days ago
llama3.2:latest                                                a80c4f17acd5    2.0 GB    2 weeks ago
mario:latest                                                   ee525fe529e2    2.0 GB    2 weeks ago
llama2:latest                                                  78e26419b446    3.8 GB    2 weeks ago
PS C:\Users\slotw> ollama delete mannix/llamax3-8b-alpaca:latest
Error: unknown command "delete" for "ollama"
PS C:\Users\slotw> ollama rm mannix/llamax3-8b-alpaca:latest
deleted 'mannix/llamax3-8b-alpaca:latest'
PS C:\Users\slotw> ollama pull swap-uniba/LLaMAntino-3-ANITA-8B-Inst-DPO-ITA
Error: pull model manifest: file does not exist
PS C:\Users\slotw> ollama pull hf.co/mradermacher/LLaMAntino-3-ANITA-8B-Inst-DPO-ITA-GGUF:Q4_K_M
pulling manifest
pulling f3e8ef4af73c: 100% ▕█████████████████████████████████████████████████████████ ▏ 4.9 GB/4.9 GB   18 MB/s      0s
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama pull vaiton/minerva:3b-base-Q8_0
pulling manifest
pulling e1890e40c92e: 100% ▕█████████████████████████████████████████████████████████ ▏ 3.1 GB/3.1 GB   19 MB/s      0s
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama pull olfh/teuken-7b-instruct-commercial-v0.4:7b
pulling manifest
pulling d3179debc827: 100% ▕██████████████████████████████████████████████████████████▏ 5.0 GB
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama pull cas/salamandra-7b-instruct:7b
pulling manifest
Error: pull model manifest: file does not exist
PS C:\Users\slotw> ollama pull cas/salamandra-7b-instruct:8b
pulling manifest
Error: pull model manifest: file does not exist
PS C:\Users\slotw> ollama pull cas/salamandra-7b-instruct
pulling manifest
pulling bac8e8c1d1d9: 100% ▕█████████████████████████████████████████████████████████ ▏ 4.9 GB/4.9 GB   19 MB/s      0s
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama pull aya-expanse:8b
pulling manifest
pulling d1ee5fdcfdb2: 100% ▕██████████████████████████████████████████████████████████▏ 5.1 GB
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama pull hf.co/QuantFactory/sabia-7b-GGUF:Q4_K_M
pulling manifest
pulling 087e6a8bdc2b: 100% ▕██████████████████████████████████████████████████████████▏ 4.1 GB
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama pull hf.co/mradermacher/manaca-1b-base-i1-GGUF:Q4_K_M
pulling manifest
pulling 8d70223f34b0: 100% ▕██████████████████████████████████████████████████████████▏ 1.1 GB
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw> ollama pull cnmoro/tucano-2b4-instruct:q4_k_m
pulling manifest
pulling dc910e6efaae: 100% ▕█████████████████████████████████████████████████████████ ▏ 1.5 GB/1.5 GB   18 MB/s      0s
verifying sha256 digest
writing manifest
success
PS C:\Users\slotw>


---
[ollama - main](https://github.com/slotwek/ollama_AI/blob/main/ollama%20-%20main.md)