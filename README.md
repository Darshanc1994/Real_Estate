import pandas
real_estate = pandas.read_csv("real_estate_sales.csv")
print(real_estate)
import numpy
from datetime import datetime
real_estate.date = pandas.to_datetime(real_estate.SaleDate)
real_estate['quarter'] = pandas.PeriodIndex(real_estate.date, freq = 'Q')
print(real_estate['quarter'])
total_sales_per_quarter = real_estate.groupby('quarter')['SalePrice'].sum()
print(total_sales_per_quarter)
real_estate['LandSF'] = real_estate['LandSF'].replace(0, numpy.nan)
real_estate['price_per_sf'] = real_estate['SalePrice']/real_estate['LandSF']
average_price_per_sf = real_estate['price_per_sf'].mean()
print(average_price_per_sf)
real_estate['month'] = pandas.PeriodIndex(real_estate.date, freq = 'M')
print(real_estate['month'])
Max_Sale_Month = real_estate.groupby('month')['SalePrice'].max()
print(Max_Sale_Month)
real_estate.to_csv('real_estate.csv', index=False)
