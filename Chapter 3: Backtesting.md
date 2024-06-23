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
- Quantitative traders use a good variety of performance measures, though which set of numbers to use is often a personal preference, but with ease of comparisons across different strategies, the Sharpe ratio and drawdowns are likely to be the two most important
- Average annualized returns aka compound annual growth rate (CAGR): A measure of the mean annual growth rate of an investment over a specified period of time longer than one year
- Represents one of the most accurate ways to calculate and determine returns for anything that can rise or fall in value over time
- CAGR can be numerically represented as `CAGR = (Vf / Vi)^(1/n) - 1`
    - Vf is the final value of the investment
    - Vi is the initial value of the investment
    - n is the number of years
- An issue with CAGR when it comes to comparison is how the denominator is calculated
    - For example in a long-short strategy was one or both sides used as a denominator? If the equity or market value changes daily was a moving average used or just the value at the end of each day
- Using Sharpe ratio and drawdown as the standard performance measures avoids these comparison issues
- There is one subtlety that often confounds portfolio managers when they calculate Sharpe ratios: should we subtract the risk-free rate from the returns of a dollar-neutral portfolio?
    - The answer is no, a dollar-neutral portfolio is self-financing, meaning the cash you get from selling short pays for the purchase of the long securities, so the financing cost (due to the spread between credit and debit rates) is small and can be neglected for many backtesting purposes
    - Meanwhile, the margin balance that must be maintained earns a credit interest close to the risk-free rate
    - Margin balance: When you engage in short selling, you borrow shorts to sell them, with the hope of buying them back at a lower price, the proceeds from selling these borrowed shares are kept in a margin account
        - The margin account must maintain a certain minimum balance known as the marin requirement, to cover potential losses from the short positions
        - The margin balance is the cash/equivalent held in the account
    - Credit interest: Brokerages often pay interest on the balance in a margin account, this interest rate is close to the risk-free rate
    - Let's say the strategy return (portfolio return - contribution from the credit interest) is R, and the risk-free rate is Rf, the excess return used in calculating the Sharpe ratio is R + rf - rf = R, so essentially the risk-free rate can be ignored
- In general, only subtract the risk-free rate from your strategy returns if your strategy incurs financing costs
- To annualized Sharpe ratio would be sqrt(12) times the monthly Sharpe ratio
- To generalize the average and standard deviation based on a certain trading period T, you would have to first find out how many such trading periods there are in a year (Nt), then: `Annualized Sharpe Ratio = sqrt(Nt) * Sharpe Ratio Based on T`

### Calculating Sharpe Ratio
#### Using Excel
- This activity aims to calculate the Sharpe ratio of a long-only strategy for ICE from November 27, 2001 to November 14, 2007, assume the risk-free rate during this period is 4 percent per annum
1. Go to finance.yahoo.com and search for "IGE", select the "iShares North American Natural Resources ETF"
2. Click on "Historical Data" from the menu options
3. Set the date range to November 27, 2001 to November 14, 2007
4. Choose the frequency (daily) and click "apply" (if it is not applying check if you have an add blocker on)
5. Click on "Download" to get a CSV file
6. Open the CSV file in Excel
7. Select the whole file, go to data -> sort and select the "date" in the columns property, then sort by "oldest to newest"
8. Select the H3 cell and type "=(G3-G2)/G2", this is the daily return
    - The daily return is calculated as the closing price today subtracted by the closing price yesterday divided by the closing price yesterday it can be represented by: `Daily Return = (Today's Closing Price - Yesterday's Closing Price) / Yesterday's Closing Price)`
9. Double click the dot in the lower right corner to populate the entire column H
10. For clarity, type "Dailyret" in the header cell H1
11. In cell I3, type "=H3-0.04/252" which is the excess daily return, assuming a 4% annum risk-free rate and 252 trading days in a year
12. Double clock the dot in the lower right to populate the entire column and label I1 "Excess Dailyret"
    - The excess daily return is the daily return subtracted by the daily risk free rate, it represents the return of the investment above what could be earned from a risk-free asset, it can be represented as `Daily Return - Daily Risk-Free Rate` where `Daily Risk-Free Rate = Risk-Free Rate/Risk free period in which the rate is applied`
13. In the last row of the next column (I1506) type "=SQRT(252)*Average(I3:I1505)"
    - If there are 0's that give division by 0 errors, the function can be changed to "=SQRT(252) * AVERAGE(IF(ISNUMBER(I3:I1503), I3:I1503)) / STDEV(IF(ISNUMBER(I3:I1503), I3:I1503))," this will ensure that all parameters are numbers
14. The number displayed should be the Sharpe ratio of this buy-and-hold strategy

