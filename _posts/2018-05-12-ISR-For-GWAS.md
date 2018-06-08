---
layout: post
comments: true
output: html_document
category: [BMD_man,BMD_qq]
tags: [GWAS, ISR, Mult-loci model, Single-locus model,Simulation]
---

# ISR (Iterative screen regression )

<p style="text-align:justify">Here we introduce a new unique variable selection procedure of regression statistic method, call Iterative screening regression(ISR). Where we formulated a new regression information criterion (RIC) and used this criterion as the objective function of the entire variable screen process. We evaluate various model selection criteria through simulations, which suggest that the proposed ISR method performs well in terms of FDR and power. Finally, we show the usefulness of our approach by applying it to A. thaliana and mouse data.</p>

<div align="center"><img src="{{ "/images/Blog/GWAS/ISRGWAS.jpg" | prepend: site.baseurl }}"></div>


# Simulation

<p style="text-align:justify">Human dataset derived from <a href="http://gigadb.org/dataset/view/id/100094/" target="_blank">PLINK</a> included two real human genotype datasets, the first dataset included  1000 samples and 100000 makers (SNPs) over all chromosomes. The second included 10000 samples(6000 cases and 4000 control) and 88058 markers (SNPs), and only included in 19, 20, 21, and 22 chromosomes. Also, another outbred <a href="https://datadryad.org/resource/doi:10.5061/dryad.2rs41" target="_blank"> CFW</a> (Carworth Farms White) mice population that including a set of 92,734 single-nucleotide polymorphism markers which were genotyped 1,161 individuals were also used to perform one simulation experiments. well, all simulation both setting the heritability was 0.5.

# Power versus FDR and TPR (Type one error)

## Mice simulation result


<div align="center"><img src="{{ "/images/Blog/GWAS/micepower.jpg" | prepend: site.baseurl }}"></div>

## Human simulation result



<div align="center"><img src="{{ "/images/Blog/GWAS/humanpower.jpg" | prepend: site.baseurl }}"></div>


# Estimated Effect (PVE)



<div align="center"><img src="{{ "/images/Blog/GWAS/MICEPVE.jpg" | prepend: site.baseurl }}"></div>

<div align="center"><img src="{{ "/images/Blog/GWAS/HUAMNPVE.jpg" | prepend: site.baseurl }}"></div>


# Real dataset

## Manhattan plot
Here is the matlab code for BMD GWAS Manhattan plot.

```matlab
load manha.mat
[nsnp,phe]=size(mlssr);nchr=length(unique(chr));
figure("Position",[0 200 1000 500])
%nasnp=label(lm);
%dims = size(nasnp);
k=1;
f(1,1)=mlssr(1,2)+2000000;
for i=2:1:nsnp
   if mlssr(i,1)~= mlssr(i-1,1)
    f(i,1)=f(i-1,1)+mlssr(i,2)+2000000;
    x(k)=f(i,1)-1000000;
    if k>1 
    xg(k)=(f(i-1,1)-x(k-1))/2+x(k-1);
    ch(k)=mlssr(i-1,1);
    else
    xg(k)=f(i-1,1)/2-mlssr(1,2)/2;
    end
    k=k+1;
   else
   f(i,1)=mlssr(i,2)-mlssr(i-1,2)+f(i-1,1); 
   ch(k)=mlssr(i-1,1);
    end 
end
xg(k)=(f(i,1)-x(k-1))/2+x(k-1);
ch(k)=mlssr(i,1);
for j=3:1:phe
for i=1:1:nsnp
    f(i,j-1)=-log10(mlssr(i,j));
end
i=1;
end
j=1;
for j=1:1:(phe-2)
    figure(j);
    cl=load('colorchrhg.txt');ncl=randperm(length(cl(:,1)));cl=cl(ncl,:);
    %cl=cl(1:nchr,:);% all kinds of color 
    scatter(f(:,1),f(:,j+1),10,cl(chr,:),'o','filled');%cl(mod(mlssr(:,1),nchr)+1,:)/1
    %display the gene name or not
    %text(f(lm,1),f(lm,j+1)+.15*4, nasnp(:,1:dims(2)),'FontSize', 10);
    chrs = unique(chr);
    chrs = chrs(:)';%p0=0;
  for c = chrs
      % Plot the SNPs on the chromosome.
      is = find(chr == c);
      maxpos = max(pos(is));
     % load cl.mat
      if ~isodd(c)
          %clr = unifrnd(0,1,1,3);
          clr=cl(c,:);
      else
          %clr = unifrnd(0,1,1,3);
          clr=cl(c,:);
      end
      % Add the chromosome number.
      %for il=1:nchr
      text(xg(c),-0.15* (max(-log10(plm)) - min(-log10(plm))),num2str(c),...
          'Color',cl(c,:),'FontSize',9,'HorizontalAlignment','center',...
          'VerticalAlignment','bottom','FontName','Times New Roman',...
          'FontWeight','bold','FontSize',14);
       %p0 = p0 + maxpos;
  end
  set(gca,'xlim',[f(1,1),f(nsnp,1)]);
  set(gca,'XTick', []);
  %set(gca,'XTickLabel',ch);
  set(gca,'TickDir','in');
  set(gca,'TickLength',[0.005,0.1]);
  set(gca,'FontName','Times New Roman', 'FontWeight','bold','FontSize',14);
  xlabel('Chromosome');ylabel('-log_{10}(\itP)');
  hold on;
  %add the signifigant line
  ylm=-log10(7.7e-06);yl=[ylm,ylm];
  ylm1=-log10(0.05/nsnp);yl1=[ylm1,ylm1];
  plot(get(gca,'xlim'),yl,'r:','LineWidth',1.5);
  plot(get(gca,'xlim'),yl1,'k:','LineWidth',1.5);
 text(xg(19),-log10(7.7e-06),num2str(7.7e-06))
 text(xg(19),-log10(0.05/nsnp),num2str(5.39E-07))
end
```

