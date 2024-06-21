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