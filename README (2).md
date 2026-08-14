# Range Based Volatility Estimation from Candlestick Data

An exact simulation, estimator efficiency, and real market application of
range based volatility estimators, built from first principles rather than
treated as off the shelf formulas.

## Motivation

Every trading day the market hands you four numbers: the open, the high,
the low, and the close. Almost every volatility measure in common use is
built from just two of them, open and close. This notebook is about the
other two: what they are worth, when the classical formulas that use them
break down, and how close a real estimator can get to the best possible
one, a question researchers were still refining as recently as the last
few years.

## What is inside

1. **Model and notation.** Log price as Brownian motion, the object of
   study made precise.
2. **Environment.** Setup and dependencies.
3. **Distribution of the extremes.** The exact conditional law of a
   Brownian bridge's high and low, derived rather than assumed.
4. **Exact bar simulation and discretization bias.** A candlestick
   simulator with no artificial bias, and a measurement of the bias that
   naive discretization introduces.
5. **Classical estimators.** Parkinson, Garman Klass, Rogers Satchell, and
   Yang Zhang, derived and implemented.
6. **Efficiency under ideal conditions and under gaps.** How much better
   these estimators are than close to close, measured precisely, and how
   that efficiency changes once overnight gaps enter the picture.
7. **Discretization bias and the MSE crossover.** The point at which a
   biased but efficient estimator stops being worth using.
8. **Detection as time.** Reframing efficiency as how many fewer days are
   needed to detect a genuine change in volatility.
9. **The wick statistic and its constant.** An original statistic
   introduced in this notebook, with an exact closed form constant,
   verified three independent ways.
10. **Jumps at two timescales.** How permanent jumps and flash crashes
    each distort the estimators differently.
11. **The linear efficiency frontier.** The best possible linear
    combination of bar features, and how close it comes to the
    theoretical ceiling.
12. **Empirical application.** The full toolkit applied to real intraday
    data for the Nifty 50 index, Adani Enterprises, and Paytm.
13. **Conclusions.**
14. **Extensions and research directions.**
15. **References.**

## Key result

The commonly quoted Parkinson efficiency of 5.2 times close to close is
not supported; the correct asymptotic value is 4.91, confirmed both in
closed form and by direct simulation. Applied to real data, the same
toolkit that proves this also diagnoses very different real assets
correctly: the Nifty 50 index shows a large share of its real risk
arriving overnight rather than during the trading session, Adani
Enterprises is extremely volatile but concentrates that risk intraday
rather than overnight despite a well documented crash history, and Paytm
alone crosses the jump threshold, consistent with its real regulatory
driven crash in early 2024.

## Tech stack

`numpy`, `scipy` (stats, integrate), `matplotlib`

## Repository structure

```
.
├── candlestick_volatility.ipynb   Full notebook: theory, derivation, and code
└── README.md
```

## Running it

```bash
pip install numpy scipy matplotlib
jupyter notebook candlestick_volatility.ipynb
```

Sections 1 through 11 and 13 through 15 run entirely on simulated paths
with fixed random seeds, fully reproducible offline. Section 12 tries a
live fetch of real intraday data for the three assets, and falls back to
an embedded real snapshot bundled in the notebook if that fetch fails, so
the notebook runs end to end even without internet access.

## References

- Christensen, K. and Podolskij, M. (2007). *Realized Range Based
  Estimation of Integrated Variance.* Journal of Econometrics.
- Parkinson, M. (1980). *The Extreme Value Method for Estimating the
  Variance of the Rate of Return.* Journal of Business.
- Garman, M. and Klass, M. (1980). *On the Estimation of Security Price
  Volatilities from Historical Data.* Journal of Business.
- Rogers, L.C.G. and Satchell, S.E. (1991). *Estimating Variance From High,
  Low and Closing Prices.* Annals of Applied Probability.
- Yang, D. and Zhang, Q. (2000). *Drift Independent Volatility Estimation
  Based on High, Low, Open, and Close Prices.* Journal of Business.
- Roll, R. (1984). *A Simple Implicit Measure of the Effective Bid Ask
  Spread in an Efficient Market.* Journal of Finance.
