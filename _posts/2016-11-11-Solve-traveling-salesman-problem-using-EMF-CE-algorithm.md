---
layout: post
comments: true
enable_mathjax: true
output: html_document
tags: [Contraction-Expansion algorithm (CE), Exchange-Move-Flip (EMF), Combinatorial Optimization,traveling salesman problem (TSP)]
---

<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.4/latest.js?config=TeX-MML-AM_CHTML">
</script>

## Traveling salesman problem (TSP)

The traveling salesman problem (TSP) is well known the classical and fundamental NP-hard combinatorial optimization problems. The classical TSP that can be described as following: find a path through a weighted graph that starts and ends at the same city, includes every other city exactly once, and minimizes the total distance tour of n cities. [MORE ABOUT](https://en.wikipedia.org/wiki/Travelling_salesman_problem)

## TSPs Instance

> Art TSPs

| [![da Vinci's Mona Lisa](http://www.math.uwaterloo.ca/tsp/data/ml/mona-lisa100K.gif)](http://www.math.uwaterloo.ca/tsp/data/ml/mona-lisa100K.gif) | [![van Gogh's Self Portrait 1889](http://www.math.uwaterloo.ca/tsp/data/art/vangogh120K.gif)](http://www.math.uwaterloo.ca/tsp/data/art/vangogh120K.gif) | [![Botticelli's The Birth of Venus](http://www.math.uwaterloo.ca/tsp/data/art/venus140K.gif)](http://www.math.uwaterloo.ca/tsp/data/art/venus140K.gif) |
| :-----------------------------------------------------------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------: |
|                                  [mona-lisa100K.tsp](http://www.math.uwaterloo.ca/tsp/data/ml/mona-lisa100K.tsp)                                  |                                       [vangogh120.tsp](http://www.math.uwaterloo.ca/tsp/data/art/vangogh120K.tsp)                                        |                                        [venus140K.tsp](http://www.math.uwaterloo.ca/tsp/data/art/venus140K.tsp)                                        |

| [![Velazquez's Juan de Pareja](http://www.math.uwaterloo.ca/tsp/data/art/pareja160K.png)](http://www.math.uwaterloo.ca/tsp/data/art/pareja160K.png) | [![Courbet's The Desperate Man](http://www.math.uwaterloo.ca/tsp/data/art/courbet180K.png)](http://www.math.uwaterloo.ca/tsp/data/art/courbet180K.png) | [![Vermeer's Girl with a Pearl Earring](http://www.math.uwaterloo.ca/tsp/data/art/earring200K.gif)](http://www.math.uwaterloo.ca/tsp/data/art/earring200K.gif) |
| :-------------------------------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|                                      [pareja160K.tsp](http://www.math.uwaterloo.ca/tsp/data/art/venus140K.tsp)                                      |                                      [courbet180K.tsp](http://www.math.uwaterloo.ca/tsp/data/art/courbet180K.tsp)                                      |                                          [earring200K.tsp](http://www.math.uwaterloo.ca/tsp/data/art/earring200K.tsp)                                          |

> National TSPs

| [![China - 71,009 Cities](/images/Blog/TSP/national/chpoints.gif)](/images/Blog/TSP/national/chpoints.gif) | [![Egypt - 7,146 Cities](/images/Blog/TSP/national/egpoints.gif)](/images/Blog/TSP/national/egpoints.gif) | [![Greece - 9,882 Cities](/images/Blog/TSP/national/grpoints.gif)](/images/Blog/TSP/national/grpoints.gif) |
| :--------------------------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------: | :--------------------------------------------------------------------------------------------------------: |
|                [China - 71,009 Cities](http://www.math.uwaterloo.ca/tsp/world/ch71009.tsp)                 |                 [Egypt - 7,146 Cities](http://www.math.uwaterloo.ca/tsp/world/eg7146.tsp)                 |                 [Greece - 9,882 Cities](http://www.math.uwaterloo.ca/tsp/world/gr9882.tsp)                 |

### The best known results for the TSP Art instances are given in the table below. I would be happy to post any improvements you find!

<div align="center"><img src="{{ "/images/Blog/TSP/TSPbestartTSP.png" | prepend: site.baseurl }}"></div>

## EMF-CE algorithm

Here, I will introdutes a novel search algorithm that based on Contraction-Expansion algorithm and integrated three operators Exchange, Move and Flip (EMF-CE) is proposed for the traveling salesman problem (TSP). EMF-CE uses a negative exponent function to generate critical value as the feedback regulation of algorithm implementation. Also, combined Exchange Step, Move step with Flip step and constitute of more than twenty combinatorial optimization of program elements. It has been shown that the integration of local search operators can significantly improve the performance of EMF-CE for TSPs. We test small and medium scale (51-1000 cities) TSPs were taken from the TSPLIB online library. The experimental results show the efficiency of the proposed EMF-CE for addressing TSPs in comparison with other state-of-the-art algorithms.

## METHODOLOGIES FOR SOLVING TSPs
