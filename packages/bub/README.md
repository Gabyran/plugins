# @magpie-community/agent-bub

[Bub](https://bub.build) as a magpie agent. magpie has no setup of its own for
Bub; with this plugin it is on magpie's Agents page like the agents magpie
ships with.

```sh
magpie plugin add @magpie-community/agent-bub
```

Then pick one of magpie's models in Bub's row. magpie writes into
`~/.bub/config.yml`:

```yaml
model: magpie:deepseek/deepseek-flash   # magpie's model, through the provider below
providers:
  magpie:
    type: openai
    api_base: http://127.0.0.1:3425/v1
    api_key: magpie-bub                 # Bub's own key, so Usage names it
```

Your comments, `fallback_models` and your own providers stay. Picking one of
Bub's own models again, `magpie bub default`, or switching it off puts every
key back as it was (a file that had no `providers:` is left with
`providers: {}`, which Bub reads). Restart `bub gateway` and open `bub chat`
sessions after a change: Bub reads its settings when it starts.

## The Bub it needs

A Bub that takes named providers under `providers:`
([bubbuild/bub#343](https://github.com/bubbuild/bub/pull/343), merged
2026-10-09). No release has it yet: 0.5.0 on PyPI doesn't. Until one does,
install Bub from its repository:

```sh
uv tool install --reinstall git+https://github.com/bubbuild/bub
```

A Bub without it fails every turn on a `magpie:` model, before any request
goes out: `'magpie' is not a supported provider`. If you see that, update Bub,
or pick one of Bub's own models in the row (or run `magpie bub default`) to put
the file back.

How agent plugins work: [usemagpie.ai/docs/plugins#agents](https://usemagpie.ai/docs/plugins#agents).
