# Brazilian Market Gas Repository

Brazilian Government is working to open its Natural Gas Market to third-parties and changing some laws regarding the fuel.

**This repository aims to collect data about Natural Gas in Brazil and build, in the future, a dashboard with all information gathered.**

## Business Understanding

### Context

Nowadays the Brazilian Natural production and transportation is controlled by Petrobras, a state-owed multinational corporation in the petroleum industry, ranked as the 120th largest company in the world by revenue¹. The company has 6 business areas² (in order of revenue):

> * `Refining, Transportation and Marketing`
> * `Exploration and Production`
> * `Distribution`
> * `Gas and Power`
> * `International`
> * `Biofuels`

#### Gas and Power

The main core of it is deal with the transportation and trading of natural gas and LNG, and generation and trading of electric power, and the fertilizer business.

Its important to mention that Petrobras also controls the distribution of oil products, ethanol, biodiesel and natural gas to wholesalers and through the Petrobras Distribuidora S.A. retail network in Brazil

#### Termination Commitment Term

The Administrative Council for Economic Defense (Portuguese: Conselho Administrativo de Defesa Econômica - CADE) and Petrobras signed a Termination Commitment Term³ due to investigations regarding alleged anti-competitive conduct by Petrobras in the Brazilian Natural Gas Market, including abuse of a dominant position and discrimination against competitors through differentiated pricing.

Through the agreement, the state company has committed to sell assets related to the natural gas market. The measure aims to prevent the future occurrence of the same facts investigated by Cade, in addition to stimulating competition in the sector, so far exploited almost entirely by Petrobras, through the entry of new agents that would attract national and international investments at various levels of the chain productive.

#### Gas to Grow Program

In September 2020, the Brazilian Chamber of Representatives approved the bill 6407/2013. Known as the “New Gas Law”, it is part of the Gas to Grow⁴ program (Gás para Crescer) and establishes the new legal framework for the Brazilian Natural Gas market.

The program aims to boost the market, facilitating the operation of private companies in the gas sector. The main changes proposed are:

> * Ensure non-discriminatory third-party access (TPA) for essential facilities (e.g., upstream pipelines, gas processing plants, and liquefied natural gas terminals);
> * Replace the point-to-point contracts by an entry-exit system with liquid virtual trading points;
> * Guarantee an independent transmission system;
> * Change the auction regime for new pipelines and expansion from concession to authorization or permit, reducing the process of creating new networks;
> * Harmonize the state and federal regulation regarding Natural Gas.

Source:

1. [Petrobras Company Profile](https://fortune.com/company/petrobras/global500/). Fortune - Global 500, 10/08/2020.

2. [Wikipedia](https://en.wikipedia.org/wiki/Petrobras)

3. Assessoria de Comunicação Social. [Cade e Petrobras celebram acordo para venda de ativos no mercado de gás natural](http://www.cade.gov.br/noticias/cade-e-petrobras-celebram-acordo-para-venda-de-ativos-no-mercado-de-gas-natural). CADE, 08/07/2019.

4. [Programa Gás Para Crescer](http://www.mme.gov.br/web/guest/secretarias/petroleo-gas-natural-e-biocombustiveis/acoes-e-programas/programas/gas-para-crescer). Secretaria de Petróleo, Gás e Energia, Ministério de Minas e Energia, 24/06/2016.

## About the data

The data were collected from:

* [Petroleum National Agency Statistical Yearbook 2020](http://www.anp.gov.br/publicacoes/anuario-estatistico/anuario-estatistico-2020), ANP *(Portuguese: Agência Nacional de Petróleo)*, consolidates data on the performance of the Brazilian oil, natural gas and biofuels industry and the national supply system in 2010-2019;

* [ANEEL](https://www.aneel.gov.br/dados/geracao) (Portuguese: Agência Nacional de Energia Elétrica) Generation by Source:
History of the volume of electricity produced in the country in GWh, expressed by the values of energy load dispatched in the National Interconnected System - SIN, classified by renewable sources or not and the volume produced by generators not yet interconnected.

* [The World Bank](https://data.worldbank.org/country/brazil)

* [Ministério de Minas e Energia](http://www.mme.gov.br/documents/36216/1119340/06+-+Boletim+Mensal+de+Acompanhamento+da+Ind%C3%BAstria+de+G%C3%A1s+Natural+Junho+2020/4ecd27ca-bd64-bfa7-3510-03799045f87f) Demand by Segment: Monthly Industry Follow-up Bulletin of Natural Gas.

* [NASA Giovanni](https://giovanni.gsfc.nasa.gov/giovanni/) Precipitation Data. Instructions after log in on the website:

> 1. `Select Plot`: Time Series, Seasonal
> 2. `Select Seasonal Dates`: Select all months, years 2010 to 2018
> 3. `Select Region`: Countries Brazil;
> 4. `Keyword`: Precipitation
> 5. `Variable`: Preciptation Rate (TRMM_#B43 v7)
> 6. `Units`: mm/month
> After making the selection above, click on `Plot Data`
* [EIA](https://www.eia.gov/environment/emissions/co2_vol_mass.php) Carbon Dioxide Emissions Coefficients

## Files

* 1_naturalGas_Wrangling.ypynb File
  
> Wrangles and load all data used in this repository.

* 2_naturalGas_Plots.ipynb File

> Concentrates all plots made from the collected data.

* 3_naturalGas_ML.ipynb File

> Concetrates all machile learning code used in this repository.

## Folders

* dashboard

> Contains all files provenients of the dashboard

* data_set

> Contains all data used in this repository.

* plots

> Destiny folder to all plots saved in `2_naturalGas_Plot` file.