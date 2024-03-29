---
permalink: /SafeCross/
title: "SafeCross: Open source application for predictive modelling of cyclist crossing success on tram tracks"
---

<p align="center">
  <img src="/assets/images/SafeCross/SafeCross_AUTO.gif" width="900">
</p>

## Introduction

SafeCross is an open-source framework for proactively assessing risk for single bicycle crashes at locations where cyclists interact with tram tracks. 

Cyclist detection and tracking is automatically performed using advanced computer vision and deep learning techniques. The trajectories are then automatically processed to calculate the angles at which the cyclists crossed the tracks. These are then fed into a risk model for predicting the probability of crossing success. Risk estimates are then compiled to predict the number of unsuccessful crossings that may occur over time, and to generate a risk heatmap which highlights risky sections of the tracks.

The tool is a standalone Windows application, and was designed with ease-of-use in mind. It can be run using a standard CPU, without the need for a cuda-enabled GPU, or any coding/manual data processing.


<p align="center">
  <img src="/assets/images/SafeCross/SafeCross_pipeline.png" width="900">
</p>

## Tools


| Step                  | Description                                                  | Tools                                     | Manuals                                  |
|-----------------------|--------------------------------------------------------------|-------------------------------------------|------------------------------------------|
| T-calibration               |                        | [Tool](https://bitbucket.org/TrafficAndRoads/tanalyst/downloads/){:target="_blank"} | TBD |
| SafeCross TA               |                        | [Tool](https://github.com/KevGildea/SafeCross/tree/main/SafeCross%20TA){:target="_blank"} | TBD |
| SafeCross AUTO             |                        | [Tool](https://github.com/KevGildea/SafeCross/tree/main/SafeCross%20AUTO){:target="_blank"} | TBD |
| SafeCross SMoS             |                        | [Tool](https://github.com/KevGildea/SafeCross/tree/main/SafeCross%20SMoS){:target="_blank"} | TBD |


## Example application in Dublin, Ireland
<p align="center">
  <img src="/assets/images/SafeCross/SafeCross_Dublin.jpg" width="900">
</p>


## Conference presentations
- <a href="https://cyclingsafety.net/" target="_blank">International Cycling Safety Conference (ICSC 2022)</a>
- <a href="http://www.cyclingandsociety.org/" target="_blank">Cycling & Society Annual Symposium (2023)</a>

## Cite our methods paper
If you find SafeCross useful in your research, please consider citing our work:

<small>
Gildea, K., Hall, D., Mercadal-Baudart, C., Caulfield, B., & Simms, C. (2023). Computer vision-based assessment of cyclist-tram track interactions for predictive modeling of crossing success. *Journal of Safety Research*. <a href="https://doi.org/10.1016/J.JSR.2023.09.017" target="_blank">10.1016/J.JSR.2023.09.017</a>
</small>
  
<a href="/assets/images/SafeCross/SafeCross_Citation.bib" download>Download citation (.bib)</a>
