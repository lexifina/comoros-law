# How this repository was made (Comoros)

This file is written by the build on 2026-10-30, the day the source data was retrieved.

## Sources

| Source | Address | Retrieved | Licence |
| --- | --- | --- | --- |
| Wikidata (CC0) | <https://www.wikidata.org/wiki/Q970> | 2026-10-30 | CC0 1.0 Universal |
| UN Treaty Collection (MTDSG status pages) | <https://treaties.un.org/> | 2026-10-29 | Facts only (treaty action, date, depositary); no text copied |
| WIPO Lex member profile | <https://www.wipo.int/wipolex/en/members/profile/KM> | 2026-10-30 | WIPO content: CC BY 4.0 (https://www.wipo.int/web/terms-of-use); only facts copied |

Every word of law in this repository comes from these sources. Lexifina reads them and records each act's dated versions, and the laws that made each change, in one corpus file. This repository is built from that file.

## What is in it

| Act | Title | Versions | Span |
| --- | --- | ---: | --- |
| `legal-system` | Comoros: legal system, from Wikidata (facts only) | 1 | 2026-10-30 to 2026-10-30 |
| `un-treaties` | Treaty actions of Comoros on multilateral treaties deposited with the UN Secretary-General (UN Treaty Collection; no treaty text) | 38 | 1975-12-09 to 2021-06-04 |
| `catalogue` | Catalogue of laws of Comoros recorded by WIPO Lex (title, date, link only; no law text) | 11 | 1844-07-05 to 2018-08-06 |
| `wipo-treaties` | Treaty actions of Comoros recorded by WIPO Lex (facts only; no treaty text) | 29 | 1985-01-15 to 2026-06-11 |

The build made 108 commits:

| Commits | Kind |
| ---: | --- |
| 4 | first version of an act |
| 104 | one law on its in-force day |
| 0 | changes no amendment note explains, credited to the publisher |

Other counts:
- 0 commits on the branch `future`: laws not yet in force on 2026-10-30.
- 7 commits dated 1 January 1970: in force before 1970, with the real day in their `In-force` trailer.
- 107 laws in the record.
- 184 tags.

## Dates

Each commit is dated at noon (Indian/Comoro) on the day the change took effect. The other dates, enacted and published, are trailers.

When a law gives no date of its own, the default rule applies: Not applicable: this record holds facts and treaty actions, not law text. Each treaty action is dated by the day the depositary records for it; the Wikidata facts carry the day they were read. https://treaties.un.org/

## How the history is built

`tools/build.py` turns the corpus into this history in one pass: one commit per law, on the day it took effect. The same corpus always gives the same commit hashes. `tools/check_repo.py` reads every version back from git and compares it with the corpus. `tools/on.py` shows the law as it stood on any date. The corpus format is described in `tools/SCHEMA.md`.

- Corpus: sha256 `8f47adcd9966df36e181093fd1075e70f47cd5cef9bb71ff7389154fc364fee9` (479351 bytes).
- Builder blob hashes (`git hash-object`): `build.py` `a4faa25af85facb64b956b372f6b528aafdd7ec1`, `check.py` `3d00541d258745461ab52b1b0cb4e1716a27a95d`, `on.py` `644a6c0857fbcc72562032b58d57aa113fee0641`.
- Python 3.12.10; git version 2.46.0.windows.1.

## Checks

79 versions of 4 acts read back from git on the day each took effect and on the day before: 0 mismatches. Trailers: 0 commits whose trailers git cannot parse. Health: 0 merge commits on main, 0 commit dates that go backwards, 0 commits dated after the build.

No second build of this corpus has been compared yet.

## Decisions made by hand

- Comoros is held back from publishing law text, so this repository records facts only: Wikidata facts, treaty actions from the UN Treaty Collection and WIPO Lex, and a catalogue of the laws WIPO Lex lists.
- Wikidata has no dated history for the facts in legal-system, so that act is one version, the oldest available, dated on the day it was read.
- UN Treaty Collection: 40 multilateral treaties deposited with the UN Secretary-General, with the state's signature, ratification, accession, succession, acceptance or approval dates. Facts only; one version per action date, with the first version credited to the action. Treaties outside the 78 status pages read are not listed.
- WIPO Lex: 11 laws from the member profile dated by the date WIPO Lex records (promulgation, entry into force, commencement, adoption, in that order); 0 laws with no recorded date are left out. Treaty actions: 41. Titles, dates and links only; no text. WIPO Lex gives some laws only 'January 1' of a year, a placeholder rather than a known date.
- The Ministry of Justice site (justice.gouv.km) forbids reproduction without authorisation, and the only national exemption candidate, the Law of 11 March 1957 on Literary and Artistic Property (a French law), has no clause excluding laws from protection, so no law text is published.
- WIPO Lex gives July 5, 1884 as the adoption date of the "Law of July 5, 1844, on Patents for Inventions"; the title and the French statute say 1844, so the catalogue uses 1844-07-05.

## What AI did and did not do

The scripts that read the sources and build this repository were written by Claude Code running Claude Opus 5.5 (`claude-opus-5-5`) under Lexifina's direction.

No model wrote, translated or corrected legal text. No model runs at build time. Every word of law in this repository comes from the official sources above.

The commit messages are written by `build.py` from the source data.

Model use at data-build time:
- none
