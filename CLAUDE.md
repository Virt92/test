# Genealogy research workspace

This repo hosts the `ex-ussr-kinship-research` skill (`.claude/skills/`) for family-history research.
Follow the skill's SKILL.md workflow.

## Case data — never commit
- Case folders live in `kinship-cases/` (git-ignored: personal family data, the repo is public).
- If the folder is missing in a fresh session, ask the user to upload the latest case archive
  (`kinship-case-*.zip`) and unpack it into `kinship-cases/`.

## How to reach sources from the cloud session
- Run the session in the **"test (genealogy)"** environment: its network allowlist covers the archive sites.
- Browser: Playwright MCP (`.mcp.json`, tools `browser_*`), or plain Node scripts with
  `require('/opt/node22/lib/node_modules/playwright')` and `proxy: { server: process.env.HTTPS_PROXY }`.
- OBD «Мемориал» (obd-memorial.ru): works headless.
  - Search URL: `https://obd-memorial.ru/html/search.htm?f=P~<surname>&pb=T~<birthplace word>&entity=111111111111111&entities=24,28,27,23,34,22,20,21,8,6,10`
    (`pb` must be a whole word, e.g. `Веселянка`, `Вологодская`).
  - Result rows: `div.row.search-result` (row `id` = record id). Record: `https://obd-memorial.ru/html/info.htm?id=<id>`.
- Do NOT bypass protections; hand these to the user:
  - pamyat-naroda.ru — CAPTCHA;
  - collections.arolsen-archives.org — requires the user's own legal consent click;
  - ru.openlist.wiki — blocks cloud networks.
- podvignaroda.ru — returned "upstream request failed"; retry later.
- Log every search in the case `search-log.csv`; register finds in `artifact-register.csv`.
