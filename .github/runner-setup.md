Self-hosted runner setup

Summary
- Register a self-hosted runner for this repository and ensure Node.js and required tools are installed.

Labels
- Recommended labels for the runner: `self-hosted`, `linux`, `x64` (adjust to your OS/arch as needed).

Quick registration (Ubuntu example)
1. In GitHub go to: Settings → Actions → Runners → Add runner, copy the registration commands shown on the page.
2. On the runner machine (example commands):

```bash
# create a directory for the runner
mkdir actions-runner && cd actions-runner

# download latest runner (example)
curl -o actions-runner.tar.gz -L https://github.com/actions/runner/releases/latest/download/actions-runner-linux-x64-2.305.0.tar.gz
tar xzf actions-runner.tar.gz

# configure the runner (replace URL and TOKEN with values from GitHub UI)
./config.sh --url https://github.com/<OWNER>/<REPO> --token <RUNNER_TOKEN> --labels "self-hosted,linux,x64"

# run as a service (recommended)
sudo ./svc.sh install
sudo ./svc.sh start
```

Environment prerequisites
- Install Node.js (v18+ recommended) and npm. Example using NodeSource on Ubuntu:

```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs
```

- Optionally install `pm2` if you'd like to manage the Node process:

```bash
sudo npm install -g pm2
```

Notes
- Keep the runner online and ensure the user running the runner has permission to start your Node app.
- Make sure the runner's labels match the `runs-on` in the workflow (`self-hosted`, `linux`, `x64`) or adjust the workflow to match your runner labels.
- For Windows or macOS runners, follow the platform-specific download/config commands shown in the GitHub runner add UI.

Security
- Never commit your runner token. Use the one-time token from the GitHub UI during `./config.sh`.
