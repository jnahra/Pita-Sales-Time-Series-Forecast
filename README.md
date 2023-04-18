# Predicting Pita Bread Sales at Family Bakery to Improve Orders Accuracy

![image-2.png](attachment:image-2.png)

### by John Nahra

# Overview

My grandfather started a bakery in downtown Cleveland with his brother and his cousin over 50 years ago. They built up the business to be very successful and a Cleveland staple. It is a source of family pride, appreciation for my Lebanese roots, and delicious Mediterranean food!

The business has now passed onto the sons, my dad and his cousins, and is continuing to thrive. Still, businesses always have room for improvement. In talking with my dad, he identified a project centered around inventory management as a useful enterprise. In particular, the inventory management of pita bread in the store front. As the grandson of one of Aladdin's founders and its first data scientist, I jumped at the opportunity to help my family in a real-world capstone project.

The large majority of the business is baking pita bread that is then distributed to grocery stores. However, we also sell pita bread out of the store front, both to retail and wholesale customers. The store manager places bread orders five times per week for fresh bread to be baked and sold at the store the next day (or two). In its current state without using data, orders are more feel-driven.

The impetus behind the project is to see if we can use data to better match orders to sales, thereby reducing the amount of bread that must be discounted as day old bread or discarded while at the same time ordering enough such that all who want delicious fresh pita bread are able to buy it.

There are several types of bread ordered, baked, and sold each day, but for the purposes of this project I focused only on one bread type: large plain pita bread.

Using daily data on store front transactions from January 2021 to March 2023, I was able to run a time series model to predict daily bread sales. I compared my sales predictions with the store front's bread orders over that same time frame and found that my predictions reduced the daily average order error by 25 and 33 packages of pita as compared with current orders on the train and test sets, respectively.

My 2023 sales forecast can be found in ['data/future_forecast.csv'](http://localhost:8888/edit/data/future_forecast.csv).

# Data Understanding

As mentioned above, I used daily data on store front transactions from January 2021 to March 2023. The data contained characteristics of each individual customer purchase: date, item, quantity, price, etc.

I filtered for large plain pita bread sales only. I split those sales into retail and wholesale categories and modeled each category separately.

Retail represents regular foot traffic. In the case of large plain pita, retail also represents customers who buy sandwiches, since large plain is used to make our shawarma wraps. Each package of pita contains five pieces of pita, thus five sandwiches is equivalent to one package of pita.

Wholesale represents some of our wholesale customers who walk into the store front to buy bread. Generally, customers wanting more than 3 trays of bread (18 packages per tray, so 54 packages of pita) need to order ahead of time. Thus, I assumed in my model that any sale over 54 packages of pita would be known ahead of time. Most of these customers are wholesale customers, but there were a few retail customers who bought a large amount of bread as well.

For a baseline comparison, I utilized daily data on the store front's bread orders from January 2021 to March 2023. This data contained order characteristics such as date, customer ID, bread type, quantity, sale cost, etc.

For my more complex time series model with additional regressors, I added variables for Cleveland Guardians day home games and Cleveland weather features.

Aladdin's Baking Company is only a short walk from Progressive Field, the home of Cleveland's MLB franchise, so I wanted to see if pita sales were affected on days where the Guardians had a home game during the day time (defined as a game starting before 7 pm). It serves to reason that there may be some effect when there is greater foot traffic downtown (at least for sandwiches), though it could also dissuade would-be non-game-going customers from making the trip due to increased traffic. I utilized data from Baseball Reference to put together the Guardians home schedule from 2021-2023 (including playoffs), filtered for day games, and used game attendance as the variable. More fans, more traffic.

I also wanted to see if Cleveland weather could provide a more accurate, granular sales forecast outside of general annual seasonality. I gathered daily weather data from the National Oceanic and Atmospheric Administration for Cleveland Hopkins Airport, which is about 15 minutes away from the bakery. I was able to get features such as precipitation and snowfall in inches as well as maximum temperature for each day.

# To be continued...

