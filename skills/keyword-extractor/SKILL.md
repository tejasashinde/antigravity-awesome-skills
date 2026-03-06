---
name: keyword-extractor
description: >
  Extracts max 50 highly relevant keywords for given text. Use when user asks to extract keywords, generate SEO keywords, create tags, identify key terms, list topic keywords, produce metadata tags from csv and any text.
---

# Keyword Extractor

Extracts **max 50 relevant keywords** from provided text and formats them in a strict, machine-ready structure.

## CORE MANDATE

The output **must contain max 50 keywords** and must follow every rule below:
- Keywords must be **separated by commas**
- Keywords must be **ordered by relevance**
- All keywords must be in **lowercase**
- **Do not repeat** any keyword
- Use **short-tail keywords (single words) and long-tail keywords (2–4 word phrases)**
- **Do not include numbering**
- **Do not include explanations**
- **Do not include bullet points**
- **Do not end the output with a period**

Return **only the keyword line**.

## Keyword Quality Rules

Prefer keywords that are useful for search, tagging, and SEO.
Prioritize keywords that are:
- specific concepts
- domain terminology
- meaningful search phrases
- natural keyword queries
- descriptive long-tail keywords

Avoid weak or generic keywords such as:
- things  
- various topics  
- important concepts  
- general information  
- different methods  

Keywords must represent **clear searchable topics**, not vague words.

---

## INPUT MODES

Supports two modes:

### Mode 1 — Inline Text

User provides text directly.

Example: extract keywords from this paragraph: "machine learning is transforming healthcare..."

### Mode 2 — CSV File Processing

User provides a `.csv` file containing text in one or more columns.

STEPS:
1. Read the CSV file.
2. Identify the column containing the source text.
3. For each row, extract the text content.
4. Run the keyword extraction workflow below.
5. Edit the same file and create a **new column named `keywords`**.
6. Store the generated comma-separated keyword list for that row in the `keywords` column.
7. Preserve all existing columns and data.
8. Save or return the **updated CSV file with the new `keywords` column added**.

---

## WORKFLOW

### 1. Analyze the Text

Identify the most important elements in the input:
- main subject
- key topics
- technical terminology
- domain concepts
- entities
- meaningful nouns
- important phrases

Ignore filler words and stopwords.

### 2. Generate Candidate Keywords

Smartly create a pool of **60-80 potential keywords**.

Candidates should include:
- primary topics
- secondary topics
- technical vocabulary
- domain terminology
- related concepts

Allow both short-tail keywords (single words) and long-tail keywords (2–4 word phrases).

Valid examples:
machine learning, data science, supply chain management, neural networks training, cloud computing

Avoid long descriptive phrases.

### 3. Rank by Relevance

Prioritize keywords in this order:
1. core subject
2. primary concepts
3. domain terminology
4. supporting topics
5. contextual terms

The most important keywords must appear first.

### 4. Select the Top 50

From the ranked candidates:
- Keep **max 50 keywords**
- remove duplicates
- remove near-duplicates
- avoid repeating synonyms with the same meaning

Example conflict: ai, artificial intelligence

Choose **only one** if both represent the same concept.

### 5. Normalize Formatting

Before producing output, enforce formatting rules:
- all keywords **lowercase**
- **comma-separated**
- **no numbering**
- **no bullet points**
- **no punctuation at the end**
- **no extra commentary**

Correct example: machine learning, neural networks, reinforcement learning

Incorrect examples:
1. machine learning  
- neural networks  
machine-learning.

### 6. Validate Output

Before returning the result, verify:

- total keywords ≤ **50**
- **no duplicates exist**
- **all are lowercase**
- **comma-separated**
- **no explanations**
- **no trailing period**

If any rule fails, **regenerate the list**.

## OUTPUT FORMAT

Return **one single comma-seperated line**:

keyword1, keyword2, keyword3, keyword4, ...keyword50

## CSV OUTPUT RULE

When operating in **CSV File Processing mode**:

- Do not print keywords as plain text.
- Insert the generated keywords into a **new column named `keywords`**.
- Each row must contain its own keyword list.
- Keywords must remain **comma-separated within the cell**.
- Do not modify or remove existing columns.

## FAILURE HANDLING

If the input text is extremely short:
- infer likely keywords from context
- still produce **max 50 keywords**

Never output more than 50.

---