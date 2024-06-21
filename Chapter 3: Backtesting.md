# Chapter 3: Backtesting
### Common Backtesting Platforms
#### Excel
- This is the most basic and common tool for traders, whether retail or institutional
- You can enhance its power further if you can write Visual Basic macros
- The beauty of Excel is "What you see or what you get" (or WSYIWYG in computing terminology)
- Data and program are also all in one place so that nothing is hidden
- A common backtesting pitfall called the "look-ahead bias" is unlikely to occur in Excel (unless you use macros, which renders it no longer WSYIWYG)
- Another advantage of Excel is that often backtesting and live trade generation can be done from the same spreadsheet, eliminating any duplication or programming efforts
- The major disadvantage of Excel is that it can be used to backtest only fairly simple models, but simple models are often the best!

#### MATLAB
- MATLAB is one of the most common backtesting platforms used by quantitative analysts and traders in large institutions
- It is ideal for testing strategies that involve a large portfolio of stocks
- It has numerous advanced statistical and mathematical modules built in, so trades do not have to reinvent the wheel if their trading algorithms involve some sophisticated but common mathematical concepts
- There's also a large number of third party freeware available for download from the internet useful for quantitative trading purposes
- Finally MATLAB is very useful in retrieving web pages with financial information and parsing it (web scraping)
- MATLAB is very useful for backtesting but clumsy for execution, you may need to build a separate execution system once the strategy has been backtested


#### TradeStation
- TradeStation is familiar to many retail traders as a brokerage that provides all-in-one backtesting and trade execution platforms linked to the brokerage's servers
- The main advantage of this setup are
    - Most of the historical data necessary for backtesting is readily available, whereas you have to download the data from somewhere else if you use Excel or MatLab
    - Once you have backtested the program you can immediately generate orders using the same program and transmit them to the brokerage
- The disadvantages of this approach is that you are tied to TradeStation as your broker, and the proprietary language used by TradeStation is not as flexible as MATLAB and does not include some of the more advanced statistical and mathematical functions some traders use

#### High-End Backtesting Platforms
- In case you do have the financial resources to purchase a high-end institutional-grade backtesting platform, here is a partial list:
    - FactSet's Alpha Testing
    - Clarifi's ModelStation
    - Quantitative Analytics' MarketQA
    - Barra's Aegist System
    - Logical Information Machines
    - Alphacet's Discovery

#### Finding and Using Historical Databases
- If you have a strategy in mind that requires a specific type of historical data, the first thing to do is to Google that type of data
- You will be surprised how many free/low-cost historical databases are out there
- The following table contains historical databases for backtracking

#### Daily Stock Data

| Source            | Pros                                                                  | Cons                                                   |
|-------------------|-----------------------------------------------------------------------|--------------------------------------------------------|
| Finance.yahoo.com | Free. Split/dividend adjusted.                                        | Has survivorship bias. Can download only one symbol at a time. |
| HQuotes.com       | Low cost. Same data as finance.yahoo.com. Software enables download of multiple symbols. | Has survivorship bias. Split but not dividend adjusted. |
| CSIdata.com       | Low cost. Source of Yahoo! and Google’s historical data. Software enables download of multiple symbols. | Has survivorship bias.                                 |
| TrackData.com     | Low cost. Split/dividend adjusted. Software enables download of multiple symbols. Fundamental data available. | Has survivorship bias.                                 |
| CRSP.com          | Survivorship bias free.                                               | Expensive. Updated only once a month.                  |

#### Daily Futures Data

| Source            | Pros                                                                  | Cons                                                   |
|-------------------|-----------------------------------------------------------------------|--------------------------------------------------------|
| Quotes-plus.com   | Low cost. Software enables download of multiple symbols.              |                                                        |
| CSIdata.com       | See above.                                                            |                                                        |

#### Daily Forex Data

