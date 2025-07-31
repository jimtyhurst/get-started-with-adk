# get_started_with_adk

Sample ADK agents from Google's qwiklabs.com lab, "Get started with Agent Development Kit (ADK)" https://explore.qwiklabs.com/classrooms/17848/labs/103329 with minor modifications to make it easier to run locally, rather than in Google Cloud Editor in the QwikLabs environment.

See https://github.com/google/adk-samples for other examples of agents developed with the ADK.

## Development environment

We assume [uv](https://github.com/astral-sh/uv) for setting up the virtual environment with package dependencies, but you can use any other package manager and virtual environment tools.

### Set up virtual environment and install packages

```shell
uv venv --python 3.13
source .venv/bin/activate
uv sync
```

### Set environment variables.

* Copy [./set_env_vars.template] to create `set_env_vars.sh`.
* Edit `set_env_vars.sh` to hold your project parameters.
* Source that file to initialize the environment variables in your shell.

```shell
cp set_env_vars.template set_env_vars.sh
# Edit the variable values in 'set_env_vars.sh'.
source set_env_vars.sh
```

### Authenticate with your Google account

```shell
gcloud auth application-default login
```

### Start the ADK web UI

This app provides a web interface for you to test your agents.


```shell
adk web
```

Copy and paste the URL that is displayed in the terminal output to open the app in a browser. In the upper left, you can select the agent to be tested. In the lower right, you can enter a prompt for the agent.

### Chat with an agent via the command-line interface

Similar to the web UI discussed above, you can send prompts to your agents through a terminal command line interface (CLI).

In this example, we test the `llm_auditor` to validate statements. That agent delegates to two subagents that are run sequentially:

1. critic_agent
2. reviser_agent

```shell
adk run llm_auditor
[user]: Verify this statement: Water consists of 2 parts hydrogen and 2 parts oxygen.
```

The response will be quite lengthy, but somewhere in the response, you will see: `**Verdict:** Inaccurate`, because water is 2 parts hydrogen to only 1 part oxygen.