<div align="center"><img src="{{ "/images/Blog/GWAS/bmdman.jpg" | prepend: site.baseurl }}"></div>

# QQ plot

Here is the matlab code for BMD GWAS QQplot.
```matlab
load qq.mat
o = -log10(sort(plm,'ascend'));
alphaLevel=0.05;halflevel=0.5;oneMinusAlphalevel=1-alphaLevel;
x=1:1:length(o);
e = -log10( (x-0.5)./(length(o)))';
cl=unifrnd(0,1,24,3);
nclm=randperm(length(cl));
scatter(e,o,30,cl(nclm(1),:),'o','filled')
hold on
M=length(o);
mSeq=10.^(log10(0.5):0.1:(log10(M - 0.5)+0.1));
n=length(mSeq);n1=length(mSeq);alpha=ones(n,1);half=ones(n,1);oneMinusAlpha=ones(n,1);
if alphaLevel==alphaLevel
    for i=1:n
        alpha(i)=betainv(alphaLevel,mSeq(i),M-mSeq(i));
    end
end
if halflevel==halflevel
    for i=1:n
        half(i)=betainv(halflevel,mSeq(i),M-mSeq(i));
    end
end
if oneMinusAlphalevel==1-alphaLevel
    for i=1:n
        oneMinusAlpha(i)=betainv(1-alphaLevel,mSeq(i),M-mSeq(i));
    end
end
%alpha=[alpha half oneMinusAlpha];
betaDown=half-alpha;betaUp=oneMinusAlpha-half; 
theoreticalPval=(mSeq/M)';
lowerBar=-log10(theoreticalPval-betaDown);%lowerBar=real(lowerBar);
upperBar=-log10(theoreticalPval+betaUp);
yBar=-log10(theoreticalPval);
g=[0 0.5 0];
line(yBar,lowerBar,'Color',g,'LineStyle','-.','LineWidth',2.5)
line(yBar,upperBar,'Color',g,'LineStyle','-.','LineWidth',2.5)
line(e,e,'Color','k','LineStyle','-','LineWidth',2.5)
set(gca,'FontName','Times New Roman','FontWeight','bold','FontSize',16);
xlabel('Expected -log_{10}(\itP)','FontName','Times New Roman','FontWeight','bold','FontSize',16);
ylabel('Observed -log_{10}(\itP)','FontName','Times New Roman','FontWeight','bold','FontSize',16);
lg=legend('ISR','95% CI');
set(lg,'FontName','Times New Roman','FontWeight','bold','FontSize',12);
```

<div align="center"><img src="{{ "/images/Blog/GWAS/bmdqq.jpg" | prepend: site.baseurl }}"></div>



