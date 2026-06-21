# Blockchain Skills (External)

69 blockchain-focused skills from
[hairyf/blockchain-skills](https://github.com/hairyf/blockchain-skills)
(MIT). **66 are usable**; 3 (`layerzero`, `mythril`, `snarkjs`) ship without a
`SKILL.md` and are skipped.

## How this is installed

This directory is a **clone** of the upstream repo (git-ignored — not vendored
into the workspace repo). Because Claude Code only discovers skills at
`.claude/skills/<name>/SKILL.md` (one level deep), each skill is **symlinked**
up one level so it loads as a real skill:

```
.claude/skills/hardhat            ->  blockchain-skills-external/skills/hardhat
.claude/skills/solidity           ->  blockchain-skills-external/skills/solidity
... (66 total)
```

So `/hardhat`, `/solidity`, `/foundry`, etc. work directly.

## Reinstall from scratch

```bash
# from the workspace root (/Volumes/ClaudeOs)
git clone --depth 1 https://github.com/hairyf/blockchain-skills.git /tmp/bskills
rsync -a --exclude='README.md' /tmp/bskills/ .claude/skills/blockchain-skills-external/
rm -rf /tmp/bskills

# symlink every skill that has a SKILL.md (skips incomplete + existing names)
for dir in .claude/skills/blockchain-skills-external/skills/*/; do
  name=$(basename "$dir")
  [ -f "$dir/SKILL.md" ] || continue
  [ -e ".claude/skills/$name" ] || ln -s "blockchain-skills-external/skills/$name" ".claude/skills/$name"
done
```

The symlinks are git-ignored via a generated block in the workspace
`.gitignore` (`BEGIN/END external blockchain skill symlinks`).

## Update

```bash
cd .claude/skills/blockchain-skills-external && git pull origin main
```

Then re-run the symlink loop above to pick up any **newly added** skills
(existing symlinks are left as-is). To prune symlinks whose skill disappeared
upstream, remove dangling links:

```bash
find .claude/skills -maxdepth 1 -type l ! -exec test -e {} \; -delete
```

> The upstream `sources/` are git submodules (heavy reference docs) and are
> **not** fetched — each skill's own `references/` folder is committed in the
> repo, so the skills are fully usable without them.
