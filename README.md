## Problem statement

This project aims to build a web application that gives users access to predicting Bitcoin price in a specific time period, more specifically, seven days from the current date. Considering confidence intervals, three predicted values are generated for the chosen date. In this case, users can compare the predicted price, the interactive graph of historical bitcoin price, and their buying price (if possible) to make trading decisions. 

## Structure of the Django Project

<p align="center">
  <img width="350" src="https://github.com/fangyiyu/Bitcoin/blob/master/structure.png">
</p>

- One Django model (User) is built. It lets users register, login, and log out together with storing the corresponding information. 
- In plots.py, two functions are defined, including data() which fetches real-life time-series data from the [Binance API](https://python-binance.readthedocs.io/en/latest/) and performs preprocessing; grah() which plots an interactive graph of the historical price of Bitcoin using [Plotly](https://plotly.com/python/getting-started/), as shown below.

<p align="center">
  <img width="800" src="https://github.com/fangyiyu/Bitcoin/blob/master/graph.png">
</p>
 
- After a user logged in, she will see her name in the up left of the main page (index.html) and a form to let her choose a date to predict, the date range is limited to seven days from "today" because of the parameter setting in the Machine learning model, so any date beyond the setting will be disabled (not clickable). After clicking the predict button, the page needs a while to load since the ML model needs time to converge. A preloader screen is set on clicking the predict button for a better user experience. After the convergence of the Machine Learning model on the backend, the user will be able to click on the default, best and worst button to see the predicted price of bitcoin on the specific date the user chose in three different scenarios: the most likely scenario, the best and the worst scenarios. These three values correspond to the yhat, yhat_upper, and yhat_lower values in the result of the Prophet Model (explained below). Users will be able to see the explanations of these three buttons by hovering on them. 

<p align="center">
  <img width="800" src="https://github.com/fangyiyu/Bitcoin/blob/master/home_page.png">
</p>

- In views.py, a Graph view is created to pass the graph generated by Plotly to index.html; a predict view is built which uses [Prophet](https://facebook.github.io/prophet/) from Facebook for the machine learning forecasting task in the backend. As an MSc. student with a research interest in machine learning, I have experimented with different time series prediction models, including LSTM, ARIMA, and Prophet. Prophet turned out to be more accurate by just utilizing time and historical price data as input. Hence the proposed model here is Prophet. Furthermore, Index, logout_view, login_view, and register views are created for user authentication. 

## Run the application


## Deployment
The application has been deployed to [Heroku](https://devcenter.heroku.com/categories/python-support), and a live demo can be seen here: 
