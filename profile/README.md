<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/amd-ph-core/.github/main/profile/phcore_header_dark.svg">
  <img src="https://raw.githubusercontent.com/amd-ph-core/.github/main/profile/phcore_header.svg" alt="ph-core — an initiative of the AMD Platform. nf-core-style tooling for public health pipelines and tools." width="760">
</picture>

Open, portable, reproducible Nextflow workflows for public health genomics, built and maintained by CDC's Office of Advanced Molecular Detection (OAMD).

[![Nextflow](https://img.shields.io/badge/nextflow%20DSL2-%E2%89%A524.10.4-23aa62?style=for-the-badge&labelColor=000000&logo=nextflow&logoColor=white)](https://www.nextflow.io/) [![run with docker](https://img.shields.io/badge/run%20with-docker-0db7ed?style=for-the-badge&labelColor=000000&logo=docker&logoColor=white)](https://www.docker.com/) [![run with singularity](https://img.shields.io/badge/run%20with-singularity-1d355c?style=for-the-badge&labelColor=000000)](https://sylabs.io/docs/) [![tested with nf-test](https://img.shields.io/badge/tested%20with-nf--test-337ab7?style=for-the-badge&labelColor=000000)](https://www.nf-test.com) [![license MIT-0](https://img.shields.io/badge/license-MIT--0-1a7f4f?style=for-the-badge&labelColor=000000)](https://opensource.org/license/mit-0) [![CDC AMD](https://img.shields.io/badge/CDC-Advanced%20Molecular%20Detection-0057B7?style=for-the-badge&labelColor=000000)](https://www.cdc.gov/advanced-molecular-detection/)

</div>

> [!IMPORTANT]
> **No PII or PHI permitted in this environment.** These repositories contain only non-sensitive, publicly available data and information. See the [standard notices](#notices) below.

## Intended Audience

This is where CDC's Office of Advanced Molecular Detection publishes bioinformatics software for public use: analysis workflows, reusable Nextflow modules, and configuration profiles. Container images used by these pipelines are published to [quay.io](https://quay.io/search?q=cdc-amd).

It is built for **public health bioinformaticians** running genomic surveillance in state, local, territorial, and tribal public health laboratories; for **academic and research laboratories** who want to run, adapt, or build on the same analyses; and for **CDC collaborators and partners** integrating with the AMD Platform. Everything published here is open source and free to use &mdash; no account, license request, or fee required. Anyone else is welcome to use it too.

---

## Start here

<table>
<tr>
<td width="25%" valign="top">

### 🧬 [Pipelines](#pipelines)

End-to-end, versioned analysis workflows for pathogen genomic surveillance. Run them straight from GitHub with `nextflow run`.

</td>
<td width="25%" valign="top">

### 🧩 [Modules](https://github.com/amd-ph-core/modules)

Tool-specific DSL2 process definitions shared across every pipeline &mdash; one tested implementation per tool.

</td>
<td width="25%" valign="top">

### ⚙️ [Configs](https://github.com/amd-ph-core/configs)

Institutional profiles, resource tuning, container settings, and reference-asset paths for AMD Platform environments.

</td>
<td width="25%" valign="top">

### 📦 [Reference data](https://cdc-amd-platform.s3.us-east-1.amazonaws.com/index.html)

Reference assets and test data the pipelines download at run time. Browse the bucket or pull any file directly &mdash; no credentials needed.

</td>
</tr>
</table>

### How it all fits together

<div align="center">

<a href="https://raw.githubusercontent.com/amd-ph-core/.github/main/profile/operational_architecture.svg">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/amd-ph-core/.github/main/profile/operational_architecture_dark.svg">
    <img src="https://raw.githubusercontent.com/amd-ph-core/.github/main/profile/operational_architecture.svg" alt="Operational architecture: code, sample sheet, reference assets, and containers are assembled by one nextflow run command into a five-stage pipeline that produces results and QC reports. Click to open full size." width="880">
  </picture>
</a>

<sub>Click the diagram to open it full size.</sub>

</div>

Code, input, reference assets, and containers come together in a single `nextflow run`
command. [`tbvarpipe`](https://github.com/amd-ph-core/tbvarpipe) is used here as a worked
example &mdash; the wiring is the same for every `ph-core` pipeline; only the pipeline name
and its processing stages change.

---

## Pipelines

Listed alphabetically. Every pipeline follows the [`ph-core` standards](#standards) and runs directly from this namespace.

| Pipeline | Description | Docs |
| --- | --- | --- |
| [`tbvarpipe`](https://github.com/amd-ph-core/tbvarpipe) | *Mycobacterium tuberculosis* WGS variant calling and lineage analysis | [Quickstart](https://github.com/amd-ph-core/tbvarpipe/blob/main/docs/quick_start_guide.md) |

```bash
nextflow run amd-ph-core/tbvarpipe -r 1.2.2 \
  -profile docker,amd \
  --input samplesheet.csv \
  --outdir results
```

More pipelines are on the way. This table lists everything that is public today; it grows as each one is released.

## Tools

Standalone bioinformatics tools maintained in this namespace. Listed alphabetically. Each one is installable on its own and is also packaged in the container images the pipelines use.

| Tool | Description | Docs |
| --- | --- | --- |
| [`srst2`](https://github.com/amd-ph-core/srst2) | Short Read Sequence Typing for bacterial pathogens &mdash; MLST and resistance/virulence gene detection direct from Illumina reads. A Python 3 maintenance fork of [`katholt/srst2`](https://github.com/katholt/srst2) for current bowtie2 / samtools | [README](https://github.com/amd-ph-core/srst2#readme) |

```bash
pip install git+https://github.com/amd-ph-core/srst2@v1.0.0
srst2 --version
```

## Shared components

| Component | Purpose |
| --- | --- |
| [`configs`](https://github.com/amd-ph-core/configs) | Configuration profiles and pipeline configs for AMD Platform environments |
| [`modules`](https://github.com/amd-ph-core/modules) | Tool-specific Nextflow DSL2 module files and their documentation |
| [`quay.io/us-cdcgov/cdc-amd`](https://quay.io/search?q=cdc-amd) | Public container images backing the pipelines &mdash; each one documents its key software, versions, licenses, and SBOM license summary |
| [`s3://cdc-amd-platform`](https://cdc-amd-platform.s3.us-east-1.amazonaws.com/index.html) | Public reference assets and test data used by the pipelines &mdash; browsable file listing, with anonymous downloads via `aws s3 --no-sign-request` |

---

## Standards

Pipelines, modules, and configs in this namespace are developed against the `ph-core` specification, a public health profile layered on top of the [nf-core](https://nf-co.re/) community standards:

- **Tier 1 &mdash; AMD Platform prerequisites.** Blocking requirements for platform deployment. &mdash; [checklist, 9 items](https://github.com/amd-ph-core/.github/blob/main/standards/Workflow-Checklist-v1.0.0-tier1-amd-platform-prerequisites.csv)
- **Tier 2 &mdash; `ph-core` requirements.** Structure, testing, containers, and documentation that every pipeline must follow. &mdash; [checklist, 31 items](https://github.com/amd-ph-core/.github/blob/main/standards/Workflow-Checklist-v1.0.0-tier2-ph-core-requirements.csv)
- **Tier 3 &mdash; `ph-core` recommendations.** Practices that improve portability, findability, and reuse. &mdash; [checklist, 107 items](https://github.com/amd-ph-core/.github/blob/main/standards/Workflow-Checklist-v1.0.0-tier3-ph-core-recommendations.csv)

Each checklist is the `v1.0.0` conformance list for that tier. Every row is one criterion, with the compliance and notes columns left blank so a file can be used directly as a review worksheet.

We gratefully acknowledge the [nf-core](https://nf-co.re/) community, whose templates, modules, and conventions this work builds upon.

## Open source and free to use

**Everything published in this namespace is fully open-source and free to use.** No account, license request, or fee is required.

- **Source code.** Released under the [MIT No Attribution license](https://opensource.org/license/mit-0) (`MIT-0`) &mdash; use it, modify it, redistribute it, no attribution required. CDC-authored material is a work of the U.S. Government and is in the public domain within the United States; see the [Public Domain Standard Notice](#notices). Source code derived from other open source projects retains its original license, recorded in that repository's `LICENSE` or `README`.
- **Third-party tools.** Every container image documents its key software, versions, and license files, together with an SBOM license summary. All identified licenses are open-source; no proprietary or commercial-only licenses are used.
- **Containers.** [`quay.io/us-cdcgov/cdc-amd`](https://quay.io/search?q=cdc-amd)

## Getting help

- Browse the documentation in each repository's `docs/` directory.
- Open an issue in the relevant repository for bugs and feature requests.
- General questions: [shareit@cdc.gov](mailto:shareit@cdc.gov)

---

## Notices

<details>
<summary><strong>Public Domain Standard Notice</strong></summary>

These repositories constitute a work of the United States Government and are not subject to domestic copyright protection under 17 USC § 105. They are in the public domain within the United States, and copyright and related rights in the work worldwide are waived through the [MIT No Attribution license](https://opensource.org/license/mit-0). All contributions to these repositories will be released under the same terms. By submitting a pull request you are agreeing to comply with this waiver of copyright interest.

</details>

<details>
<summary><strong>Disclaimer</strong></summary>

Use of this service is limited only to **non-sensitive and publicly available data**. Users must not use, share, or store any kind of sensitive data like health status, provision or payment of healthcare, Personally Identifiable Information (PII) and/or Protected Health Information (PHI), etc. under **ANY** circumstance.

Administrators for this service reserve the right to moderate all information used, shared, or stored with this service at any time. Any user that cannot abide by this disclaimer and Code of Conduct  may be subject to action, up to and including revoking access to services.

The material embodied in this software is provided to you "as-is" and without warranty of any kind, express, implied or otherwise, including without limitation, any warranty of fitness for a particular purpose. In no event shall the Centers for Disease Control and Prevention (CDC) or the United States (U.S.) government be liable to you or anyone else for any direct, special, incidental, indirect or consequential damages of any kind, or any damages whatsoever, including without limitation, loss of profit, loss of use, savings or revenue, or the claims of third parties, whether or not CDC or the U.S. government has been advised of the possibility of such loss, however caused and on any theory of liability, arising out of or in connection with the possession, use or performance of this software.

</details>

<details>
<summary><strong>License Standard Notice</strong></summary>

Software in this namespace is released under the [MIT No Attribution license](https://opensource.org/license/mit-0) (`MIT-0`), which permits free use, modification, and redistribution without an attribution requirement. Each repository carries its own `LICENSE` file, which governs that repository. Source code derived from other open source projects retains its original license, recorded in that repository's `LICENSE` or `README`, and third-party tools packaged in our container images remain under the licenses of their respective projects.

This software is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the Disclaimer above.

</details>

<details>
<summary><strong>Privacy Standard Notice</strong></summary>

This repository contains only non-sensitive, publicly available data and information. All material and community participation is covered by the Disclaimer above and the [Code of Conduct](https://github.com/CDCgov/template/blob/master/code-of-conduct.md). For more information about CDC's privacy policy, please visit [https://www.cdc.gov/other/privacy.html](https://www.cdc.gov/other/privacy.html).

</details>

<details>
<summary><strong>Contributing Standard Notice</strong></summary>

Anyone is encouraged to contribute to the repository by [forking](https://help.github.com/articles/fork-a-repo) and submitting a pull request. All contributions to this project will be released under the [MIT No Attribution license](https://opensource.org/license/mit-0). By submitting a pull request you are agreeing to comply with this waiver of copyright interest.

All comments, messages, pull requests, and other submissions received through CDC including this GitHub page may be subject to applicable federal law, including but not limited to the Federal Records Act, and may be archived. Learn more at [https://www.cdc.gov/other/privacy.html](https://www.cdc.gov/other/privacy.html).

</details>

<details>
<summary><strong>Records Management Standard Notice</strong></summary>

This repository is not a source of government records, but is a copy to increase collaboration and collaborative potential. All government records will be published through the [CDC web site](https://www.cdc.gov).

</details>

<details>
<summary><strong>Additional Standard Notices</strong></summary>

Please refer to [CDC's Template Repository](https://github.com/CDCgov/template) for more information about [contributing to this repository](https://github.com/CDCgov/template/blob/master/CONTRIBUTING.md), [public domain notices and disclaimers](https://github.com/CDCgov/template/blob/master/DISCLAIMER.md), and [code of conduct](https://github.com/CDCgov/template/blob/master/code-of-conduct.md).

</details>

<div align="center">

Maintained by the [Office of Advanced Molecular Detection](https://www.cdc.gov/advanced-molecular-detection/), Centers for Disease Control and Prevention

[www.cdc.gov](https://www.cdc.gov) &nbsp;·&nbsp; [github@cdc.gov](mailto:github@cdc.gov) &nbsp;·&nbsp; [shareit@cdc.gov](mailto:shareit@cdc.gov)

</div>