#### Using MATLAB
- For this section I will explain the MATLAB functions in detail, but as the code is outdates, for deprecated functions I will the deprecated and mention it's respective non-deprecated function.

#### Pre-Code Knowledge
- `clc`: Clear's out the terminal, but not the workspace
- `clea/clearvars`: Clear's out the workspace but not the terminal
- Deprecated: `xlsread(filename, xlrange)`:
    - Reads data from an excel spreadsheet from the file with filename with the range of xl range (e.g data = xlsread("IGE", "B1:C2"))
    - Assignment works in such a way that `data = xlsread(filename, xlrange)`, data will only contain the numerical data values, one can have up to three assignments with the syntax `[numericalData, textData, rawData] = xlsread(filename)`
    - The non-deprecated versions are `readtable`, `readmatrix`, and `readcell`, these functions also read excel files into their respective data types, though it is good to remember that readtable and readcell support mixed data, readmatrix is purely numerical
- Indexing: `x = y(row, col)`
    - This creates a matrix by indexing from another matrix
        - The indexing starts at 1, not 0
        - `end`: Represents the last index of the matrix
        - `:`: Colon operator, used to specify a range, `:` itself without anything selects all rows
    - Example: `tradeDays = txt(2:end, 1)`, this contains the trading days (omits the column name which is why it starts at 2, the date column is the first column which is why we take 1)
- Deprecated: `datenum(dateString, formatIn, pivotYear)`
    - This is not exactly deprecated, but MATLAB recommends using datetime()
    - This function converts date and time into a serial date number, dateString is the date to be converted
    - formatIn is the format of the input date, this must follow the date formatting symbols used by MATLAB(e.g "dd-mm-yyyy", "mm/dd/yyyy"), 
    - the pivotYear specifies the starting year in an 100 year range, with a pivot year of 1900, the two characters in the range 00-99 are interpreted as 1900-1999
    - A serial date number in MATLAB is a single number representation of a date by counting the number of days that have passed since a fixed base date, in MATLAB this date is January 0, 0000
    - The reason to convert to a serial date number is because it is kind of an "intermediate form", we are able to convert to this format, then convert to a different format
    - The non-deprecated function is `datetime` which displays the date in a more human-readable format
- `datestr(dateNumber, formatOut, pivotYear, options)`
    - dateNumber is the date to be converted, it can be a serial date number or a date vector (a vector of 6 elements representing [year, month, day, hour, minute, second])
    - formatOut is a string specifying the desired output of the string
    - options are name-value paired arguments that modify the behaviour, for example 'local' is a name that uses a specific time zone
- `cellstr(array/matrix)`:
    - Converts an array of strings to a cell array of character vectors
    - A cell-array in MATLAB is a data type that allows you to store arrays of different types and sizes, each element of a cell array is called a cell, and cells can be accessed with the curly braces {}
    - To convert the array from strings/characters to numerical values the array must either be a string array, character array, or a cell array of character vectors
- `str2double(array)`:
    - The input must be of type character vector, character array, cell array of character vectors, or string array
    - It outputs a double-precision numeric array, if the input cannot be converted to a number NaN is returned for those numbers
- `[x, sortIndex] = sort(array, order)`:
    - Returns a matrix as well as the sort index, the input is the array to be sorted and an order, the orders are "ascend" (default) and "descend"
    - The sortIndex is an array that represents the indexes of the rearrangements
    - This allows for other vectors to be ordered the exact same as the sortIndex, e.g closePrices = closePrices(sortIndex), the closePrices will be ordered the same as the original sort
- `./`: Performs element wise division that divides each element of one array by the corresponding index of another
- `mean`: Returns the mean of an array
- `std`: Returns the standard deviation of an array
- `isfinite(array)`: Returns a logical array of the same size where the elements of the input that are finite are true and false when they are not (inf, NaN)

#### My MATLAB Code Variation
This is what my code looks like (the code in the book does not work)
```matlab
    % make sure previously defined variables are erased.
    clear;

    % read a spreadsheet named "IGE.xls" into MATLAB.
    nums =xlsread("IGE"); % removes the text headers

    % format the dates
    tdates = nums(:, 1);
    tdates = datestr(tdates, 'yyyymmdd');
    tdates = str2double(cellstr(tdates));

    cls = nums(:, end);

    % sort the dates and closing prices
    [tdates, sortIndex] = sort(tdates, 'ascend');
    cls = cls(sortIndex);

    % calculating returns
    dailyret=(cls(2:end)-cls(1:end-1))./cls(1:end-1);
    excessRet=dailyret - 0.04/252;

    % removing invalid returns
    validExcessRet = excessRet(isfinite(excessRet));

    % sharpe ratio!
    sharpeRatio=sqrt(252)*mean(validExcessRet)/std(validExcessRet)
```

