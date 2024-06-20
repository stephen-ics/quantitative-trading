# Chapter 2: Fishing for Ideas

### Leverage
- Leverage allows traders to control a larger position with a smaller amount of capital 
- Position: The amount of a particular asset that a trader has invested in
- Regulation T: A regulation set by the Federal Reserve Board that governs the amount of credit brokerage firms and dealers can extend to invetors for the purchase of securities
- Trading futures, currencies, and options can allow for higher leverage than stocks
- While intraday positions allow a regulation T leverage of 4, interday (overnight) positions only allow a leverage of 2

### Types of Trades
- Directional Trades:
    - Long Trades: Buying an asset expecting its price to rise
    - Short Trades ("shorting a stock"): Selling an asset expecting its price to fall
- Dollar Neutral Trades:
    - Hedged Trades: Taking positions that offset potential losses in one asset with gains in another (e.g buying on stock and shorting another similar stock)
    - Pair Trades: A type of hedged trade where you take long and short positions in two related assets to profit from the relative performance
- Market Neutral Portfolios:
    - Aims to have a beta close to zero
    - Beta: A measure of a portfolio's volatility relative to the overall market, indicates how much the portfolio's returns are expected to move in relation to market returns
        - Beta = 1: The portfolio or security is expected to move in line with the market (if market goes up by 1%, portfolio goes up by 1% V.V)
        - Beta > 1: The portfolio or security is expected to be more volatile than the market (a beta of 1.5 means if the market goes up by 1%, the portfolio is expected to go up by 1.5%)
        - Beta < 1: The portfolio is expected to be less volatile than the market, a beta of 0.5 means if the market goes up by 1% the portfolio goes up by 0.5%
        - Beta = 0: The portfolio is expected to have no correlation with market movements

### How to determine Type of Trade
- Capital availability determines whether you should focus on directional trades (long/short only) or dollar-neutral trades (hedged/pair trades)
- A dollar neutral portfolio or a market neutral portfolio require twice the capital or leverage of a long or short only portfolio
- Though a hedged position is less risky than an unhedged position, the corresponding returns are smaller
- Below is a table of how capital availability affects trading choices:

| **Low Capital**                                      | **High Capital**                                   |
|------------------------------------------------------|----------------------------------------------------|
| Proprietary trading firm’s membership                | Retail brokerage account                           |
| Futures, currencies, options                         | Everything, including stocks                       |
| Intraday                                             | Both intra- and interday (overnight)               |
| Directional                                          | Directional or market neutral                      |
| Small stock universe for intraday trading            | Large stock universe for intraday trading          |
| Daily historical data with survivorship bias         | High-frequency historical data, survivorship bias–free |
| Low-coverage or delayed news source                  | High-coverage, real-time news source               |
| No historical news database                          | Survivorship bias–free historical news database    |
| No historical fundamental data on stocks             | Survivorship bias–free historical fundamental data on stocks |

### Futures
- Margin Requirement: The initial margin is the amount of capital required to open a futures position (not exclusive to futures)
    - The margin requirement must be maintained in the account to keep the position open, as soon as your losses approach your margin deposit, your broker will issue a margin call to demand a deposit of additional funds into your account
    - Failure to meet margin calls mean that your broker has the right to liquidate your position
- Nominal Value: The total value of the underlying asset controlled by a futures contract `Nominal Value = Contract Size * Current Market Price`
- Futures that have high nominal values and high volatility but low margin requirements still require large amounts of capital to maintain the margin requirements as a few losses may incur a margin call if your capital is insufficient

#### Sharpe Ratio
- The Sharpe Ratio is a measure used to assess the risk-adjusted return of an investment
- The Sharpe Ratio is calculated  by `Sharpe Ratio = (Rp - Rf) / σp`
    - Rp is the expected return rate of the portfolio
    - Rf is the risk-free rate of return
    - σp is the standard deviation of the portfolio's returns, representing total risk (volatility)
- Higher Sharpe Ratio: A more favourable risk-adjusted return (investment is providing a higher excess return per unit of risk)
- Lower Sharpe Ratio: A less favourable risk-adjustment return (investment is providing a lower excess return per unit of risk)
- Quantitative Interpretation:
    - Less than 1.0: Suboptimal
    - 1.0 to 1.99: Good
    - 2.0 to 2.99: Very good
    - 3.0 and above: Excellent (very rare)
- It has been mathematically proven that long-term growth is achieved by finding a strategy with the maximum Sharpe ratio



