# About

[An Overview of the Brazilian New Gas Market and the Electric Sector](https://medium.com/@lauramsfernandes/an-overview-of-the-brazilian-new-gas-market-and-the-electric-sector-b173f34ac307) it is a blog post made on Sep 9 2020, and has the objective to understand how is settle the Brazilian gas market nowadays and how the market opening can affect the Brazilian Energy Sector. It aims to answer the following questions:

1. How is the demand for Natural Gas in Brazil?
2. Reinjection: Reservoir Strategy or Lack of Structure?
3. How are sales structured by segment?
4. How can the New Gas Market impact the Energy Sector?

## Plots

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
The data was scrapped from a govern report [Monthly Industry Follow-up Natural Gas Bulletin](http://www.mme.gov.br/documents/36216/1119340/06+-+Boletim+Mensal+de+Acompanhamento+da+Ind%C3%BAstria+de+G%C3%A1s+Natural+Junho+2020/4ecd27ca-bd64-bfa7-3510-03799045f87f).

```
# Dict with values scrapp from MME Relatory
sales_segment_ = {'Industrial¹' : [43.61, 40.82, 40.77, 39.75, 36.97, 36.34, 37.17, 35.70, 28.16, 31.22, 34.61, 33.87],
                  'Automotive' : [4.82, 4.96, 5.40, 6.06, 6.26, 5.87, 6.29, 4.83, 3.36, 3.63, 4.34, 4.72],
                  'Residencial' : [0.97, 1.11, 1.18, 1.26, 1.27, 1.00, 1.14, 1.30, 1.38, 1.49, 1.64, 1.33],
                  'Comercial' : [0.79, 0.83, 0.78, 0.84, 0.91, 0.86, 0.87, 0.84, 0.51, 0.32, 0.46, 0.64],
                  'Electric Generation' : [45.90, 29.59, 34.25, 27.69, 29.03, 40.46, 25.63, 19.52, 17.26, 15.70, 18.12, 22.78],
                  'Cogenaration' : [2.50, 2.37, 2.65, 2.84, 2.65, 2.30, 2.12, 2.26, 2.22, 1.65, 2.07, 2.10],
                  'Others (including GNC)' : [0.04, 0.58, 0.53, 0.40, 0.83, 0.42, 0.35, 0.36, 1.22, 0.76, 0.65, 0.63]}

# Creating DataFrame
sales_segment_ = pd.DataFrame(data=sales_segment_)

# Setting Index
sales_segment_.index = [2015,2016,2017,2018,2019,1,2,3,4,5,6,2020]

# Creating DataFrame for Covid Period
sales_seg_covid_ = sales_segment_.loc[[1,2,3,4,5,6]].copy()

# Setting Index to string
sales_seg_covid_.index = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun']

# Dropping Covid Period from Segment DataFrame
sales_segment_.drop([1,2,3,4,5,6,2020], inplace=True)
```

```
# Turning Sales Period DataFrame into MyDataFrame
sales_segment = MyDataFrame(sales_segment_)

# Setting unit, title and footer
sales_segment.unit = '10⁶ m³/day'
sales_segment.title = 'Brazilian Sales of Natural Gas by Segment'
sales_segment.footer = 'Source:\nMME, Monthly Industry Follow-up Bulletin of Natural Gas - June 2020\n\n¹ Includes consumption by refineries, fertilizer factories and use of gas as raw material.'
```
After that it was calculated the segment proportion.
```
sales_per = sales_segment.df.copy()

# Calculation proportion
years=np.arange(2015,2020,1)
for i, year in enumerate(years):
    sales_per.loc[year] = sales_segment.df.iloc[i,:].div(sales_segment.df.iloc[i,:].sum())

# Converting into MyDataFrame
sales_per = MyDataFrame(sales_per)

# Setting unit, title and footer
sales_per.unit = '%'
sales_per.title = 'Brazilian Sales of Natural Gas by Segment'
sales_per.footer = 'Source:\nMME, Monthly Industry Follow-up Bulletin of Natural Gas - June 2020\n\n¹ Includes consumption by refineries, fertilizer factories and use of gas as raw material.'
```
![Sales per Segment](./plots/sales_per.png)
## Energy Sector
