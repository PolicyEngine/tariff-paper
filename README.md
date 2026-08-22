# Tariff rate constructs

This repository contains the working paper “Tariff rate constructs for the 2025–26 trade shock: weights, scope, and synthetic customs entries.” The assembled manuscript source is `paper.md`; section sources are retained in `drafts/`; the committed publication artifact is `build/paper.pdf`.

## Build

Install [Pandoc](https://pandoc.org/) with citeproc support and [XeLaTeX](https://tug.org/xetex/), then run from the repository root:

```sh
pandoc paper.md -o build/paper.pdf --citeproc --include-in-header=build/pdf-preamble.tex --pdf-engine=xelatex
```

## License

The manuscript is licensed under the [Creative Commons Attribution 4.0 International License](LICENSE). Third-party software, data, and other separately identified materials retain their own licenses.
