# Install nanoskills by agent

You are installing a set of agent skills that share one workflow. Read the whole
file first, then follow it in order — the one thing that breaks the install is
mistaking the repo root for a skill.

Install the nanoskills bundle from https://github.com/arinadi/nanoskills

Important: the repo root is NOT a skill. The skills live at skills/nanocrt/,
skills/nanostory/, and skills/nanoprd/. Cloning the repo directly into a skills
directory installs broken skills.

1. Work out which agent you are. Check for ~/.claude, ~/.config/opencode,
   .cursor, .codex, .windsurf, or .gemini.

2. If you are Claude Code, use the plugin marketplace:
       claude plugin marketplace add arinadi/nanoskills
       claude plugin install nanoskills@nanoskills
   Then skip to step 4.

3. Otherwise, clone once and install the skill directories only:
       git clone --depth 1 https://github.com/arinadi/nanoskills.git ~/src/nanoskills
   Link ~/src/nanoskills/skills/* into your agent's skills directory. The repo
   ships install.sh which does this for ~/.claude/skills (all skills in one run).

4. Verify: <skills dir>/nanocrt/SKILL.md, nanostory/SKILL.md, and
   nanoprd/SKILL.md must exist, and each frontmatter `name:` must match its
   folder. nanostory needs nanocrt installed alongside it (it reuses the
   storytelling reference).

Report which path you took and where it landed. Do not touch my other skills.