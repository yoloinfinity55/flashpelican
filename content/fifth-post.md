Title: How to Deploy a Pelican Site to GitHub Pages
Date: 2025-10-15 12:00
Category: Tech
Tags: pelican, github, deployment, automation, ci-cd

Deploying a Pelican static site to GitHub Pages is a common and effective way to host it for free. This guide details how to automate the process, so your site updates automatically whenever you push new content.

We will deploy a **Project Page** to the URL `https://yoloinfinity55.github.io/flashpelican`.

### Step 1: Prepare Your Pelican Site for Production

Your site needs to know its final URL.

1.  **Open `publishconf.py`**: This file is specifically for production settings.
2.  **Set the `SITEURL`**: Find the `SITEURL` variable and set it to your full GitHub Pages URL.

    ```python
    # In publishconf.py
    SITEURL = 'https://yoloinfinity55.github.io/flashpelican'
    ```

3.  **Create a `requirements.txt` file**: This tells the automated process what Python packages to install.

    ```bash
    # Run this in your terminal with your virtual environment active
    pip freeze > requirements.txt
    ```

### Step 2: Set Up the GitHub Repository

Push your Pelican *source code* (not the `output` folder) to a new GitHub repository.

1.  **Create a new repo on GitHub** named `flashpelican` under the `yoloinfinity55` account.
2.  **Add a `.gitignore` file** to your project to exclude unnecessary files. It should contain at least:

    ```
    output/
    .venv/
    __pycache__/
    *.pyc
    ```

3.  **Push your project** to the new repository's `main` branch.

    ```bash
    # From your project folder
    git init
    git add .
    git commit -m "Initial commit of Pelican site"
    git branch -M main
    git remote add origin https://github.com/yoloinfinity55/flashpelican.git
    git push -u origin main
    ```

### Step 3: Create the GitHub Actions Workflow

This Action will automatically build and deploy your site.

1.  **Create the workflow directory**: In your project, create a new folder path: `.github/workflows/`.
2.  **Create a new YAML file**: Inside that directory, create a file named `deploy.yml`.
3.  **Add the workflow code**: Paste the following content into `deploy.yml`. **Note the important `permissions` block**, which gives the action permission to push the built site to your `gh-pages` branch.

    ```yaml
    name: Deploy Pelican Site to GitHub Pages

    on:
      # Run on pushes to the main branch
      push:
        branches:
          - main

    jobs:
      build-and-deploy:
        runs-on: ubuntu-latest
        
        # This permissions block is essential for the action to push to your repo
        permissions:
          contents: write
          
        steps:
          - name: Checkout repository
            uses: actions/checkout@v4

          - name: Set up Python
            uses: actions/setup-python@v4
            with:
              python-version: '3.10'

          - name: Install dependencies
            run: |
              python -m pip install --upgrade pip
              pip install -r requirements.txt

          - name: Build the site
            # Use publishconf.py for production settings
            run: pelican content -s publishconf.py

          - name: Deploy to GitHub Pages
            uses: peaceiris/actions-gh-pages@v3
            with:
              github_token: ${{ secrets.GITHUB_TOKEN }}
              publish_dir: ./output
    ```

### Step 4: Finalize and Deploy

1.  **Commit and push** your new files (`publishconf.py`, `requirements.txt`, and the updated `.github/workflows/deploy.yml`) to GitHub.
2.  **Go to your `flashpelican` repository settings** on GitHub, then click on the **"Pages"** tab in the left sidebar.
3.  Under "Build and deployment", set the **Source** to **"Deploy from a branch"**.
4.  Set the **Branch** to `gh-pages` and the folder to `/ (root)`. Click **Save**.

The GitHub Action will now run automatically. After a minute or two, your site will be live at: **https://yoloinfinity55.github.io/flashpelican**```