## Submit an overleaf project to arxiv

1. Convert all figures to .eps format.
2. Make sure the `.bib` file has the same name as your main `.tex` file. arxiv requires the `.bbl` file to compile, so we need the following step to obtain the `.bbl` file.
3. Click the `submit` button on the top right of overleaf, and select `arxiv`.
4. Submit the downloaded zip file to arxiv.



## Tips

 - When using numeric citation style, specify `\bibliographystyle{unsrt}`, and `\PassOptionsToPackage{numbers, compress}{natbib}` for NeurIPS template or `\usepackage[numbers, sort&compress]{natbib}` for general template.
