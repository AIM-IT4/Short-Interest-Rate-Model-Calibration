# Short Interest Rate Model Calibration with QuantLib-Python

## Hull-White 1 Factor Model

The Hull-White model is a practical exogenous model for fitting market interest rate term structures, described by:

$$ dr_t = (\theta(t) - a r_t) \, dt + \sigma \, dW_t $$

Where:
- \( a \) is the mean reversion constant,
- \( \sigma \) is the volatility parameter,
- \( \theta(t) \) is chosen to fit the input term structure of interest rates.

### Calibration in QuantLib-Python

To calibrate the Hull-White model in QuantLib-Python, use the `JamshidianSwaptionEngine`. This requires setting up the model with appropriate market data and then solving for the best-fit parameters \( a \) and \( \sigma \) that minimize the error in pricing known swaptions.

## Black Karasinski Model

The Black Karasinski model is an interest rate model characterized by:

$$ d \ln(r_t) = (\theta_t - a \ln(r_t)) \, dt + \sigma \, dW_t $$

### Calibration Using QuantLib-Python

As this model is non-affine, it necessitates the use of the `TreeSwaptionEngine` for calibration, which is versatile enough to handle various non-affine short rate models. The process involves fitting the model to market swaption volatilities by iteratively adjusting \( a \) and \( \sigma \).

## G2++ Model: A Two-Factor Calibration Example

The G2++ model involves two factors, \( x_t \) and \( y_t \), which add complexity and accuracy to the fitting process:

$$ dr_t = \phi(t) + x_t + y_t $$
$$ dx_t = -a x_t \, dt + \sigma \, dW^1_t \quad \text{(14.1)} $$
$$ dy_t = -b y_t \, dt + \eta \, dW^2_t \quad \text{(14.2)} $$
$$ \langle dW^1_t, dW^2_t \rangle = \rho \, dt \quad \text{(14.3)} $$

### QuantLib-Python Implementation

For calibrating the G2++ model, QuantLib-Python offers several engines including `TreeSwaptionEngine`, `G2SwaptionEngine`, and `FdG2SwaptionEngine`. The choice of engine affects both the calibration time and the accuracy of the fitted model. Calibration typically involves using historical data to estimate the parameters \( a \), \( b \), \( \sigma \), \( \eta \), and \( \rho \), ensuring the model's effectiveness in simulating and predicting future interest rate movements.

