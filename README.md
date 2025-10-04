# Retrieval-Augmented Code Generation (RAG for Programming Tasks)

This project implements a **Retrieval-Augmented Generation (RAG)** system that takes a **natural language programming task** and generates Python code using **retrieved HumanEval examples** as context.  
It retrieves semantically similar programming problems, builds a contextual prompt, and feeds it into a code-generation model to produce the solution.

---

## 🚀 Features

- Loads and processes the **HumanEval dataset** (`openai/openai_humaneval`)
- Embeds task descriptions using `SentenceTransformer`
- Stores and retrieves examples using **FAISS** (vector search)
- Builds a context-aware prompt for the model
- Generates Python code using **DeepSeek Coder 1.3B-Instruct**

---

## 🧩 Pipeline Overview

1. **Dataset Preparation**
   - Loads HumanEval dataset
   - Extracts task ID, prompt, and canonical solution

2. **Embedding**
   - Encodes all prompts into vectors using `all-MiniLM-L6-v2`
   - Normalizes embeddings and stores them in FAISS index

3. **Retrieval**
   - Retrieves top-k similar examples for a given new task

4. **Prompt Construction**
   - Combines retrieved examples + new task into a formatted prompt

5. **Code Generation**
   - Uses DeepSeek Coder 1.3B-Instruct model to generate a Python solution

---

## 🛠️ Installation

```bash
git clone https://github.com/raniramez/rag-code-generator.git
cd rag-code-generator
pip install -r requirements.txt
```

---

## ▶️ Usage

```bash
python Main.py
```

Then enter your coding problem when prompted, for example:

```
Enter your coding task: Write a function that returns True if a string is a palindrome.
```

Output:

```
--- Generated Code ---
def is_palindrome(s: str) -> bool:
    return s == s[::-1]
```

---

## ⚙️ Model Info

- **Retriever:** `sentence-transformers/all-MiniLM-L6-v2`
- **Generator:** `deepseek-ai/deepseek-coder-1.3b-instruct`
- Runs on CPU or GPU automatically.

---

## 📚 Example Prompt Structure

```
### Examples
### Task: HumanEval_1
def add(a, b): return a + b

### New Task
Write a function to compute factorial recursively.

### Your Python solution:
```

---

## 📁 Project Structure
```
├── Main.py
├── requirements.txt
└── README.md
```

---

## 💡 Future Improvements

- Integrate caching for embeddings  
- Evaluate generation quality against HumanEval test cases  
- Add support for multiple retrievers or model comparison

---

## 👤 Author
**Rani Ramez**  
Mechatronics & AI Engineering | Ain Shams University  
📧 Contact: [LinkedIn](https://www.linkedin.com/in/raniramez)
