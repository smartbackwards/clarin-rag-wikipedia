# RAG over Wikipedia with Polish and open language models

The RAG part of a university NLP project (Wrocław University of Science and Technology, 2025), extracted from a group
assignment. It answers English questions from a Wikipedia index and compares three language models on the same
retrieved context.

## What it does

1. Loads a FAISS index of Wikipedia (July 2023 snapshot, from Kaggle: `jjinho/wikipedia-2023-07-faiss-index`).
2. Embeds the question with `sentence-transformers/all-MiniLM-L6-v2` and retrieves the top documents.
3. Passes the documents and the question to a model served by the CLARIN-PL chat API, through a small LangChain
   wrapper (`ClarinChatLLM`).
4. Compares **Bielik**, **PLLuM** and **Llama** on the same questions.

## Files

| Path | Contents |
|---|---|
| `clarin_rag.ipynb` | The whole pipeline, with outputs |
| `results/<model>_en_questions/` | One JSON per question: query, answer, retrieved documents, metadata (`bielik`, `llama`, `pllum`) |

## What we saw

A short, subjective read of ten questions (notes in the notebook are in Polish):

- Llama gave short, on-topic answers.
- Bielik gave longer, well-structured answers.
- PLLuM often copied Wikipedia text, or lost track of the question on factual comparisons.

This was a class exercise on ten questions, not a benchmark.

## Running it

The notebook was run locally on Windows. It needs `faiss-cpu`, `sentence-transformers`, `langchain-core`, `pandas`
and `kagglehub`, plus the index and article files it reads (see the first cells).

You need your own CLARIN-PL API token. Set it in the environment before running:

```bash
export CLARIN_API_TOKEN="your-token"
```

No token is stored in this repository.
