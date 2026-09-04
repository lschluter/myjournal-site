# myjournal-site

The public pages for **MyJournal**, an Android journaling app. Served by GitHub Pages at
<https://lschluter.github.io/myjournal-site/>.

This repository exists because Google Play requires the privacy policy at a publicly accessible URL,
and the app's own repository is private.

## Do not edit `privacy/` here

Everything under `privacy/` is **generated**. It is rendered from the app repository's
`docs/privacy-policy.md` and `docs/privacy-policy.pt-BR.md` and pushed here by CI, so that the
published policy cannot drift from the code whose behaviour it describes. An edit made directly in
this repository will be silently overwritten on the next sync, and a weekly job fails if the two
ever disagree.

To change the policy, change it in the app repository.

`index.md`, `support.md` and `_config.yml` are hand-written and do live here.

## Layout

| Path | |
|---|---|
| `/` | Landing page |
| `/privacy/` | Privacy policy (English) — the URL registered in Play Console |
| `/privacy/pt/` | Privacy policy (Português) |
| `/privacy/vN/` | Permanent copy of disclosure version N, kept so users can re-read what they agreed to |
| `/support/` | Support and security reporting |
