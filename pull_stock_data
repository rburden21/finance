import pandas as pd
import yfinance as yf
import matplotlib.pyplot as plt

data = yf.download(['QQQ','AAPL','AMZN'], start = '2020-01-01', end = '2022-07-31')

print(data.head(5))

closes = data['Adj Close']
benchmark_returns = closes.QQQ.pct_change()

#construct simple portfolio
appl_position = closes.AAPL * 50
amzn_position = closes.AMZN * 50

#compute portfolio value over time
portfolio_value = appl_position + amzn_position

#compute portfolio daily pnl
portfolio_pnl = (
                    (appl_position - appl_position.shift())
                    + (amzn_position - amzn_position.shift())
                )
            
#compute portfolio daily return
portfolio_returns = (portfolio_pnl / portfolio_value)
portfolio_returns.name = 'Port'

#prepare data for plotting
portfolio_cumulative_returns = (portfolio_returns.fillna(0.0)+1).cumprod()
benchmark_cumulative_returns = (benchmark_returns.fillna(0.0)+1).cumprod()

#plot cumulative portfolio v benchmark returns
pd.concat(
            [
                portfolio_cumulative_returns,
                benchmark_cumulative_returns
            ],
            axis=1
        ).plot()

plt.show()