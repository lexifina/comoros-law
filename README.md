# Comoros: law history in git (metadata only, no law text)

**This repository holds no law text.** The text of Comoros's laws is not published here because the Ministry of Justice site says its content may not be reproduced without prior authorisation, and the Journal officiel is not online. What is here is facts only, so the repository has something real in it and the history can grow when the laws can be added.

It follows the shared design of [lexifina/global-law](https://github.com/lexifina/global-law): one file per unit, one commit per record on its day, and the record that made each change as the commit's author.

**What is in it now**

| Folder | Content | Versions | History |
| --- | --- | ---: | --- |
| `legal-system/` | Facts from Wikidata: government, institutions, legal instruments recorded there | 1 | Read on 2026-10-30 (no dated history exists) |
| `un-treaties/` | Treaty actions at the UN Treaty Collection (40 multilateral treaties deposited with the UN Secretary-General) | 38 | One version per day with an action, 1975 to 2021 |
| `wipo-treaties/` | Treaty actions recorded by WIPO Lex (WIPO-administered treaties and others it tracks) | 29 | One version per action day, 1985 to 2026 |
| `catalogue/` | Catalogue of the laws WIPO Lex lists for Comoros: title, subject, date, link only | 11 | Dated by the date WIPO Lex records (the earliest is the French Law of 5 July 1844 on patents) |

**Language.** English. Names are as given by Wikidata and the UN Treaty Collection.

## Sources

- Wikidata, under CC0 (https://www.wikidata.org/wiki/Q970): facts about Comoros and records that its legal instruments exist.
- UN Treaty Collection (https://treaties.un.org/): treaty names and the dates of signature, ratification, accession or succession, for the multilateral treaties deposited with the UN Secretary-General whose status pages were read (78). This is not a full list of the state's treaty actions.
- WIPO Lex member profile (https://www.wipo.int/wipolex/en/members/profile/KM), content under CC BY 4.0: facts only (law titles, subject, dates, links; treaty names, administering organisation and dates). WIPO Lex gives the Law of 5 July 1844 on patents an adoption date of 1884; the title says 1844, so 1844 is used.

## Dates

The treaty histories are dated by the day the depositary or WIPO Lex records for each action, and the catalogue by the date WIPO Lex records for each law. The Wikidata facts have no dated history, so they are one version dated on the day they were read (2026-10-30).

## How it is checked

Every version is read back from git on the day it took effect and on the day before (`tools/check_repo.py`) and must match `corpus.json`; results are in `REPRODUCE.md`.

## What "author" means

The author of a commit is the record that made the change, with an e-mail address that cannot exist. The committer is always Lexifina.

## Limits

No law text. Wikidata can be incomplete or wrong. The treaty lists cover only the treaties whose status pages were read. The catalogue is the short list WIPO Lex holds, mostly intellectual-property laws, several of them French laws applied in the colony; it is not a list of Comoros's statutes.
