# ACH research and illustrative PTX example

ACH is a proposed workflow for turning a bounded source corpus into checked findings, compact witnesses, and hypothesis-relative coverage records. This repository publishes the current architecture documents, the prompts, and one compact worked example so the method can be inspected and improved.

## Start here

- [Architecture and rationale](docs/architecture-and-rationale.md): the purpose and overall design.
- [Short specification](docs/short-specification.md): the current rules and limits.
- [Prompts](prompts/README.md): the task instructions, grouped by function.
- [Illustrative PTX run](examples/ptx-urination-illustrative/README.md): a retrospective example of compact output.
- [PTX run inputs](examples/ptx-urination-illustrative/README.md#ptx-run-inputs): the header, ranked index, deployed Archivist prompt, and selected FRD prompts.

## Status and limits

This is an architecture research record, not a validated research synthesis. The PTX example was selected and edited with hindsight to illustrate what a compact run might look like. It is not a real ACH run, a meta-analysis, a clinical recommendation, or a conclusion about pentoxifylline. The original 111 source conversions and historical validation workspaces are not distributed here. The [provenance index](examples/ptx-urination-illustrative/provenance-index.md) gives their project-relative locators and hashes where available.

The proposed workflow still needs tested controls for selection, source fidelity, compression, stopping, and semantic preservation. The documents record design proposals and experiments; they do not establish that ACH is already reliable for independent use.

The source folders used to prepare this publication copy were left unchanged. This repository contains a selected public presentation of the current specification and illustrative example, not the entire 1,624-file working folder.
