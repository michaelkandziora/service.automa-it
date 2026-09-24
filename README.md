# automa-it

`automa-it` is a collection of Bash utilities for setting up and managing Linux development environments. It includes scripts for shells, Docker, Python, Node.js, backups, and related system tasks, along with a small Flask service that can package selected script groups for remote installation.

## Repository layout

- `Scripts/` contains the interactive menu, shared helpers, configuration, and setup scripts.
- `Flask/` contains the optional HTTP service.
- `Tests/` contains shell test helpers.
- `docker-compose.yaml` and `Dockerfile` define the Flask service container.

## Run the menu locally

```bash
git clone https://github.com/michaelkandziora/service.automa-it.git
cd service.automa-it/Scripts
chmod +x menu.sh
./menu.sh .
```

## Run the Flask service

With Docker Compose:

```bash
git clone https://github.com/michaelkandziora/service.automa-it.git
cd service.automa-it
docker compose up --build -d
```

The Flask service listens on port `5000` by default. It provides an `/install.sh` endpoint that returns a generated installer for a selected script group. The default group is used when no tag is supplied; supported tags are `default`, `pro`, `zsh`, `docker`, `python`, `nodejs`, `backup`, and `forensic`.

For local development, create and activate a virtual environment, install the dependencies, and start the Flask app:

```bash
cd service.automa-it/Flask
python -m venv .venv
source .venv/bin/activate
pip install -r ../requirements.txt
python app.py
```

The app is configured to listen on port `5000`. Review any generated shell script before running it, especially when the service is reachable beyond your local machine.

## Configuration

`Scripts/config.toml` contains preferences used by the setup scripts. The current TOML reader is used by `customize_omz.sh` for Oh My Zsh theme, alias, and plugin settings.

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE).
