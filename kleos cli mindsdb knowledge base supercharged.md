  <img src="https://media2.dev.to/dynamic/image/width=1000,height=420,fit=cover,gravity=auto,format=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fogya8bivno1987lrftc3.jpeg" alt="Cover Image" />
  <hr />
  
  # Kleos CLI: Mindsdb Knowledge Base supercharged
  
  **Tags:** `ai`, `python`, `programming`, `agentaichallenge`

  **Published At:** 6/30/2025, 8:46:51 AM

  **URL:** [https://dev.to/yashksaini/kleos-cli-mindsdb-knowledge-base-supercharged-1a83](https://dev.to/yashksaini/kleos-cli-mindsdb-knowledge-base-supercharged-1a83)

  <hr />
  Okh so lets begin with the important context, currently there is constant evolution going on in the world of AI agents, and there is large amount of unstructured raw data which keeps on increasing, developers need to constantly simplify complex data and accelerate AI workflows to manage this whole data, so they seek help from  tools and frameworks that can make thier task easy. With many different database sources, and formats available storing them, managing them and running SQL queries to use them. All of this is very tedious work, one that requires accuracy and fast results.

The perfect solution for this, is the new [Knowledge Base](https://docs.mindsdb.com/mindsdb_sql/knowledge-bases) :- an an advance system that organizes data with its actual meaning not by just cross matching the frequent words or important keywords. 

- MindsDB's new Knowledge Base organizes data by its actual meaning, not just by the keywords or frequent words matching

- It Supports semantic search with context-aware retrieval

- Handles various data sources like databases, CSV, text, and many other integrations like Youtube, [Hackernews](https://news.ycombinator.com/)

- Utilizes embedding models, re-ranking models, and vector stores to create embeddings to provide context data retrieval.

- Enables intelligent querying and meaningful data discovery

{% embed https://www.youtube.com/watch?v=lfkm1IUKwOQ %}
 
To make interacting with MindsDB's powerful features even more intuitive and efficient, especially its cutting-edge Knowledge Base and AI Agent functionalities, I developed **[Kleos](https://github.com/yashksaini-coder/Kleos)**. Kleos (a greek word which summaries, _The enduring transmission of meaningful, wise knowledge — curated, remembered, and used across time._) is a Python-based async command-line interface designed to be your trusty companion for using the MindsDB Knowledge Base.

Every system has its `telos` — its final cause or purpose. This CLI fulfills the purpose of MindsDB's Knowledge Base: to seek, structure, and serve insight through intelligent agents. Kleos aims to streamline the process of building and managing these intelligent systems directly from your terminal.

This article will walk you through Kleos CLI, highlighting its key features and demonstrating how it leverages MindsDB KB to help you build powerful AI-driven applications with ease.

## Core Philosophy: SQL as the Language of AI

One of MindsDB's foundational principles, which Kleos has integrated at root level, is the use of SQL as the primary language for AI development. Instead of requiring developers to learn complex machine learning libraries or manage separate MLOps pipelines for many common tasks, MindsDB allows you to:

*   **Connect to diverse data sources:** From your existing databases to SaaS applications and file storages.
*   **Create AI Models:** Train models for tasks like classification, regression, time series forecasting, and even interact with large language models (LLMs) for generative tasks.
*   **Build Knowledge Bases:** Create semantic search capabilities over your textual data.
*   **Deploy AI Agents:** Combine LLMs with your data and KBs to create intelligent assistants.
*   **Query Predictions and Insights:** Fetch predictions and insights as if you were querying a regular database table.

All of this achieved by using SQL extensions. Kleos CLI acts as a convenient and powerful interface to execute these SQL commands, manage your MindsDB resources, and automate workflows, making the power of in-database AI more accessible than ever. We've built Kleos using Python, [Click](https://click.palletsprojects.com/) for robust command-line parsing, and [Rich](https://rich.readthedocs.io/) for beautiful, informative terminal output.

# What Kleos can do!

![Kleos Commands](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/4o3yu855eqqc35ikh7kh.jpeg)

### Key Features of Kleos & MindsDB in Action

Kleos provides a comprehensive suite of commands to manage various aspects of your MindsDB environment. Here’s a look at some core functionalities:

### 1. Seamless Setup (`kleos setup`)

Getting started often involves connecting to your data. MindsDB excels at integrating with numerous data sources. Kleos helps you quickly set up common datasources. For instance, the HackerNews datasource, a popular source for real-time discussions and articles, can be configured with a single command:

```bash
kleos setup hackernews --name my_hackernews_data
```

![Kleos Setup](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gy4py31t1vh46qqyu2bj.jpeg)

This simple command tells MindsDB to create a connection named `my_hackernews_data` that can query HackerNews directly. Kleos ensures this process is smooth, even creating the datasource if it doesn't already exist when you try to use it in other commands.

### 2. Knowledge Bases (KBs) - The Heart of Kleos (`kleos kb ...`)

Knowledge Bases are a cornerstone of MindsDB's recent advancements, allowing you to embed and search large volumes of text data semantically. Kleos provides extensive support for managing KBs.


![Kleos KB](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/szyu89z9cu209hfqbymw.jpeg)

**a. Creating Knowledge Bases (`kleos kb create`)**

You can easily create a new KB, specifying the underlying embedding models (to convert text to vectors) and optional reranking models (to improve search result relevance). Kleos supports models from various providers like Ollama (for local LLMs) and Google Gemini.

```bash
# Create a KB using a local Ollama model for embeddings and google gemini for reranking model

kleos kb create gemini_ollama_kb --embedding-provider ollama --embedding-model nomic-embed-text --reranking-provider gemini --reranking-model gemini-2.0-flash --google-api-key YOUR_GOOGLE_API_KEY --content-columns "question,answer" --metadata-columns "score"
```

Kleos handles the construction of the `CREATE KNOWLEDGE_BASE` SQL, including the JSON parameters for model configurations.

![Kleos KB Create](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/10o2ccb24h46lznqxo3f.jpeg)

**b. Ingesting Data (`kleos kb ingest`)**

Once a KB is created, you need to populate it. Kleos simplifies data ingestion, especially from structured sources like the HackerNews tables.

```bash
# Ingest the latest 100 stories from HackerNews into 'my_hn_kb'
# This uses smart defaults for content and metadata columns.
kleos kb ingest my_hn_kb --from-hackernews stories --limit 100 --hn-datasource my_hackernews_data
```

For more control, you can specify which columns map to your KB's content and metadata:
```bash
kleos kb ingest my_custom_kb --from-hackernews comments
  --hn-datasource my_hackernews_data
  --content-column "text"
  --metadata-map '{"comment_id":"id", "author":"by", "parent_story":"parent"}' 
  --limit 200
```

This command translates to an `INSERT INTO ... SELECT ...` statement, efficiently loading data into your KB.


![Kleos KB Insert](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6gskqkk2ihgv6ic9z62v.jpeg)

**c. Semantic Search (`kleos kb query`)**

The true power of KBs lies in semantic search. Kleos allows you to query your KBs using natural language, with options for metadata filtering:

```bash
# Simple semantic search
kleos kb query my_docs_kb "recent breakthroughs in quantum computing"

# Search with metadata filtering and limit results
kleos kb query product_reviews_kb "positive feedback on model X" \
  --metadata-filter '{"rating":{"$gte": 4}, "verified_purchase":true}' \
  --limit 5
```

The `--metadata-filter` accepts a JSON string, enabling powerful, targeted queries by combining vector search with traditional attribute filtering.


![Kleos KB query](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/2186sop0y76872b211wr.jpeg)

### 3. AI Agents - Your Intelligent Assistants (`kleos kb create-agent`, `kleos kb query-agent`)

MindsDB allows you to create AI Agents that combine the power of Large Language Models (LLMs) with the contextual knowledge stored in your KBs and databases. Kleos makes agent creation and interaction straightforward.

**a. Creating Agents (`kleos kb create-agent`)**


![Kleos LB create-agent](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nunecyiywm7nl83p0gwq.jpeg)

Define an agent, link it to one or more KBs, and specify the LLM it should use:

```bash
# Create an agent using Google's Gemini model, connected to 'product_faq_kb'
kleos kb create-agent product_support_agent 
  --model-name gemini-2.0-flash 
  --google-api-key "GOOGLE_API_KEY"
  --include-knowledge-bases "product_faq_kb" 
  --prompt-template "You are a helpful support agent. Answer the user's question based on the provided documents: {{question}}. Context: {{context}}"
```
You can also include regular database tables for additional context and pass other parameters like temperature or API keys.

**b. Querying Agents (`kleos kb query-agent`)**


![Kleos KB query-agent](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xsxnn87cl415kdt90fr6.jpeg)

Once created, interact with your agent using natural language:
```bash
kleos kb query-agent product_support_agent "What is the warranty period for model X?"
```

The agent will leverage its LLM and the content from `product_faq_kb` to provide an answer.

### 4. AI Models / Generative AI Tables (`kleos ai ...`)


![Kleos AI](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jv1ux9g8kfjeawhxf193.jpeg)

Beyond KBs and Agents, Kleos helps you manage MindsDB's powerful AI Models (often referred to as Generative AI Tables). These models are trained on your data using SQL and can perform a variety of tasks.

**a. Creating AI Models from Data (`kleos ai create-model`)**


![Kleos AI create-model](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/zhvca6t2pxwnw8x2vncb.jpeg)

Train a model directly from a SQL query. For example, to create a model that summarizes HackerNews story titles:

```bash
kleos ai create-model title_summarizer
  --select-data-query "SELECT title AS original_title FROM my_hackernews_data.stories WHERE score > 50 LIMIT 100"
  --predict-column title_summary
  --engine google
  --prompt-template "Generate a very short, catchy summary for this news title: {{original_title}}" 
  --param api_key YOUR_GOOGLE_API_KEY
  --param model_name gemini-2.0-flash
```

This creates a queryable `title_summarizer` model. You can then select from it, providing new titles to get summaries. Kleos supports listing, describing, refreshing, and dropping these models too.

### 5. Automation with MindsDB Jobs (`kleos job ...`)


![Kleos Jobs](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/m0y7eq33nfcxqq4lg471.jpeg)

Repetitive tasks like data ingestion or model retraining can be automated using MindsDB Jobs. Kleos provides commands to manage these jobs.

**a. Creating Jobs (`kleos job create`, `kleos job update-hn-refresh`)**

![Kleos job create](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gx9615uoxh4he1u9wfep.jpeg)

For instance, to create a job that updates your HackerNews data daily:
```bash
kleos job update-hn-refresh daily_hn_data_update --schedule "EVERY 1 day at 02:00"
```
Or, create a custom job with any SQL statements:
```bash
kleos job create nightly_kb_update
  "INSERT INTO my_kb SELECT new_text, new_metadata FROM new_data_source LATEST;"
  --schedule "EVERY 1 day at 03:00"
```

Kleos also allows you to list, check the status/history of, and drop jobs, giving you full control over your automated workflows. This combination aims to make the Kleos not just powerful but also pleasant to use.

## Why This Matters: The Power of In-Database AI & Kleos's Role

The ability to perform complex AI/ML tasks directly within your database using SQL, as enabled by MindsDB, is a game-changer. It democratizes AI by lowering the barrier to entry and streamlines workflows by keeping data and intelligence in one place.

Kleos CLI aims to be a key enabler in this ecosystem by providing:
*   **Accessibility:** A user-friendly command-line tool that makes MindsDB's advanced features easy to discover and use.
*   **Productivity:** Simplifying common tasks like KB management, agent creation, and job automation.
*   **Experimentation:** Facilitating local development and rapid prototyping with tools like the provided Docker Compose setup.

Whether you're building RAG (Retrieval Augmented Generation) applications, AI saas application, or AI agents workflows, creating custom chatbots, automating data insights, or simply exploring the potential of in-database AI, Kleos and MindsDB offer a powerful combination. 

## Nearly at End

Kleos CLI is an open-source project, and your contributions and feedback are highly welcome!

*   **GitHub Repository:** {% embed https://github.com/yashksaini-coder/Kleos %}

*   **Try it out:** You can clone the repo and install it locally on your machine using `pip install .` You can install the cli by running the command `pip install Kleos`. While writing this article, this feature is in work and will be available very soon.

*   **Explore Knowledge Base** Dive deeper into what [Knowledge Base](https://docs.mindsdb.com/mindsdb_sql/knowledge-bases) can offer.


At present, the kleos depends on mindsdb docker-extension & gemini for llm proider, but journey of Kleos is just beginning. Future enhancements could include even richer interactive experiences, more detailed reporting outputs, and support for a wider array of MindsDB's evolving features. 

Thanks for sticking to the end of article. This project took a lot fo heart, research, and all-nighter and late nights snacks too. 

Donate if you wish to support 💗: [yashksaini-coder - GitHub](https://github.com/sponsors/yashksaini-coder) and ⭐ the [Kleos](https://github.com/yashksaini-coder/Kleos) project. See you all next time.

Upvote [Kleos](https://peerlist.io/yashksaini/project/kleos) and support if you haven't already.

![Kisuke GIF](https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExdXU1eDV5YjBtcng0ODJtM2xoeWF4MWFsYzhjM2VwY3Y4djF4emp0ZiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/aDS8SjVtS3Mwo/giphy.gif)

    
  