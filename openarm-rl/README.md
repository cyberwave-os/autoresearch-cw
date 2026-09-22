# OpenArm pick and place RL

Objective of this task: Train a RL model that moves a OpenArm with 2 wrist cameras and a RealSense on top and accomplishes 70% success rate on pick and place of a paper cup, from one area of a table to the other. 

To accomplish this, you have:

* Access to the Cyberwave MCP with a valid token (dev environment). With this, you can add RL tasks and run simulations and much more
* Access to a Cyberwave environment that fits our use case https://app-dev.cyberwave.com/vittorio-banfis-workspace-3/envs/autolearner-openarm
* Access to the Cyberwave remote labs. You will find a remote lab that mirrors the setup described above
* Full access to this MacBook Pro (I installed XCode and Homebrew)

Proceed as follows:

1. Read the Cyberwave documentation to learn how to write RL models in a way that follows the Cyberwave guidelines
2. Using the Cyberwave MCP, download the Mujoco zip file of the environment above
3. Write and train a RL task to accomplish the goal
4. Upload it to Cyberwave, run a simulation and observe the video result. Decide if you accomplished the goal or if you need to go back to (3)
5. Once you are satisfied, access the remote lab feature of Cyberwave, release the RL model there, run the RL model as controller of the real open arm device
6. Check the video of the real device and decide if you accomplished the goal or you need to go back to (3)

Do not stop or ask for user feedback until you are done.

## Authentication

You can find both the API key for the API and the credentials to log in with Chrome in the .env file.
You can log in with Chrome to https://app-dev.cyberwave.com

## Cyberwave setup

This project uses the **Cyberwave dev environment**. Both the MCP server and the
Python SDK must point to dev:

| Service | Dev endpoint |
| --- | --- |
| Cyberwave MCP | `https://mcp-dev.cyberwave.com/mcp` |
| Cyberwave API | `https://api-dev.cyberwave.com` |

Do not use the production endpoints (`https://mcp.cyberwave.com/mcp` or
`https://api.cyberwave.com`) for this project.

### 1. Create a Cyberwave API key

Create or copy an API key from the profile page in the
[Cyberwave dev app](https://app-dev.cyberwave.com/profile). Keep the key secret:
never commit it to this repository or paste a real key into documentation,
issues, or logs.

### 2. Install the Cyberwave MCP for Codex

The Codex desktop app and Codex CLI share the same MCP configuration at
`~/.codex/config.toml`. Install [Node.js](https://nodejs.org/) first if `npx` is
not already available, then add this configuration:

```toml
[mcp_servers.cyberwave]
command = "npx"
args = ["-y", "mcp-remote@latest", "https://mcp-dev.cyberwave.com/mcp", "--header", "Authorization: Bearer <CYBERWAVE_API_KEY>"]
```

Replace `<CYBERWAVE_API_KEY>` with the API key from the dev app. This value is
stored in your user-level Codex configuration, so ensure the file is readable
only by your user:

```bash
chmod 600 ~/.codex/config.toml
```

Restart the Codex desktop app after saving the file. Confirm that Codex loaded
the server:

```bash
codex mcp get cyberwave
codex mcp list
```

In the Codex app, `/mcp` should show `cyberwave`, and a read-only request such as
"list my Cyberwave workspaces" should succeed. If a production Cyberwave MCP is
already configured under the same name, replace its URL with the dev URL above
and restart Codex.

### 3. Install the Cyberwave Python SDK

From this directory, create and activate an isolated virtual environment, then
install the SDK from PyPI:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install cyberwave
```

Configure the same dev API key and explicitly select the dev API before running
SDK code:

```bash
export CYBERWAVE_API_KEY="<CYBERWAVE_API_KEY>"
export CYBERWAVE_BASE_URL="https://api-dev.cyberwave.com"
```

Verify the installation and configuration without printing the API key:

```bash
python - <<'PY'
import os
from importlib.metadata import version

import cyberwave

assert os.environ.get("CYBERWAVE_API_KEY"), "CYBERWAVE_API_KEY is not set"
assert os.environ.get("CYBERWAVE_BASE_URL") == "https://api-dev.cyberwave.com"
print(f"Cyberwave SDK {version('cyberwave')} is installed")
print(f"API endpoint: {os.environ['CYBERWAVE_BASE_URL']}")
PY
```

Run `source .venv/bin/activate` and export the two variables again in every new
shell, unless they are supplied by a local secret manager or shell environment.

