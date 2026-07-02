# GitHub Setup — [Project Name]

Per-project repo, token, and **GitHub Pages deployment** (with custom domain + rollback).

## Intake (ask before scaffolding)
Collect these two values, then reuse them below:
- **Homepage URL:** `https://[domainname.com]`  (used in `package.json` `homepage`)
- **Custom domain (CNAME):** `[domainname.com]`  (leave blank to use the default
  `https://[user].github.io/[repo]/` URL instead)

## Repository
- Create a dedicated GitHub repository for this project.
- Link the repository to the local project folder.

## Token
- Store the GitHub classic PAT in the project `.env` file as `GITHUB_TOKEN` or `GH_TOKEN`.
- Example:
  ```env
  GITHUB_TOKEN=ghp_your_classic_token_here
  ```
- Do not commit `.env` to Git.

## Required Access
- `repo` for private repositories
- `public_repo` for public repositories
- `workflow` if GitHub Pages or Actions deployment is used

## Deploy to GitHub Pages (gh-pages)
Primary method — publishes the built `dist/` to a `gh-pages` branch.

1. Install:
   ```bash
   npm install -D gh-pages
   ```
2. `package.json` — set homepage + deploy scripts:
   ```json
   {
     "homepage": "https://[domainname.com]",
     "scripts": {
       "predeploy": "npm run build",
       "deploy": "gh-pages -d dist --cname [domainname.com]"
     }
   }
   ```
   - Drop `--cname [domainname.com]` if there is **no** custom domain.
3. `vite.config.ts` — set `base` (see `core-technology-template.md`):
   - Custom / apex domain → `base: '/'`
   - Project pages (no custom domain) → `base: '/[repo-name]/'`
4. Deploy:
   ```bash
   npm run deploy
   ```
5. GitHub → Settings → Pages:
   - Source: `gh-pages` branch, `/ (root)` (or use Actions — see alternative below)
   - Custom domain: `[domainname.com]`, then enable **Enforce HTTPS**
   - DNS: apex `A`/`ALIAS` records to GitHub Pages IPs, or `CNAME` → `[user].github.io`

### Rollback (why gh-pages helps)
- Each `npm run deploy` is a commit on the `gh-pages` branch.
- To revert a bad deploy: `git revert` (or reset) on `gh-pages` to the last good commit,
  or re-run `npm run deploy` from a previous source commit — restores the last good build.

## Alternative: GitHub Actions
- In GitHub, open Settings > Pages and set the source to **GitHub Actions**.
- In Actions > General, allow workflow permissions to read and write.
- If the workflow updates pull requests or workflow files, enable GitHub Actions to
  create and approve pull requests.
- Requires the `workflow` token scope.

## Checklist
- [ ] Dedicated repo created and linked to the local folder
- [ ] Classic PAT in `.env` (`repo`/`public_repo` + `workflow`); `.env` gitignored
- [ ] Homepage URL + custom domain captured from Intake
- [ ] `gh-pages` installed; `homepage` + `predeploy`/`deploy` scripts set
- [ ] Vite `base` matches domain type (`/` custom, `/[repo]/` project pages)
- [ ] `npm run deploy` publishes to `gh-pages`; site serves with **HTTPS enforced**
- [ ] Rollback path verified (revert on `gh-pages` restores last good build)
