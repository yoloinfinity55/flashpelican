Title: Quick Guide: Pelican on an M1 Mac
Date: 2025-10-15 11:30
Category: Tech
Tags: pelican, m1, mac, python, quickstart

Setting up the Pelican static site generator on an Apple Silicon (M1) Mac is straightforward. This guide provides the essential commands to get you up and running quickly.

### 1. Prepare Your Environment

First, create a project directory and a Python virtual environment to keep dependencies isolated. This assumes you have Python 3 installed from the official Python website.


Create project folder and move into it
```bash
mkdir -p ~/projects/my-pelican-site
cd ~/projects/my-pelican-site
```
Create and activate a virtual environment
```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 2. Install Pelican

With the virtual environment active, use `pip` to install Pelican and the Markdown parser.

```bash
python -m pip install "pelican[markdown]"
```

### 3. Initialize Your Site

Run the Pelican quickstart script and answer the on-screen prompts. Accepting the defaults is fine for now.

```bash
pelican-quickstart
```

### 4. Create Content and Preview

Add your first post by creating a new `.md` file inside the `content/` folder. Then, generate the HTML and start the local server to preview your work.


Generate the static site into the 'output' folder
```bash
pelican content
```
Start the local preview server
```bash
pelican --listen
```

Now, you can view your new site by navigating to `http://localhost:8000` in your browser.



