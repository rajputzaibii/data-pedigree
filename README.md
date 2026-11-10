# Data Pedigree

**Check whether the data behind a research paper is actually available.**

Paste a DOI or a paper title, and Data Pedigree reads the paper's data availability statement and gives a plain-language answer:

| Result | Meaning |
|---|---|
| ✅ **Data available** | Data is in a public repository (Zenodo, Dryad, NCBI, OSF, …) or in the supplementary files. A link is shown. |
| ⚠️ **Available on request** | Data is not public; the authors must be asked. The tool drafts a polite request email. |
| ❌ **Not available** | No statement, data restricted (licence, company, privacy), or explicitly not shared. |

🔗 **Live site:** https://YOUR-USERNAME.github.io/data-pedigree/ *(replace after publishing)*

---

## Why I built this

In a class discussion about peer review, I asked my professor how reviewers know that published results are really supported by data. The answer was that it is often a matter of trust, and sometimes reviewers ask for the data.

That made me curious. Research on data sharing shows the problem is real:

- Only about **1 in 7** authors who promised data "on request" shared it or agreed to, when 1,634 were asked ([Acciai et al., 2023](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10120507/)).
- The odds that a dataset still exists fall by **17% per year** after publication ([Vines et al., 2014](https://doi.org/10.1016/j.cub.2013.11.014)).

Professional tools exist (ODDPub, DataSeer, Dimensions Research Integrity), but they are built for publishers and institutions. I wanted a simple, free tool that any student can use on a single paper.

## How it works

1. **Find the paper:** looks up the DOI or title in [Crossref](https://www.crossref.org).
2. **Read the data statement:** for open-access papers, fetches the full text from [Europe PMC](https://europepmc.org), finds the data availability section and extracts repository links and accession numbers (e.g. `PRJNA…`, `GSE…`).
3. **Check dataset records:** searches [DataCite](https://datacite.org) for datasets officially linked to the paper, which can work even for paywalled papers.
4. **Classify** the statement into one of the three results using keyword rules.

It recognises 45+ repositories across fields: general (Zenodo, Figshare, Dryad, OSF, Dataverse), life sciences (NCBI, ENA, GEO, PDB, PRIDE), breeding and agriculture (e!DAL, Breedbase, T3, Ag Data Commons), ecology (GBIF, PANGAEA), social science (ICPSR, UK Data Service, GESIS) and more.

## Privacy and security

- No server, no accounts, no database: the whole site is one static HTML file.
- Searches go directly from the visitor's browser to the three public databases.
- A Content Security Policy blocks the page from contacting any other site.
- Emails are never sent by the site. They open in the user's own email app.

## Testing

I tested the tool on real papers from my field and compared its answer with my own reading of each paper. See [`testing/validation.csv`](testing/validation.csv).

| Papers tested | Tool agreed with me | Open access | Paywalled |
|---|---|---|---|
| *fill in* | *fill in* | *fill in* | *fill in* |

**What I learned from testing:** *(write 2–3 sentences: where it worked well, where it failed, and why)*

## Limitations

- Full text is only readable for open-access papers indexed in Europe PMC (strongest for life sciences).
- Classification uses keyword rules, so unusual wording can be misread.
- It checks whether data is *available*, not whether it is complete or whether the results are correct.

## How this was built

The idea, scope, design decisions and testing are mine. The code was written with an AI assistant (Claude by Anthropic), which I directed through many rounds of changes: defining the three result types, replacing automatic emailing with a user-sent email for credibility and spam reasons, widening it from breeding to all fields, and redesigning the interface.

## Roadmap

- [ ] Check whether repository links still work (dead-link detection)
- [ ] Batch mode: check a list of DOIs at once
- [ ] Better support for paywalled papers

## License

MIT
