# About

[An Overview of the Brazilian New Gas Market and the Electric Sector](https://medium.com/@lauramsfernandes/an-overview-of-the-brazilian-new-gas-market-and-the-electric-sector-b173f34ac307) it is a blog post made on Sep 9 2020, and has the objective to understand how is settle the Brazilian gas market nowadays and how the market opening can affect the Brazilian Energy Sector. It aims to answer the following questions:

1. How is the demand for Natural Gas in Brazil?
2. Reinjection: Reservoir Strategy or Lack of Structure?
3. How are sales structured by segment?
4. How can the New Gas Market impact the Energy Sector?

## Demand

At [wrangling file](1_naturalGas_Wrangling.ipynb) under the number `6` you can find the code thats load and set the MyDataFrame instantiated class about the Brazilian Natural Gas demand.

```
# Demand DataFrame
demand = MyDataFrame(balance.df.loc[:,['Import','Reinjection', 'Gas flaring', 'Own consumption¹', 'NGL²', 'Sales³', 'Adjustments and losses']])

# Setting unit, title and footer
demand.title = 'Brazilian Natural Gas Demand'
demand.unit = '10⁶ m³'
demand.footer = 'Sources: \nANP/SIM, as per Ordinance ANP No. 43/98, for imports data; ANP/SDP, as per Decree No. 2.705/98, for\nproduction, reinjection, gas flaring and losses data; Petrobras, for own consumption, NGL and sales data.\n\n¹ Refers to Petrobras own consumption in production areas, refineries, NGPP (Natural Gas Power Plant),\n transportation and storage. \n² Volume of gas absorbed in NGPPs. \n³ Sales to distributors, nitrofertilizers plants (Fafen) and electricity generation.'
```
At [plot file](2_naturalGas_Plots.ipynb) is the code regarding the demand plot.
```
demand.df.plot()
plt.xticks(np.arange(2010,2020,1))
plt.ylabel(demand.unit)
plt.title(demand.title)
plt.figtext(0.01,-0.3, balance.footer)
plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left', borderaxespad=0.);
plt.savefig('plots/demand.png',dpi=1200,bbox_inches='tight')
```
![Demand](plots\demand.png)

## Reinjection
## Sales
## Energy Sector

