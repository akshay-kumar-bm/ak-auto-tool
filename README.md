# ak-auto-tool

A workspace of small AI-automation experiments: a website-to-MCP-retriever generator, an Ace Tech Solutions marketing site, and a saved ADK REST API reference.

## Contents

### proj1/mcp_tool: MCP Website Generator
Crawls a website (configurable depth/page limit/delay), embeds page text with SentenceTransformers (`all-MiniLM-L6-v2` default), stores vectors in a FAISS index with metadata, and registers a callable retriever in `MCP_REGISTRY` that returns url/title/text/score results.
- `scrapers/website_scraper.py`: recursive crawler (requests + BeautifulSoup/lxml)
- `indexers/faiss_indexer.py`: chunking, embedding, FAISS build/save/load
- `mcps/registry.py`: registry of retrievers
- `generate_mcp.py`: CLI + `generate_mcp_from_website(...)` API
- `mcp_indices/langchain_index.faiss`: a sample prebuilt index

```bash
cd proj1
./setup.sh && source venv/bin/activate
python -m mcp_tool.generate_mcp --url "https://www.langchain.com" --name langchain
```
```python
from mcp_tool.mcps.registry import MCP_REGISTRY
MCP_REGISTRY["langchain"]("how to use retrievers in langgraph?")
```
Note: `proj1/README.md` documents a different, older `mcp_tool.py` CLI (LangChain RecursiveUrlLoader, hybrid search) that is not in the repo; the package under `proj1/mcp_tool/` is what exists. `sample_mcp_creation_doc.txt` holds a sample.

### ace-tech-website/my-app
Next.js 15 / React 19 / Tailwind 3 site titled "Ace Tech Solutions - AI Automation Company" with Header, Hero, Services, Footer, ContactForm and pages for about, services, contact, terms and privacy. Largely scaffolded via GitHub Copilot agent PRs (see git history).
```bash
cd ace-tech-website/my-app && npm install && npm run dev
```

### proj2, proj3
Placeholder READMEs only ("reserved for future project requirements").

### adk_rest_api_reference.md
A ~940-line copy of the Google Agent Development Kit REST API reference, kept as notes.

## Limitations
Exploratory workspace: no tests, inconsistent docs, empty placeholder projects, and no end-to-end integration between the pieces.
