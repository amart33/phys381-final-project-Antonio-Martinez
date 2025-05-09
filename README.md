# Heat Capacity Simulation below 10 K

## Project Overview
This project simulates the heat capacity of a material at low temperatures and fits the data to extract electronic and lattice contributions. At these temperatures, quantum effects become significant, and heat capacity can be modeled as a sum of two terms: 
* $C_v = \gamma T + \beta T^3$

To better visualize the coefficients through the data, we can linearize the data by dividing by T:

* $C_v/T= \gamma + \beta T^2$

This second equation makes it easier to extract parameters through a simple linear fit. 
This project used known material property values of copper, but these could be changed to your desired material's specific values using its $\gamma$ value and Debye temperature. 
The program simulates a chosen n-number of temperature measurements and trials of the experiment and adds Gaussian noise to mimic uncertainty. It then tabulates and plots the data along with the printed fitted parameters as well as saves these tables and plots. Next it performs a check of the simulation by extracting back the Debye temperature from the simulated data to compare to the original value. Finally it checks the quality of the fits through chi-square analysis. 

## Physics Background
- $\gamma T$ is the electronic contribution to heat capacity
- $\beta T^3$ is the phonon (lattice) contribution from the Debye model
- $\theta_D$ is the Debye temperature of the material. 
- While $\gamma$ and $\theta_D$ are generally well known for materials, $\beta$ is less commonly cataloged in literature. For the initial $\beta$ in this simulation, enter the material's Debye temperature and $\beta$ will be calculated using the following formula:

- $C_v \approx \frac{12\pi^4}{5} R ( \frac{T}{\theta_D } )^3 = \beta T^3 $, where $R$ is the molar gas constant

- To calculate the Debye temperature from the data, the previous equality is just rearranged for $\beta$
- **Note: All values are internally scaled within the program; comments in the code clarify physical units when scaling occurs**

## Methods and Tools
- Python + Jupyter Notebook
- Libraries: `NumPy`, `Matplotlib`, `SciPy`, `Pandas`
- Curve fitting with `scipy.optimize.curve_fit`
- Constants $\pi$ and $R$ from `scipy.constants`
- Error analysis using the covariance matrix
- Chi-squared analysis for model validation

## Inputs and Outputs
#### Inputs
- $\gamma$ and Debye temperature for desired material
- `n` sets number of desired experimental trials and temperature points

#### Outputs
- Simulated heat capacity data with noise
- Fitted parameters with uncertainties
- Saved tabulated data for analysis and export
- Saved plots of data with model fits 
- Debye temperature estimates with uncertainties
- Chi-squared and reduced chi-squared values for goodness of fit

## Results
The simulation was run using copper’s material properties with $\gamma = 0.695\ \text{mJ/mol·K}^2$ and  $\theta_D = 343\ \text{K}$.

Fitting the data to both $C_v = \gamma T + \beta T^3$ and $C_v/T = \gamma + \beta T^2$ models yields accurate extractions of $\gamma$ and $\beta$. The Debye temperature recalculated from the fitted $\beta$ values was consistently very close to the original value of 343 K, validating the accuracy of the simulation. 

The chi-squared analysis showed that the linearized model $C_v/T$ provided better fit quality, though reduced chi-squared values suggest that with the current noise model there may be a slight overfitting of the data. Overall, the simulation effectively reproduces key thermodynamic behavior with interpretable, realistic outputs, though further refinement is needed.

Plots and tabulated results are provided in the notebook.