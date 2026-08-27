# Cursor for Python Engineers: A Hands-On Workshop

**Duration:** 1h 40 minutes  
**Audience:** Python Engineers  
**IDE Version:** Cursor Agentic Windows Desktop IDE ver. `3.17.21`  
**Practice project:** A Python Model Context Protocol (MCP) server built with [FastMCP Python library](https://gofastmcp.com/)

## Table of contents

- [Workshop Overview](#workshop-overview)  
- [Participant prerequisites](#participant-prerequisites) 
- [**Part 1:** Introduction to Cursor](#part-1-introduction-to-cursor)  
    - [What is Cursor?](#what-is-cursor)  
    - [Ownership](#ownership)  
    - [How to Download and Install Cursor](#how-to-download-and-install-cursor)  
    - [How to Update Cursor IDE](#how-to-update-cursor-ide)  
    - [Promotions, Trials, and Discounts](#promotions-trials-and-discounts)  
    - [Community and Resources](#community-and-resources)  
- [**Part 2:** Practical Exercise - Building an MCP Server](#part-2-practical-exercise---building-an-mcp-server)
    - [Understanding MCP](#understanding-mcp)  
    - [Building with FastMCP](#building-with-fastmcp)  
    - [Testing the Server](#testing-the-server)  
- [**Part 3:** Cursor Workflows & Best Practices](#part-3-cursor-workflows--best-practices)  
    - [Checklist: Avoiding Common AI Pitfalls](#checklist-avoiding-common-ai-pitfalls)

## Workshop Overview

Cursor (by Anysphere/SpaceX) can feel like magic - until it doesn't. In this beginner-friendly, hands-on workshop, you'll learn a practical workflow for building and changing real Python code with Cursor without getting lost.

This workshop teaches a repeatable, safe workflow for using Cursor to plan, implement, inspect, refactor, and debug real Python changes. We will cover:

* Planning small tasks and generating multi-file changes with Cursor Composer feature.
* Iterating safely using Chat + Apply diffs.
* Navigating quickly with code search.
* Speeding up everyday edits with inline completion and the inline editor.

## Participant prerequisites

Participants should bring:

- A laptop with Windows 11, macOS, or a supported Linux distribution (e.g., [Ubuntu](https://ubuntu.com/)).
- [Cursor](https://cursor.com/download) installed and signed in.
- [Python](https://www.python.org/downloads/) 3.11 or later available in a terminal.
- Git installed (e.g., [Git Bash for Windows](https://git-scm.com/install/windows)).
- [Node.js](https://nodejs.org/en) 18+.
- A working internet connection for package installation and finance market-data requests.

No prior experience with Cursor, MCP, FastMCP, or AI-assisted coding is required. Basic Python functions, imports, and terminal commands are helpful.

## Part 1: Introduction to Cursor

### What is Cursor?

Cursor is an AI-first [IDE (Integrated Development Environment)](https://en.wikipedia.org/wiki/Integrated_development_environment) built as a fork of [VS Code](https://code.visualstudio.com/). It integrates advanced [Large Language Models (LLMs)](https://en.wikipedia.org/wiki/Large_language_model) directly into the code editor, allowing developers to generate, edit, and debug code through natural language prompts and highly context-aware auto-completion.

For this workshop, think of Cursor as a **fast collaborator inside your editor**, not an autopilot. It is useful when you provide clear goals, relevant context, boundaries, and a way to verify the result.


**Pros:**

* ✅ **Familiar Interface**, because it is a [VS Code](https://code.visualstudio.com/) fork, all your favorite extensions, themes, and keybindings work out of the box.
* ✅ Keeps coding, review, terminal work, and AI assistance in **one workspace**.
* ✅ **Deep Context**. Cursor understands your entire codebase, reading across multiple files to provide accurate suggestions.
* ✅ **Agentic Capabilities**. Features like Composer can plan and execute complex, multi-file code changes.
* ✅ **Speeds up routine** edits, boilerplate, navigation, and first drafts.
* ✅ **Useful** for explaining unfamiliar code and generating test cases.
* ✅ **Helps beginners** turn intent into a concrete next step.

**Cons:**

* ❌ **Cloud Reliance:** Features require an active internet connection to communicate with the cloud-hosted LLMs.
* ❌ **Cost:** While there is a free tier, heavy professional use requires a monthly or yearly [subscription](https://cursor.com/pricing).
* ❌ **Occasional Hallucinations:** Like all AI tools, it can sometimes confidently invent APIs, imports, behavior, or facts.
* ❌ **You are responsible** for security, correctness, licensing, and data handling
* ❌ **Generated tests can repeat** the same **misunderstanding** as the implementation
* ❌ **Overreliance** can slow skill development and hide fundamentals

### Ownership

Cursor was created by **Anysphere**, an AI research startup backed by prominent investors including OpenAI Startup Fund and Andreessen Horowitz (a16z). **SpaceX** officially completed its $60 billion all-stock acquisition of Cursor (parent company Anysphere) on August 14, 2026 [[source](https://cursor.com/blog/joining-spacex)].

### How to Download and Install Cursor

Cursor is cross-platform. To install:

1. Navigate to the official website at [cursor.com/download](https://cursor.com/download).
2. Download the appropriate installer for your operating system (e.g., Windows `.exe`, macOS `.dmg`, or Linux).

For Windows operating system, you can check your system type (`x64` vs `ARM64`) in the `Settings > System > About`:

![0001.png](img/0001.png "Settings > System > About > System type")

3. Find the downloaded file (e.g., `CursorSetup-x64-3.17.21.exe`).
4. Follow the install steps for your OS:
    - **Windows**: Run the installer and follow the on-screen prompts,
    - **macOS**: Drag Cursor into your `Applications` folder,
    - **Linux**: Install via your package manager (`apt` or `dnf`) if available, or extract the `AppImage/archive` and run it.
4. Open `Cursor` from your applications menu or desktop
5. Sign in with your [Cursor account](https://cursor.com/dashboard) when prompted
6. On first launch, you will be prompted to optionally import your [VS Code](https://code.visualstudio.com/) settings and extensions.

### How to Update Cursor IDE

Keeping your IDE updated ensures you have the latest AI models and bug fixes.

* **Windows Desktop Interface:** Navigate to the top menu bar, click on `Help`, and select `Check for Updates…`. Cursor will download and apply any available updates.

### Promotions, Trials, and Discounts

* **Standard Free Tier:** Cursor offers a basic free tier with access to baseline AI autocomplete features.
* **14-Day Pro Trial:** New users typically receive a 14-day free trial of the Pro tier, which includes premium fast requests to advanced models like Claude 3.5 Sonnet and GPT-4o.
* *Note: Always check the [Cursor pricing page](https://cursor.com/pricing) for the most up-to-date student discounts or promotional events.*

### Community and Resources

* **Cursor Ambassador Program:** Passionate about Cursor? Apply to become an ambassador and help grow the community: [https://cursor.com/ambassadors](https://cursor.com/ambassadors)
* **Community Forum:** The official place to report bugs, request features, and discuss workflows with other developers: [https://forum.cursor.com/](https://forum.cursor.com/)

## Part 2: Practical Exercise - Building an MCP Server

For our hands-on practice, we will build a Model Context Protocol (MCP) server using Python. This section utilizes concepts from the presentation "ruslan_korniichuk_-_mcp_20260720.pdf".

### Understanding MCP

* The Model Context Protocol (MCP) acts as a universal adapter, described as a "USB-C port for AI".


* It was created by Anthropic and donated to the Linux Foundation in December 2025.


* MCP connects AI applications (like Claude or ChatGPT) to data sources, tools, and workflows.


* The architecture consists of an MCP Host (the AI application), an MCP Client (which maintains the connection), and an MCP Server (which provides context to the clients).

**The Three Primitives of MCP:**

* **Resources:** Read-only context, such as file contents or database records ("Here is some data").


* **Prompts:** Reusable templates for structuring LLM interactions ("Here is how to ask").


* **Tools:** Executable functions like API calls or database queries ("Take this action").

### Building with FastMCP

FastMCP is the standard framework for building MCP applications. It acts as the "FastAPI of the MCP ecosystem".

* It is declarative and Pythonic.


* It relies on standard Python type hints (like `int`, `str`, and Pydantic models).


* It requires zero boilerplate, featuring automatic JSON schema generation and auto-discovery.

**Step 1: The Minimal Server**
Using Cursor's Composer, ask it to create a file named `stocks_server_min.py` with the following code:

```python3
from fastmcp import FastMCP

mcp = FastMCP("stocks")

@mcp.tool
def ping() -> str:
    """Return a simple health-check message."""
    return "stocks MCP server is alive"

if __name__ == "__main__":
    mcp.run()

```

*Run the server by typing `python stocks_server_min.py` in the Cursor terminal*.

**Step 2: Extending the Server**
Now, use Cursor's Chat + Apply to expand our server into a robust stock analysis tool. Create `stocks_server.py` using the `yfinance` library:

```python3
"""Stock market MCP server built with FastMCP and yfinance."""
import os
import yfinance as yf
from fastmcp import FastMCP

mcp = FastMCP("stocks")
WATCHLIST = ["AAPL", "MSFT", "GOOGL", "NVDA", "TSLA"]

# Tool 1: get_company_info
@mcp.tool
def get_company_info(ticker: str) -> dict:
    """Return basic company information for the given ticker symbol."""
    info = yf.Ticker(ticker).info
    return {
        "ticker": ticker.upper(),
        "name": info.get("longName") or info.get("shortName"),
        "sector": info.get("sector"),
        "industry": info.get("industry"),
        "country": info.get("country"),
        "website": info.get("website"),
        "market_cap": info.get("marketCap"),
        "summary": info.get("longBusinessSummary"),
    }

# Tool 2: get_stock_price
@mcp.tool
def get_stock_price(ticker: str) -> dict:
    """Return the latest available stock price and currency for the ticker."""
    t = yf.Ticker(ticker)
    fast = t.fast_info
    return {
        "ticker": ticker.upper(),
        "price": float(fast["last_price"]),
        "currency": fast.get("currency"),
        "previous_close": float(fast.get("previous_close")),
    }

# Static resource: stocks://watchlist
@mcp.resource("stocks://watchlist")
def watchlist() -> list[str]:
    """Return the default watchlist of ticker symbols."""
    return WATCHLIST

if __name__ == "__main__":
    transport = os.getenv("MCP_TRANSPORT", "stdio").lower()
    if transport == "http":
        mcp.run(transport="http", host="127.0.0.1", port=8000)
    else:
        mcp.run()

```

### Testing the Server

You can inspect the server locally using the MCP Inspector shipped with FastMCP.

* Run the command: `fastmcp dev inspector stocks_server.py`.


* This command starts your server on stdio and launches the MCP Inspector in your web browser.


* Inside the Inspector, you can list your tools, call `get_stock_price` with `ticker="AAPL"`, and view the JSON response.

## Part 3: Cursor Workflows & Best Practices

During the live refactor of our `stocks_server.py`, practice these Cursor commands:

1. **Code Search (Ctrl/Cmd + Enter):** Ask Cursor "Where is the watchlist defined?" to instantly jump to the `WATCHLIST` variable.
2. **Inline Editor (Ctrl/Cmd + K):** Highlight the `get_stock_price` function and prompt: *"Add error handling if the ticker is invalid."*
3. **Composer (Ctrl/Cmd + I):** Prompt: *"Create a new file called `test_stocks.py` and write pytest functions for all the tools in `stocks_server.py`."*

### Checklist: Avoiding Common AI Pitfalls

To prevent Cursor from acting unpredictably, follow this prompt engineering checklist:

* [ ] **Provide Context:** Always tag relevant files using `@` (e.g., `@stocks_server.py`) so the LLM isn't guessing.
* [ ] **Be Specific:** Instead of *"fix the bug,"* use *"the get_stock_price tool throws a KeyError on line 34 when querying a delisted stock. Please handle this by returning None."*
* [ ] **Iterate Small:** Don't ask Composer to build an entire application in one prompt. Build the data models first, verify them, and then move to the API logic.
* [ ] **Review Diffs Carefully:** Treat AI-generated code like a Pull Request from a junior developer. Always read the diff before clicking "Apply."

---