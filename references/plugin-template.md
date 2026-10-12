# Claude Code plugin template for DuckDB extensions

Directory layout inside your extension repo:

```
<your-extension-repo>/
└── plugins/
    ├── .claude-plugin/marketplace.json     # so users can add YOUR repo directly
    └── <plugin-name>/                      # convention: duckdb-<extension-name>
        ├── .claude-plugin/plugin.json      # required manifest
        ├── README.md                       # install command + skill table
        └── skills/<skill-name>/SKILL.md    # 1..N skills, split by user problem domain
```

## plugin.json

```json
{
  "name": "duckdb-<extension>",
  "version": "<keep in sync with extension releases>",
  "description": "2-3 sentences: what the extension does and what the skills cover.",
  "author": { "name": "<you>" },
  "homepage": "https://github.com/<you>/<your-extension-repo>"
}
```

## SKILL.md discipline (what we verify before listing)

1. **frontmatter description = trigger, not marketing.** Pack it with scenario keywords so the agent picks it up from natural language ("Use when a query needs X and plain SQL doesn't cover it").
2. **Split skills by user problem domain**, not by internal module. 3-6 skills beat one giant file.
3. **Decision tree at the top** (90% of users need 3 lines) → quick reference → gotchas.
4. **Only SQL you have actually run.** Sources, in order of trust: README verified examples → registry `description.yml` hello_world → a probe against `INSTALL <name> FROM community`. Never write function signatures from memory.
5. Bump the `version` field with every extension release so skills don't rot.

## Marketplace entry (the one-line PR)

```json
{
  "name": "duckdb-<extension>",
  "description": "<one line, scenario keywords>",
  "source": { "source": "git-subdir", "url": "<you>/<your-extension-repo>", "path": "plugins/<plugin-name>" },
  "homepage": "https://github.com/<you>/<your-extension-repo>",
  "category": "data"
}
```

The entry `name` **must match** the `name` in your `plugin.json` exactly — that's the install id (`<name>@duckdb-extension-skills`).

## Verify before submitting

```bash
claude plugin validate plugins/<plugin-name>
```

Then double-check: `INSTALL <extension> FROM community; LOAD <extension>;` works on the current stable DuckDB, and one representative SQL snippet from each skill runs.
