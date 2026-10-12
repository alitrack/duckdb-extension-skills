# duckdb-extension-skills

One Claude Code marketplace for DuckDB extension skills — verified, source-checked, maintained by the people who build the extensions.

```
/plugin marketplace add alitrack/duckdb-extension-skills
```

Then install any plugin:

```
/plugin install duckdb-luajit@duckdb-extension-skills
/plugin install duckdb-skills@duckdb-extension-skills      # official DuckDB team skills
/plugin install anofox-forecast@duckdb-extension-skills    # DataZoo time-series forecasting
```

## Why

The official [`duckdb-skills`](https://github.com/duckdb/duckdb-skills) plugin teaches agents to *use the DuckDB CLI* — read files, run queries, install extensions (`INSTALL x FROM community` is one command away). But after an extension is installed, the agent still doesn't know the extension's functions. This marketplace fills that gap: **one entry per extension, with SQL that has been tested against the real binary**.

## Catalog

| Plugin | Extension | What it does | Maintainer |
|:---|:---|:---|:---|
| `duckdb-skills` | (core CLI) | Read any file, query, docs search, install extensions | [duckdb](https://github.com/duckdb) (official) |
| `duckdb-luajit` | `luajit` | LuaJIT UDFs/tables, 40+ libs: incremental ETL/SCD2, CN e-invoice/OFD/TDX, entity resolve, privacy | [alitrack](https://github.com/alitrack) |
| `duckdb-dq` | `dq` | expect_* assertions, profiling, quality reports | [alitrack](https://github.com/alitrack) |
| `duckdb-raster` | `s2raster` | GeoTIFF I/O, S2 cell math | [alitrack](https://github.com/alitrack) |
| `duckdb-ml` | `ml` | 30+ ML algorithms trained & scored in SQL | [alitrack](https://github.com/alitrack) |
| `duckdb-orc` | `orc` | Apache ORC reader | [alitrack](https://github.com/alitrack) |
| `duckdb-petgraph` | `petgraph_ext` | Graph algorithms on edge tables | [alitrack](https://github.com/alitrack) |
| `duckdb-turbovec` | `turbovec` | Compressed vector search (ANN) | [alitrack](https://github.com/alitrack) |
| `duckdb-python-udf` | `python_udf` | Persistent Python UDFs | [alitrack](https://github.com/alitrack) |
| `anofox-forecast` | `anofox_forecast` | 36 time-series models, backtesting, changepoints | [DataZoo](https://github.com/DataZooDE) |
| `anofox-statistics` | `anofox_statistics` | OLS/GLM/mixed-effects, hypothesis tests | [DataZoo](https://github.com/DataZooDE) |

## Contributing — extension maintainers welcome

Your repo already ships a `plugins/<name>/` directory with a Claude Code plugin? Listing it here is a **one-line PR**: add an entry to [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json) and a row to the catalog table above. No code is copied into this repo — the marketplace references your repository directly, so your skills stay where you maintain them.

### Inclusion criteria

1. **Listed in the [community-extensions registry](https://duckdb.org/community_extensions/list_of_extensions)** (or an official core extension) — `INSTALL <name> FROM community` must work.
2. **SQL is tested, not recalled.** Every SQL snippet in the skill comes from your README's verified examples, the registry's `hello_world`, or a probe run against the real binary. Wrong function signatures are worse than no skill.
3. `claude plugin validate <your-plugin-dir>` passes.
4. **You are the extension's maintainer** (or have their blessing). Skills are attributed to the provider — we don't write skills for other people's extensions without asking first.
5. License of the *skill content* permits redistribution (the plugin directory in your repo, not necessarily the extension binary).

### No plugin yet?

The [template used by the plugins here](references/plugin-template.md) is a directory with a `.claude-plugin/plugin.json`, a `README.md`, and `skills/<skill-name>/SKILL.md` files. Point the `SKILL.md` description at real scenarios ("Use when a query needs X and plain SQL doesn't cover it"), put a decision tree up front, and only include SQL you have run.

## Relationship to the official plugin

`duckdb-skills` (the DuckDB team's plugin) is listed here by reference, not copied. Their skills cover the CLI layer; the entries here cover individual extensions. Installing both from this one marketplace is the intended workflow. If the DuckDB team ever starts listing community extension skills themselves, we'll happily contribute this catalog upstream.

## License

MIT. Each plugin keeps its own license — see the linked repositories.

## Alternatives / related

- [duckdb/duckdb-skills](https://github.com/duckdb/duckdb-skills) — official CLI-layer skills
- [motherduckdb/agent-skills](https://github.com/motherduckdb/agent-skills) — MotherDuck-specific skills
- [duckdb/community-extensions](https://github.com/duckdb/community-extensions) — the extension registry itself
