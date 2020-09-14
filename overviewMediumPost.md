# About

[An Overview of the Brazilian New Gas Market and the Electric Sector](https://medium.com/@lauramsfernandes/an-overview-of-the-brazilian-new-gas-market-and-the-electric-sector-b173f34ac307) it is a blog post made on Sep 9 2020, and has the objective to understand how is settle the Brazilian gas market nowadays and how the market opening can affect the Brazilian Energy Sector. It aims to answer the following questions:

1. How is the demand for Natural Gas in Brazil?
2. Reinjection: Reservoir Strategy or Lack of Structure?
3. How are sales structured by segment?
4. How can the New Gas Market impact the Energy Sector?

## plots

All plots code can be found on [plot file](2_naturalGas_Plots.ipynb).

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
```
demand.df.plot()
plt.xticks(np.arange(2010,2020,1))
plt.ylabel(demand.unit)
plt.title(demand.title)
plt.figtext(0.01,-0.3, balance.footer)
plt.legend(bbox_to_anchor=(1.05, 1), loc='upper left', borderaxespad=0.);
plt.savefig('plots/demand.png',dpi=1200,bbox_inches='tight')
```
![Demand](./plots/demand.png)

## Reinjection

It is import to mention the reinjection question to clarify some miscomprehension about the subject that can lead to wrong assumptions about the natural gas demand. Some industry consultants with economy background may think that reinjection is a natural gas waste. However is a reservoir technique to maintain its internal pressure.

A correlation graph using the `balance` dataframe was plot to prove that reinjection has no relation with any waste metric. For example, if the reinjection had any correlation with gas flaring, it would indicates that reinjection were being made in the same period of time that offshore plataforms was burning gas to relieve the production.
```
corr = balance.df.corr()
ax = sns.heatmap(
    corr,
    vmin=-1, vmax=1, center=0,
    #sns.palplot(sns.diverging_palette(145, 280, s=85, l=25, n=7))
    cmap=sns.diverging_palette(145, 280, n=200),
    square=True
)
ax.set_xticklabels(
    ax.get_xticklabels(),
    rotation=45,
    horizontalalignment='right'
);

plt.title('Balance Correlation')
plt.savefig('plots/corr.png',dpi=600,bbox_inches='tight')
```
![Correlation](./plots/corr.png)
## Sales
## Energy Sector