| Source            | Pros                                                                  | Cons                                                   |
|-------------------|-----------------------------------------------------------------------|--------------------------------------------------------|
| Oanda.com         | Free.                                                                 |                                                        |

#### Intraday Stock Data

| Source            | Pros                                                                  | Cons                                                   |
|-------------------|-----------------------------------------------------------------------|--------------------------------------------------------|
| HQuotes.com       | See above.                                                            | Short history for intraday data.                       |

#### Intraday Futures Data

| Source            | Pros                                                                  | Cons                                                   |
|-------------------|-----------------------------------------------------------------------|--------------------------------------------------------|
| DTN.com           | Bid-ask data history available as part of NxCore product.             | Expensive: requires subscription to live datafeed.     |

#### Intraday Forex Data

| Source            | Pros                                                                  | Cons                                                   |
|-------------------|-----------------------------------------------------------------------|--------------------------------------------------------|
| GainCapital.com   | Free. Long history.                                                   |                                                        |

#### Are the Data Split and Dividend Adjusted
- When a company had its stock split N to 1 (N is usually 2, but can be a fraction like 0.5 as well)
- Stock Split: When a company increases the number of its outstanding shares to lower the price per share, for example in a 2-for-1 split, each shareholder receives an additional share for every share they own, and the price of each share is halved
- Reverse Split: This is the opposite, where the number of outstanding shares is reduced, increasing the price per share, in a 1-for-2 reverse split, each shareholder gets one share for every two shares they own, and the price of each share is doubled
    - Adjustment Calculation: If a stock split happens with a ratio of N to 1, the ex-date (the date the stock split takes effect) is T, all prices before T need to be multiplied by 1/N, this adjustment ensures that the historical price reflects the current share structure
- Dividend: A payment made by a company to its shareholders, usually as a distribution of profits (typically causes a drop on the ex-date)
    - Adjustment Calculation: If a company issues a divided of $d per share with an ex-date of T, all prices before T need to be adjusted by a multiplier calculated as: `Multiplier = (Close(T - 1) - d) / Close(T - 1)`
    - Close(T - 1) is the closing price of the trading day before the ex-date, this adjustment keeps the historical daily returns consistent pre- and post-adjustment
    - Ex-date (Ex-dividend date): The date on which a stock starts trading without the value of its next dividend payment, for stock splits it's the date the split takes effect
- This is the method Yahoo Finance adjusts its historical data, and is the most common way
- It is best to find historical data that is already split and dividend adjusted

#### Are the Data Survivorship Bias Free?
- Unfortunately, databases free from survivorship bias are quite expensive and may not be affordable for a start-up business
- One way to overcome this problem is to start collecting point-in-time data yourself for the benefit of your future backtest
- If you save the prices each day of all the stocks in your universe to a file, you will have a point-in-time or survivorship-bias-free database to use in the future
- Another way to lessen the impact of survivorship bias is to backtest your strategy on more recent data so that the results are not distorted by too many missing stocks

#### Does Your Strategy Use High and Low Data?
- For almost all daily stock data, the high and low prices are far noisier than the open and close prices
- What this means is that even when you had placed a buy limit order below the recorded high of a day, it might not have been filled, and vice versa for a sell limit order
- This could be due to the fact that a very small order was transacted at the high, or the execution could have occurred on a market to which your order was not routed
- Sometimes, the high or low is simply due to an incorrectly reported tick that was not filtered out
- Hence, a backtest that relies on high and low data is less reliable than ones that rely on open and close data
- Sometimes even a market on open (MOO) or market on close (MOC) order might not be filled at the historical open and close prices shown in your data
- This is due to the fact that the historical prices shown may be due to the primary exchange, or it may be a composite price including all the regional exchanges
- Depending on where your order was routed, it m ay be filled at a difference price from the historical opening and closing price shown in your dataset
- Typically an extreme return, say 4 standard deviations away from the average should be accompanied by a news announcement, or should occur on a day when the market index also experienced extreme returns, if not then the data is suspect

#### Performance Measurement
