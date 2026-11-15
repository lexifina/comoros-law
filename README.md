# Comoros: law history in git


The Comoros' law as a git history, on the design every country here shares: one file per unit, one commit per version on the day recorded for it, and the record that made each change as the commit's author. For now it holds no law text, only facts: the Comoros' treaty actions, a short catalogue of its laws, and facts about its legal system. `git blame` names the record behind every line; `git log` lists every action on a treaty; picking a date gives the record as it stood that day.

Part of [lexifina/global-law](https://github.com/lexifina/global-law), one git history for every country's law: this is the Comoros' national law, which global-law reads at `comoros/national/acts/`.

**What is in it now:** no law text. [`un-treaties/`](un-treaties/README.md) records the Comoros' 55 actions (20 signatures, 19 accessions, 15 ratifications and 1 acceptance) on 40 multilateral treaties deposited with the UN Secretary-General, on 38 days from 9 December 1975 to 4 June 2021; [`wipo-treaties/`](wipo-treaties/README.md) holds WIPO Lex's record of 41 treaties the Comoros has joined or signed, one version each; [`catalogue/`](catalogue/README.md) lists the 11 laws WIPO Lex records for the Comoros (title, subject, dates and link), among them the 2018 Constitution; and [`legal-system/`](legal-system/README.md) holds 13 files of facts about the state from Wikidata, in one version; they are not law. [`REPRODUCE.md`](REPRODUCE.md) says how the files were made.

**Why there is no law text.** The Ministry of Justice publishes laws at [justice.gouv.km](https://justice.gouv.km), but its legal notice forbids reproducing its content without prior authorisation, and the Journal officiel is not online. The only national copyright law on record, the Law of 11 March 1957 (a French law), does not exclude laws from protection. The laws will be added if that changes.

Each UN treaty is one file named from its number in the UN Treaty Collection: `un-treaties/untc-iv-11.md` is the Convention on the Rights of the Child (IV-11). WIPO Lex records are named from its ids: `wipo-treaties/treaty-19793.md` is the Paris Agreement, `catalogue/law-20721.md` the Constitution of the Union of the Comoros.

The records are in English, with names as Wikidata, the UN Treaty Collection and WIPO Lex give them.

## Questions as git commands

| Question | Command |
| --- | --- |
| Every action the Comoros took on the Convention on the Rights of the Child | `git log -p --word-diff -- un-treaties/untc-iv-11.md` |
| Which treaty action wrote each line? | `git blame un-treaties/untc-iv-11.md` |
| Every version of the Convention's record, with the day of each | `git log --format="%h %(trailers:key=In-force,valueonly,separator=) %an" -- un-treaties/untc-iv-11.md` |
| The record as it stood on 1 January 1992 | `python tools/on.py 1992-01-01 un-treaties untc-iv-11` |

**Outside git**, we also host this record publicly, for free:

- **[Ask Claude about the Comoros](https://global-law.lexifina.com/v1/try_claude?country=comoros)**: opens Claude with a first question ready.
- **[Ask ChatGPT](https://global-law.lexifina.com/v1/try_chatgpt?country=comoros)**: the same question in ChatGPT.
- **[Search the Comoros' record on our site](https://lexifina.com/law?country=comoros&q=Rights+of+the+Child)**: a search for "Rights of the Child" in its catalogue of titles, no account needed.
- **[Developer REST API](https://global-law.lexifina.com/v1/search_law?query=Rights+of+the+Child&jurisdiction=comoros)**: the same search as JSON, with no key. See the [documentation here](https://lexifina.com/api/global-law).

Both assistants read the record through the free Global law connector (MCP, `https://global-law.lexifina.com/mcp`); the first time, the chat gives you the link that adds it. Ask in English or in French.

**Host it yourself easily.** All it takes is git and Python, and the tools run on your machine:

```sh
git clone --depth 1 https://github.com/lexifina/global-law && cd global-law
python3 tools/countries.py add comoros/national/acts
python3 tools/law.py show 2026-01-01 comoros/national/acts/un-treaties/untc-iv-11.md
```

Opened in Claude Code, Cursor, VS Code or Codex, the clone also starts a local MCP server with the same tools ([MCP.md](https://github.com/lexifina/global-law/blob/main/MCP.md)).

## Dates

Each commit is dated at noon, Indian/Comoro, on the day recorded for the entry, and carries it in its `In-force:` trailer:

- a UN treaty action, by the day the UN Treaty Collection records for it (signature, ratification, accession or acceptance); it is the day of the action, not the day the treaty came into force for the Comoros;
- a WIPO Lex treaty, by the Comoros' ratification, accession or similar instrument (37 of 41), else its entry into force for the Comoros, else its signature;
- a catalogue law, by the date WIPO Lex records (promulgation, entry into force, commencement or adoption, in that order); WIPO Lex dates the Law of 5 July 1844 on patents to 1884, and the title's 1844 is used;
- git cannot store dates before 1970, so the 7 earlier commits (catalogue laws of 1844 to 1965) are dated from 1970-01-01, one second apart, with the real day in `In-force:`. Ask for a date with `tools/on.py`, not `git log --before`.

Each UN treaty action is credited to the action (`Ratification: Convention on the Rights of the Child ...`), each WIPO Lex treaty to the treaty, and catalogue entries to their day (`Catalogue entries of 2018-08-06`), each with an e-mail address that cannot exist; these are records, not laws. The first version of each treaty list, and the Wikidata facts (one version, dated 30 October 2026, the day they were read), are credited to the publisher, `Lexifina (compiled from Wikidata, the UN Treaty Collection and WIPO Lex)` (`Kind: publisher`). The committer is Lexifina.

## How it is checked

- `tools/check_repo.py` reads every version back from git on the day it took effect and on the day before and compares it with the corpus, whose hash is in `data/corpus.sha256`; it also checks that every commit's trailers parse, that `main` has no merge commits and that no commit is dated in the future. [`REPRODUCE.md`](REPRODUCE.md) records 79 versions read back with no mismatch.
- `tools/build.py` writes the history from that one corpus file, and the same corpus gives the same commit hashes; no second build has been compared yet.
- Only facts are taken from the sources: each file holds a name, dates and the page they came from, and no text of any law or treaty.

## What it does not show

- **Law text.** No code, act or constitution, for the reason above. The catalogue is the short list WIPO Lex holds, mostly intellectual-property laws, several of them French laws applied in the colony; it is not a list of the Comoros' statutes.
- **Most treaty actions.** The UN list covers the 78 status pages read, and WIPO Lex lists only the treaties it tracks; bilateral treaties are not here.
- **Reservations and declarations.** The treaty files give names and dates only.
- **A dated history of the facts.** Wikidata keeps none, and it can be incomplete or wrong.

## Sources

| Source | Kind | Past versions | Notes |
| --- | --- | --- | --- |
| [United Nations Treaty Collection](https://treaties.un.org/) | Status pages of multilateral treaties deposited with the UN Secretary-General | yes, each action on its day | Facts only: treaty names and the dates of the Comoros' actions; read on 29 October 2026 |
| [WIPO Lex](https://www.wipo.int/wipolex/en/members/profile/KM) (World Intellectual Property Organization) | Member profile: catalogue of laws, treaty actions | no, one record per law or treaty | Titles, subjects, dates and links; no text; read on 30 October 2026 |
| [Wikidata](https://www.wikidata.org/wiki/Q970) | Facts about the state (CC0), not law | no, one reading | Read on 30 October 2026 |

## Licence

See [`LICENSE`](LICENSE). The Wikidata facts are CC0 1.0; from the UN Treaty Collection only facts are taken, the treaty names and the dates of treaty actions, credited to its status pages; WIPO Lex content is under CC BY 4.0, and only facts are copied from it. Lexifina's history, commit messages, tables and tools are CC0 1.0.

No AI model wrote, translated or corrected legal text; the scripts were written by an AI model, and no model runs when the history is built (see [`REPRODUCE.md`](REPRODUCE.md)).

## More

From [lexifina/global-law](https://github.com/lexifina/global-law):

- [FEATURES.md](https://github.com/lexifina/global-law/blob/main/FEATURES.md): every feature, and what every corpus must support (`git blame`, `law.py`, the MCP tools)
- [FAQ.md](https://github.com/lexifina/global-law/blob/main/FAQ.md): questions and answers · [CONTRIBUTING.md](https://github.com/lexifina/global-law/blob/main/CONTRIBUTING.md): proposing changes · [MCP.md](https://github.com/lexifina/global-law/blob/main/MCP.md): the MCP server · [REPRODUCE.md](https://github.com/lexifina/global-law/blob/main/REPRODUCE.md): how it was built · [CHANGELOG.md](https://github.com/lexifina/global-law/blob/main/CHANGELOG.md)
- [FRESHNESS.md](https://github.com/lexifina/global-law/blob/main/FRESHNESS.md): how current each corpus is · [Monitoring](https://github.com/lexifina/global-law/tree/main/monitoring): whether updates are running · [WATCHING.md](https://github.com/lexifina/global-law/blob/main/WATCHING.md): how each official source is watched for changes
- [performance/](https://github.com/lexifina/global-law/tree/main/performance): how fast the tools are, measured
- [visualisations/](https://github.com/lexifina/global-law/tree/main/visualisations): charts and bridges across the world's law
- [Vulnerabilities](https://github.com/lexifina/global-law/tree/main/vulnerabilities): mistakes in legislation as published
