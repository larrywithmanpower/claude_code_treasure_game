Deploy this project to GitHub Pages. Follow each step carefully.

## Step 1 — Check GitHub Login

Run this command to check if the user is logged into GitHub:
```
gh auth status
```

If NOT logged in, guide the user to login:
- Tell them to run: `gh auth login`
- Walk them through: choose "GitHub.com" > "HTTPS" > "Login with a web browser"
- Wait for them to confirm login is complete before continuing
- Re-run `gh auth status` to confirm login succeeded

## Step 2 — Check or Create GitHub Repository

Run this to check if a remote origin already exists:
```
git remote -v
```

If NO remote origin exists:
1. Get the GitHub username:
   ```
   gh api user --jq '.login'
   ```
2. Create a new public GitHub repository named `claude_code_treasure_game`:
   ```
   gh repo create claude_code_treasure_game --public --source=. --remote=origin --push
   ```
3. Tell the user their repo URL: `https://github.com/USERNAME/claude_code_treasure_game`

If remote origin ALREADY exists, skip to Step 3.

## Step 3 — Prepare Project for GitHub Pages

1. Make sure there is an `index.html` in the project root. If it does not exist, create a simple one that displays the project name and lists any images in the `./images/` folder as a gallery.

2. Commit all changes:
   ```
   git add .
   git commit -m "Deploy to GitHub Pages"
   ```
   If nothing to commit, that is fine — continue.

## Step 4 — Deploy to GitHub Pages

Push to the `gh-pages` branch using the GitHub CLI:

```
git checkout --orphan gh-pages
git reset --hard
git checkout main -- .
git add .
git commit -m "GitHub Pages deployment"
git push origin gh-pages --force
git checkout main
```

Then enable GitHub Pages via CLI:
```
gh api repos/{owner}/{repo}/pages \
  --method POST \
  -f source[branch]=gh-pages \
  -f source[path]=/ 2>/dev/null || \
gh api repos/{owner}/{repo}/pages \
  --method PUT \
  -f source[branch]=gh-pages \
  -f source[path]=/
```

Replace `{owner}` and `{repo}` with the actual values from `gh api user --jq '.login'` and the repo name.

## Step 5 — Confirm Deployment

1. Get the GitHub Pages URL:
   ```
   gh api repos/{owner}/{repo}/pages --jq '.html_url'
   ```

2. Tell the user:
   - Live site: `https://USERNAME.github.io/claude_code_treasure_game/`
   - GitHub repo: `https://github.com/USERNAME/claude_code_treasure_game`
   - It may take 1-2 minutes for the site to go live

3. Done!
