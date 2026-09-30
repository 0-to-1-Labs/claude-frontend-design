# frontend-design (0 to 1 Labs)

A drop-in replacement for Anthropic's stock `frontend-design` skill. It is built on the
[September 2026 revision](https://github.com/anthropics/skills/blob/41bbe19/skills/frontend-design/SKILL.md)
of the upstream skill and adds four things the stock skill does not have:

- a one-sentence statement of the design direction before the plan and the code;
- font-loading mechanics (`display=swap` for hosted fonts, `preload` with `crossorigin`
  for self-hosted fonts, metric-matched fallbacks against layout shift);
- a concrete accessibility and responsive quality floor (WCAG AA contrast, visible
  keyboard focus, `prefers-reduced-motion`, semantic elements, no layout shift);
- triggers for the concrete things people ask for: components, pages, artifacts,
  posters, landing pages, dashboards, React components, HTML/CSS layouts, and restyling.

Everything else is the upstream text as published.

## Install

Via the [0 to 1 Labs marketplace](https://github.com/0-to-1-Labs/claude-marketplace):

```
/plugin marketplace add 0-to-1-Labs/claude-marketplace
/plugin install frontend-design@0-to-1-labs
```

## Replace the stock plugin

This plugin keeps the plugin name and the skill name `frontend-design` on purpose. Claude
invokes it automatically in the same situations as the stock skill. Only one skill named
`frontend-design` should load, so disable or uninstall the stock plugin:

```
/plugin disable frontend-design@claude-plugins-official
```

or

```
/plugin uninstall frontend-design@claude-plugins-official
```

If both plugins stay enabled, both skills load and both register as
`/frontend-design:frontend-design`. Claude Code does not pick one for you. Its documented
[name-conflict order](https://code.claude.com/docs/en/plugins/loading#name-conflicts)
applies only to plugins from different origins (managed settings, `--plugin-dir`,
marketplace, skills directory, claude.ai sync). Two installed marketplace plugins with the
same manifest name fall outside that rule. Claude then sees two skills with the same name
and chooses one from their descriptions on each request. You cannot tell from the session
which guidance ran, and `/frontend-design:frontend-design` is ambiguous.

## Keep the plugin updated

Claude Code can update this plugin automatically. Auto-update is off by default for
third-party marketplaces, so turn it on once:

1. Run `/plugin`.
2. Open the **Marketplaces** tab and select `0-to-1-labs`.
3. Choose **Enable auto-update**.

Claude Code then checks for new versions after each session start and installs them.
Restart Claude Code to load an update.

To update by hand:

```
claude plugin marketplace update 0-to-1-labs
claude plugin update frontend-design@0-to-1-labs
```

## What it does

The `frontend-design` skill loads when you build new UI or reshape existing UI. It follows
the upstream process: ground the design in the subject, plan a token system, review the
plan against the brief for generic defaults, then build. This fork adds the direction
statement, the font-loading rules, and the quality floor list described above.

## License

Apache License 2.0. See [LICENSE](LICENSE).

This is a derivative work of Anthropic's `frontend-design` skill
([anthropics/skills](https://github.com/anthropics/skills/tree/main/skills/frontend-design)),
which is licensed under Apache 2.0. `skills/frontend-design/SKILL.md` was modified from
the original by 0 to 1 Labs. Source: <https://github.com/0-to-1-Labs/claude-frontend-design>.
