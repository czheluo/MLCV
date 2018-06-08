---
layout: post
output: html_document
tags: [GWAS, ISR, Mult-loci model, Single-locus model,Simulation]
---

# ISR (Iterative screen regression )

<p style="text-align:justify">Here we introduce a new unique variable selection procedure of regression statistic method, call Iterative screening regression(ISR). Where we formulated a new regression information criterion (RIC) and used this criterion as the objective function of the entire variable screen process. We evaluate various model selection criteria through simulations, which suggest that the proposed ISR method performs well in terms of FDR and power. Finally, we show the usefulness of our approach by applying it to A. thaliana and mouse data.</p>

<div align="center"><img src="{{ "images/Blog/GWAS/ISRGWAS.jpg" | prepend: site.baseurl }}"></div>


# Simulation

<p style="text-align:justify">Human dataset derived from <a href="http://gigadb.org/dataset/view/id/100094/" target="_blank">PLINK</a> included two real human genotype datasets, the first dataset included  1000 samples and 100000 makers (SNPs) over all chromosomes. The second included 10000 samples(6000 cases and 4000 control) and 88058 markers (SNPs), and only included in 19, 20, 21, and 22 chromosomes. Also, another outbred <a href="https://datadryad.org/resource/doi:10.5061/dryad.2rs41" target="_blank"> CFW</a> (Carworth Farms White) mice population that including a set of 92,734 single-nucleotide polymorphism markers which were genotyped 1,161 individuals were also used to perform one simulation experiments. well, all simulation both setting the heritability was 0.5.

# Power versus FDR and TPR (Type one error)

## Mice simulation result


<div align="center"><img src="{{ "images/Blog/GWAS/micepower.jpg" | prepend: site.baseurl }}"></div>

## Human simulation result



<div align="center"><img src="{{ "images/Blog/GWAS/humanpower.jpg" | prepend: site.baseurl }}"></div>


# Estimated Effect (PVE)



<div align="center"><img src="{{ "images/Blog/GWAS/MICEPVE.jpg" | prepend: site.baseurl }}"></div>

<div align="center"><img src="{{ "images/Blog/GWAS/HUAMNPVE.jpg" | prepend: site.baseurl }}"></div>


#Real dataset

## Manhattan plot

Here is the matlab code for BMD GWAS Manhattan plot.

<a> {% include BMD_man.html %} </a>

# QQ plot

Here is the matlab code for BMD GWAS QQplot.

<!--div align="center"><img src="{{ "/images/Blog/.jpg" | prepend: site.baseurl }}"></div-->

<a>{% include BMD_qq.html %}</a>


