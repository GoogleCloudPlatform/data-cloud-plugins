# Data Cloud Plugins

This repository serves as the central hub for embedding the Agentic Data Cloud across your favorite developer-focused AI tools. 

Whether you are a developer vibe-coding in Claude Code, an enterprise engineer using the Gemini CLI, or an agent builder constructing complex systems with LangGraph, this kit provides the prescriptive tools like **Skills and MCP servers** you need to interact safely and efficiently with [Google Data Cloud products](https://cloud.google.com/data-cloud).

## 📓 What's Included

Data Cloud Plugins is currently organized as an index pointing to product-specific extensions, MCP configurations, and builder tools.

- [Extensions & Plugins](#individual-extensions--plugins)
- [MCP Servers](#model-context-protocol-mcp)
- [Agent Evaluations & Monitoring](#agent-evaluations--monitoring)

## 🏬 Extensions & Plugins Marketplace

Extensions and plugins are the primary way to inject specialized capabilities into your AI agents. Think of a plugin marketplace as a digital registry or catalog that makes it easy to discover, share, and install these tools directly into your environment. By installing these packages, you equip tools like Gemini CLI, Claude Code, and Codex with the exact **Skills, Prompts, and MCP Servers** they need to understand and interact with your Google Data Cloud infrastructure.

<!-- {x-release-please-start-version} -->

<details>
<summary><h3>Gemini CLI Installation</h3></summary>

Gemini CLI extensions are installed directly from their remote GitHub repositories.
```bash
gemini extensions install https://github.com/gemini-cli-extensions/<REPO>
```

</details>

<details>
<summary><h3>Claude Code Installation</h3></summary>

Claude Code utilizes a marketplace system for plugins. Install the Data Cloud Plugins marketplace to access all Data Cloud plugins:

```bash
# Step 1. Install marketplace
## Option 1. Install marketplace from CLI
claude plugin marketplace add GoogleCloudPlatform/data-cloud-plugins

## Option 2. Install marketplace from Claude
/plugin marketplace add https://github.com/GoogleCloudPlatform/data-cloud-plugins.git

# Step 2. Install a plugin
claude
/plugin install <plugin-name>@data-cloud-plugins

# Step 3. Reload plugins
/reload-plugins

# Optional. Update the marketplace
claude plugin marketplace update data-cloud-plugins
```

</details>

<details>
<summary><h3>OpenAI Codex Installation</h3></summary>

Codex utilizes a marketplace system for plugins. Install the Data Cloud Plugins marketplace to access all Data Cloud plugins:

```bash
# Step 1. Install marketplace
codex plugin marketplace add GoogleCloudPlatform/data-cloud-plugins

# Step 2. Install a plugin
codex plugin add <plugin-name>@data-cloud-plugins

# Optional. Update the marketplace
codex plugin marketplace upgrade data-cloud-plugins
```

</details>

<details>
<summary><h3>Antigravity CLI Installation</h3></summary>

Antigravity CLI installs plugins directly from remote GitHub repositories. You have two options:

**Option 1. Install the full Data Cloud Plugins collection**

Installs all Data Cloud plugins from this repository in one step:

```bash
agy plugin install https://github.com/GoogleCloudPlatform/data-cloud-plugins
```

**Option 2. Install individual plugins from their product repositories**

Point `agy` at a specific plugin's repository to install just that one:

```bash
agy plugin install <REPO>
```

For example:

```bash
agy plugin install https://github.com/gemini-cli-extensions/alloydb
agy plugin install https://github.com/gemini-cli-extensions/spanner
```

See the [Individual Extensions & Plugins](#-individual-extensions--plugins) table below for the full list of repositories.

</details>

<!-- {x-release-please-end} -->

### 📦 Individual Extensions & Plugins

These extensions package product-specific Skills and MCP servers for use in any of your AI tools. Refer to the specific product repositories linked above for installation and configuration requirements.

| Product | Location | Description |
| :--- | :--- | :--- |
| **Data Agent Kit Starter Pack** | https://github.com/gemini-cli-extensions/data-agent-kit-starter-pack | This plugin provides a specialized suite of skills for data users using BigQuery, Dataflow and Managed Apache Spark  along with Knowledge catalog. It acts as an expert assistant, allowing you to use natural language prompts in your preferred coding agent to architect complex data pipelines, transform data with dbt, write Spark and BigQuery SQL notebooks, create and troubleshoot Dataflow pipelines, and orchestrate end-to-end workflows across the GCP data ecosystem. |
| **AlloyDB for PostgreSQL** | https://github.com/gemini-cli-extensions/alloydb | Create, connect, and interact with an AlloyDB for PostgreSQL database and data. |
| **AlloyDB Omni** | https://github.com/gemini-cli-extensions/alloydb-omni | Create, connect, and interact with an AlloyDB Omni database and data. |
| **Bigtable** | https://github.com/GoogleCloudPlatform/cloud-bigtable-ecosystem | Connect, query, and interact with Cloud Bigtable. |
| **Cloud SQL for MySQL** | https://github.com/gemini-cli-extensions/cloud-sql-mysql | Connect and interact with a Cloud SQL for MySQL database and data. |
| **Cloud SQL for PostgreSQL** | https://github.com/gemini-cli-extensions/cloud-sql-postgresql | Create, connect, and interact with a Cloud SQL for PostgreSQL database and data. |
| **Cloud SQL for SQL Server** | https://github.com/gemini-cli-extensions/cloud-sql-sqlserver | Connect to Cloud SQL for SQL Server. |
| **DB Context Engineering Agent** | https://github.com/GoogleCloudPlatform/db-context-enrichment | Author and maintain QueryData / Conversational Analytics API context sets (templates, facets, value searches) that teach the NL→SQL planner your schema vocabulary and golden query shapes. |
| **Firestore** | https://github.com/gemini-cli-extensions/firestore-native | Connect and interact with Cloud Firestore. |
| **Google Cloud Storage** | https://github.com/gemini-cli-extensions/google-cloud-storage | Vetted Google Cloud Storage skills for your coding agent. |
| **Looker** | https://github.com/gemini-cli-extensions/looker | Connect to Looker. |
| **Oracle Database** | https://github.com/gemini-cli-extensions/oracledb | Connect, query, and interact with Oracle Databases and their data within Gemini CLI. |
| **Spanner** | https://github.com/gemini-cli-extensions/spanner | Connect and interact with Spanner data using natural language. |


## 🧩 Model Context Protocol (MCP) Servers

If you are building your own agents or using an interface that supports raw MCP connections, check our comprehensive guide on utilizing **Google Cloud MCP Servers** vs. the open-source **MCP Toolbox**.
* 📖 **[View MCP Configurations](./mcp-servers/README.md)**

## 📊 Agent Evaluations & Monitoring

For developers building production agents (e.g., using ADK or LangGraph), we provide opinionated guidance on making your agents observable, safe, and measurable.
* **[Agent Analytics](./agent-analytics/README.md):** Track usage and performance of agents using BigQuery.
* **[Agent Evaluation](./agent-evaluation/README.md):** Benchmark and test your agents using EvalBench.
* **[UCP Analytics](./ucp-analytics/README.md):** Two-file sample implementation that parses [Universal Commerce Protocol](https://ucp.dev) traffic from an `httpx` event hook and streams events into a partitioned, clustered BigQuery table. Covers all 32 UCP spec event types (27 from the parser, 6 from the included `SampleAgent`, one overlap). Ships a `quickstart.py` you can run against your own GCP project plus a `smoke_test.py` regression check. Copy `ucp_analytics.py` (parser + writer + tracker) and `sample_agent.py` (agent-emitted event types) into your project and grow the classifier / schema as needed.

---

## Security Reminder: Agent Environment Hardening

Your agent can execute tools and commands on your behalf. Protect your Google
Cloud resources by enforcing **The Principle of Least Privilege** across all
CLIs, MCP servers and other resources available to your agents.

*   **Service Accounts:** Use
    [service accounts](https://docs.cloud.google.com/docs/authentication/use-service-account-impersonation)
    instead of end user credentials to access Google Cloud resources.
*   **Limited Permissions:** Assign roles with
    [limited permissions](https://docs.cloud.google.com/iam/docs/roles-overview)
    to the service account that you're using for authentication.
*   **Principal Access Boundaries:** Prevent unwanted cross-org agent access by
    using
    [Principal Access Boundary policies](https://docs.cloud.google.com/iam/docs/principal-access-boundary-policies#use-case-one-project)
    to scope your agent to projects you intend it to access.
*   [Include a condition in the policy binding](https://docs.cloud.google.com/iam/docs/principal-access-boundary-policies#use-case-one-project)
    to ensure that the policy only applies to the service accounts that you
    intend to restrict.

You can read more
[here](https://docs.cloud.google.com/data-cloud-extension/vs-code/prompt-injection-risk)
on how to mitigate prompt injection attacks with Google Cloud MCP.

---

## 🏗️ Contributing

Contributions are welcome. Please, see the [CONTRIBUTING](CONTRIBUTING.md) guide to get started. 

For technical details on setting up an environment for developing on Toolbox itself, see the [DEVELOPER](DEVELOPER.md) guide.

Please note that this project is released with a Contributor Code of Conduct. By participating in this project you agree to abide by its terms. See [Contributor Code of Conduct](CODE_OF_CONDUCT.md) for more information.
