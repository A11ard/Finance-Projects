# Options

**Overview:** This project uses the Black-Scholes-Merton Model  for pricing options, finding Greeks, finding implied volatility, and accommodating dividends. It's primary purpose is to model a stock's movement based off of geometric brownian motion and observe how different options' change over a given period.

[Skip to Results](#findings-and-discussion)

## Cloning

```bash
git clone https://github.com/A11ard/Finance-Projects.git
cd Finance-Projects/options/
```

## Usage

Stock.py contains the stock class. The main focus of this class is the 'frame' instance attribute. Think of this as a spreadsheet where each row is a day further into the future. The annualized historical volatility is calculated and recorded in the 'annual_vola' column. The price of the stock is modelled with the assumption that a stock's log returns are normally distributed around a certain mean return (mu) and a standard deviation of returns (sd).

Option.py contains the bsm class. This can be used multiple ways. The BSM model works like this:
```
 Price = BSM(X, U, R, V, T, D)
```
With the inputs listed respectively: exercise price, underlying stock price, risk-free rate, volatility, time until expiration, continuous dividend rate.

One way to use this class is to instantiate it with all 6 inputs and use the get_price() function to get the price according to the BSM model.

Another way to use this class is to calculate implied volatility (IV). IV is the volatility implied by the options market. It uses the market price of a certain option (which is of course determined by supply and demand), and keeps inputting different volatilities into the BSM model until the model spits out the market price. This specific volatility that makes the model price equal the market price is the implied volatility. The function iv() returns the implied volatility.

The third way, and most practical for the stated purpose of this project, is to make use of the 'history' instance attribute. This is yet another spreadsheet. The columns include the option's price, delta, theta, and vega. Each of these are derived from a stock object that is stored in the 'stock' instance attribute. It is through this, and accessing the 'frame' attribute of the stock, that the BSM object can calculate these metrics for each future day.

## Findings and Discussion

The Greeks are important parts of options trading strategies. Here, the change in the Greeks for different options are displayed. Among different options on the same stock (different is defined by different exercise price, expiration date, contract type), how is are the Greeks different?

### Delta
Delta is the first derivative of an option's price with respect to the price of the underlying stock. For every dollar the stock increases, the price of the option is expected to change by delta dollars. Therefore, delta is positive for calls and negative for puts. The absolute value of delta will never exceed 1.

Delta is also an estimate of the chance an option expires in the money.

### Theta
Theta is the first derivative of an option's price with respect to the time left until expiration. For every unit of time (day, in this case) that passes, the price of the option is expected to change by theta dollars. Theta is generally negative (time decay) and approaches 0 as the time remaining approaches 0.

### Vega
Vega is the first derivative of an option's price with respect to the volatility of the stock. For every point volatility increases, the price of the option is expected to rise by vega dollars. Vega is the same for calls and puts and is always positive.
