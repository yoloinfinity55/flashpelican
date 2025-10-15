Title: Quick Guide: Pelican on an M1 Mac (Markdown)
Date: 2025-10-15 11:45
Category: Tech
Tags: pelican, m1, mac, python, quickstart


This is a practical, step-by-step guide for installing and setting up the static site generator **Pelican** on a **Mac mini with an M1 (Apple Silicon) chip**.

Pelican is a Python-based tool, so the first steps focus on establishing a clean Python environment.


## 💻 Part 1: Initial M1 Setup (Python & Virtual Environment)

A virtual environment is highly recommended for all Python projects. It isolates the dependencies for Pelican from other Python projects and your system's Python installation.

### Step 1: Install Python (if not already installed)

While macOS comes with a version of Python, it's best practice for development to install the official version.

1.  **Download the Official Installer:** Go to the official Python website's downloads page and look for the latest stable version for **macOS**. The installer will automatically be an **Apple Silicon (arm64)** build, which is natively optimized for your M1 chip.
2.  **Run the Installer:** Double-click the downloaded `.pkg` file and follow the on-screen prompts.
3.  **Verify the Installation:** Open your **Terminal** application (Spotlight search: <kbd>Cmd</kbd> + <kbd>Space</kbd>, type "Terminal").

    ```bash
    python3 --version
    # Expected output: Python 3.x.x (where x.x is the version you installed)
    ```

### Step 2: Create Your Project Directory

Choose a location for your Pelican site and create a new folder.

1.  In your Terminal, navigate to your desired location (e.g., a `projects` folder in your home directory) and create a new project folder named `my-pelican-site`.

    ```bash
    mkdir -p ~/projects/my-pelican-site
    cd ~/projects/my-pelican-site
    ```

### Step 3: Create and Activate a Virtual Environment

Use Python's built-in `venv` module to create an isolated environment in your new project folder.

1.  **Create the Virtual Environment:**

    ```bash
    python3 -m venv .venv
    ```

    *This command creates a new folder named `.venv` inside your project directory.*

2.  **Activate the Virtual Environment:**

    ```bash
    source .venv/bin/activate
    ```

    *Your Terminal prompt should now change to start with `(.venv)`, indicating the environment is active. All packages you install now will only affect this project.*

---

## 📦 Part 2: Pelican Installation and Quickstart

With the Python environment ready, you can now install Pelican and generate your site.

### Step 4: Install Pelican

Use the Python package installer (`pip`) to install Pelican and the Markdown parser (which is recommended for writing content).

1.  **Install Pelican:**

    ```bash
    python -m pip install "pelican[markdown]"
    ```

### Step 5: Run the Quickstart Script

Pelican comes with a quickstart utility to set up the basic structure and configuration.

1.  **Run the Quickstart:**

    ```bash
    pelican-quickstart
    ```

2.  **Answer the Questions:** The script will ask you a series of questions.
    *   For questions with a default value in brackets (e.g., `[my blog]`), you can press <kbd>Enter</kbd> to accept it.
    *   You will be asked for your **URL prefix**. This is important. If you plan to deploy your site to a domain like `https://www.example.com`, enter that here. For now, you can press <kbd>Enter</kbd> to leave it blank, or enter a placeholder.
    *   **Do you want to generate a Makefile? (Y/n)**: **Y** (Recommended for easier running).
    *   **Do you want to generate a Rakefile? (Y/n)**: **n** (Unless you use Ruby Rake).

---

## ✍️ Part 3: Create Content and Preview

### Step 6: Create Your First Article

Pelican content is typically written in Markdown or reStructuredText. The quickstart created a `content` folder.

1.  **Create a New File:** Use your preferred text editor (like VS Code, Sublime Text, or `nano` in the terminal) to create a new file named `first-post.md` inside the `content` folder.

    ```bash
    # You can use the terminal editor `nano`
    nano content/first-post.md
    ```

2.  **Add Content:** Paste the following basic structure, which includes required metadata:

    ```markdown
    Title: Hello World of Pelican
    Date: 2025-10-15 12:00
    Category: General
    Tags: quickstart, mac-mini, m1

    This is my first post created with Pelican on my M1 Mac mini!
    It's super easy to get started once Python and venv are set up.
    ```

3.  **Save the File:** If you used `nano`, press <kbd>Ctrl</kbd>+<kbd>O</kbd>, then <kbd>Enter</kbd>, then <kbd>Ctrl</kbd>+<kbd>X</kbd>.

### Step 7: Generate Your Static Site

This step compiles your content into the final HTML/CSS/JS files.

1.  **Generate the Site:**

    ```bash
    pelican content
    ```

    *The generated files will be placed in the newly created `output/` directory.*

### Step 8: Preview Your Site Locally

Use Pelican's built-in web server to view your site in a browser.

1.  **Serve the Site:**

    ```bash
    pelican --listen
    # OR, if you chose to generate a Makefile:
    make serve
    ```

2.  **View in Browser:** Open your web browser and navigate to:

    ```
    http://localhost:8000/
    ```

    *You should now see your Pelican site with your new "Hello World of Pelican" post!*

### Final Step: Deactivate Environment

When you are done working, you should deactivate the virtual environment.

1.  **Deactivate:**

    ```bash
    deactivate
    ```

    *Your Terminal prompt will return to normal.*

To resume work later, just navigate back to your project folder (`cd ~/projects/my-pelican-site`) and run `source .venv/bin/activate` again.