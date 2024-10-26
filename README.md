# Implied_Volatility_and_Delta_Hedging
Forecasting a stock's volatility by calculating its implied volatility and creating a delta-neutral portfolio.

We'll calculate implied volatility for a point in the future using the Black-Scholes model to back-calculate the volatility(sigma) based on the market price of a put option. The portfolio is delta-neutral because price decreases are wholly offset by a complementary increase in the put options. We will also observe its option price sensitivities through the Greeks.

### Choosing a stock 

We will be forecasting Amazon's volatility (ticker: AMZN). We're bullish on AMZN since its price has increased by 10%, and growth at Amazon Web Services, or AWS, is accelerating due to generative AI integration. Sales have jumped, and profits in Q1 are impressive. Despite the layoffs and restructuring of the company, AMZN has shown remarkable returns, and its shares are still "undervalued" due to a mismatch between its valuation metric and growth expectations (EBITDA).

yfinance and yahoo_fin are two libraries we will use to get stock prices and option prices.

![stock_price](https://github.com/RutunjayRao/Implied_Volatility_and_Delta_Hedging/assets/89570687/82a3d12c-f9c9-49c4-a84e-83c8f8bda667)

### Distribution of returns

If we plot a histogram of returns, we can see that it does not necessarily follow a normal distribution, conflicting with Black-Scholes assumption of normally distributed returns. We will use a European Option pricing formula, assuming we receive the stock at expiration.

![distribution](https://github.com/RutunjayRao/Implied_Volatility_and_Delta_Hedging/assets/89570687/8cbbd296-9bec-4c7d-967c-d93a118544db)

### Calculating Option Premiums
As we'd expect, call premiums rise with increasing spot price while put premiums fall with increasing spot price. We have assumed a strike price (X) of $142. The current stock price (S0) is $140.57. 

![put_call_pricing](https://github.com/RutunjayRao/Implied_Volatility_and_Delta_Hedging/assets/89570687/c102e21e-d735-4154-91be-71b201f53de0)

### Volatility smile for Put option

A volatility smile is a common graph shape that results from plotting the strike price and implied volatility of a group of options with the same underlying asset and expiration date. The Black-Scholes model predicts that the implied volatility curve is flat when plotted against varying strike prices. Based on the model, the implied volatility would be the same for all options expiring on the same date with the same underlying asset, regardless of the strike price. Yet, in the real world, this is not the case.

![vol_smile](https://github.com/RutunjayRao/Implied_Volatility_and_Delta_Hedging/assets/89570687/b9b4f3f9-62f3-4894-bb2b-9f6197170490)

### Greeks

We'll calculate the Greeks delta, gamma, vega (not actually a Greek letter), theta, and rho, which are option premium sensitivities (partial derivatives) with respect to specific characteristics of the underlying asset:

-Delta: change in option price with $1 change in underlying asset price (velocity)
-Gamma: change in delta with $1 change in underlying asset price (acceleration)
-Vega: change in option price with 1% change in implied volatility
-Theta: change in option price with 1 day change in expiration (time decay)
-Rho: change in option price with 1% change in interest rate

For our put option, we can see how Delta varies with changes in time to expiry:

![delta_variation](https://github.com/RutunjayRao/Implied_Volatility_and_Delta_Hedging/assets/89570687/320a3033-13c0-4394-8262-615571479759)

### Delta Hedging

We will then finally see that for a delta-neutral portfolio, assuming we have 100 shares, we would be required to buy "2" put options.
Option contract value to delta hedge AMZN comes out to be $1371.
We will also see that with a $1 decrease in the stock price, value changes very negligibly.
