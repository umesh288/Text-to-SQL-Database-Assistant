# Text-to-SQL Employee Database Agent

Ask questions about an employee database in natural language. This project uses a LangChain agent and a local Qwen3 model served by Ollama to generate, validate, and run read-only SQLite queries, then return the results in a clear response.

> Despite “MySQL” in the notebook filename, the notebook connects to a **SQLite** database.

## Features

- Retrieves database schema to inform query generation
- Converts questions into SQLite `SELECT` queries
- Checks queries before execution and blocks common write or schema-changing operations
- Attempts to correct failed queries
- Supports interactive command-line questions

## Requirements

- Python
- [Ollama](https://ollama.com/) running locally at `http://localhost:11434`
- Qwen3 model `qwen3:0.6b`
- Employee SQLite database at `db/employees_db-full-1.0.6.db`

Install the Python packages:

```bash
pip install -U langchain langchain-ollama langchain-community langchain-core
```

Download the model:

```bash
ollama pull qwen3:0.6b
```

## Run

Open and run `Text to MySQL Agent.ipynb` in Jupyter. Make sure the SQLite database is available at the path configured in the notebook. The final cell starts an interactive chat; enter a question such as:

```text
What is the average salary of employees in the Sales department?
```

Enter `quit`, `q`, or `exit` to stop.

## How it works

1. Reads the database schema.
2. Generates a SQL query from the user's question.
3. Validates that the query is read-only.
4. Executes the query against SQLite.
5. Returns an answer, attempting to fix query errors when needed.

## Tech stack

Python · LangChain · Ollama · Qwen3 · SQLite · SQL
