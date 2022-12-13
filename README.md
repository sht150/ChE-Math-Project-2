# ChE-Math-Project-2
## Mathematical modeling of dimer exchange assay of estrogen receptors
Reference: Goulet, D., 2016. Modeling, simulating, and parameter fitting of biochemical kinetic experiments. siam REVIEW, 58(2), pp.331-353.

Estrogen receptor $ER\alpha$ is found in various cell types in human body. Understanding the rates of formation of these receptors is of particular interest due to their correlation with breast cancer. Typically, the dimer exchange assay protocol is employed for the laboratory studies of estrogen receptors.

The ligand binding protein domain of the estrogen receptor is a monomer $(M_{1})$ which rapidly dimerizes $(D_{11})$ in solution. The equilibrium of the monomer-dimer solution is achieved rapidly and thus, the kinetics of formation of dimer cannot be observed experimentally. Thus, the dimer exchange assay protocol is employed which involves addition of maltose binding protein monomer $(M_{2})$ to the ligand binding protein. This results in sufficiently high equilibriation times to allow the kinetics to be recorded. However, this also results in formation of two other dimers - the fusion dimer $(D_{22})$ and the heterodimer $(D_{12})$.


1. $M_{1} + M_{1} \leftrightarrow D_{11}$

2. $M_{2} + M_{2} \leftrightarrow D_{22}$

3. $M_{1} + M_{2} \leftrightarrow D_{12}$

Let $k_{1f}$ and $k_{1r}$ be forward and backward rate constants for the first reaction. Similarly, $k_{2f}$ and $k_{2r}$ for second reaction and $k_{3f}$ and $k_{3r}$ for third reaction. 

Using the law of mass action, we can get the following species balance equations:

$\frac{dM_{1}}{dt}=-2k_{1f}(M_{1})^{2}+2k_{1r}(D_{11})-k_{3f}(M_{1})(M_{2})+k_{3r}(D_{12})$

$\frac{dM_{2}}{dt}=-2k_{2f}(M_{2})^{2}+2k_{2r}(D_{22})-k_{3f}(M_{1})(M_{2})+k_{3r}(D_{12})$

$\frac{dD_{11}}{dt}=k_{1f}(M_{1})^{2}-k_{1r}(D_{11})$

$\frac{dD_{22}}{dt}=k_{2f}(M_{2})^{2}-k_{2r}(D_{22})$

$\frac{dD_{12}}{dt}=k_{3f}(M_{1})(M_{2})-k_{3r}(D_{12})$

The above model can be reduced based on the fact that monomesr are never destroyed, they are simply incorporated into dimers.
Thus,
$\frac{d(M_{1}+2D_{11}+D_{12})}{dt}=$

$\frac{d(M_{2}+2D_{22}+D_{12})}{dt}=0$

##### Assumptions
1. Addition of maltose binding protein to ligand binding protein does not significantly alter dimerization kinetic parameters. Thus, $k_{1f} = k_{2f} = k_{3f}/2 = k_{f}$ and $k_{1r} = k_{2r} = k_{3r} = k_{r}$
2. Initial monomer concenrations are negligible

Incorporating the above assumptions in the system of ordinary differential equations of species balance, the model can be reduced to the following three equations:

$\frac{dD_{11}}{dt}=k_{f}(2D_{11}(t_{0})+D_{12}(t_{0})-2D_{11}+D_{12})^{2}-k_{r}(D_{11})$

$\frac{dD_{22}}{dt}=k_{f}(2D_{22}(t_{0})+D_{12}(t_{0})-2D_{22}+D_{12})^{2}-k_{r}(D_{22})$

$\frac{dD_{12}}{dt}=2k_{f}(2D_{11}(t_{0})+D_{12}(t_{0})-2D_{11}+D_{12})(2D_{22}(t_{0})+D_{12}(t_{0})-2D_{22}+D_{12})-k_{r}(D_{12})$

where, $t_{0}$ is initial time

### Experimental data for dimerization assay kinetics
# Fig 1
### Parameter fitting
The parameter fitting was carried out by minimizing the root mean square function of the experimental data.
```
from scipy.optimize import minimize

sol1 = minimize(RMSE, x0 = (280, 0.1));

print(sol1);
```
 fun: 0.38108519866792356
 x: array([278.98170532,   0.3063763 ])

The parameter fit was obtained as (kf,kr) = (279, 0.31) and these values were used in further analysis. The following figure shows the plot of experimental data and model fit.
# Fig 2
The above plot indicates that the parameters fit well do the experimental data. The guess values for the parameter were obtained from the reference paper's fitted parameter values. The kf parameter is difficult to obtain using this system of equations and it converges very close to the guess value. This is due to the assumption that initial monomer concentrations are equal to zero and initial condition values for dimer concentration being used at time = 0.03 hours instead of zero. This observation is also verified by the paper. The value for kr converges close to the value obtained in the paper from a reasonable initial guess.

### Local sensitivity analysis
The parametric sensitivity analysis is performed below changing the parameter values by 1%
```
y1 = odeint(odes, ic, time, args=(279*1.01, 0.31))
y2 = odeint(odes, ic, time, args=(279, 0.31*1.01))
plt.plot(time, ((y1[:,0] - y[:,0])/y[:,0])/0.01,'b', label = "kf");
plt.plot(time, ((y2[:,0] - y[:,0])/y[:,0])/0.01,'r', label = "kr");
```
# Fig 4
The above analysis indicates that kr is much more sensitive than kf. The sensitivity of kf is very close to zero also corroborating the fact that it is difficult to obtain in the first section of model fitting

### Global sensitivity analysis
Perturbing the the parameters by 20% and plotting the fit for the dimer values at 1000 different values of parameter values and saving the dimer concentration values for all parameter values.
```
N = 1000
kf = np.random.uniform(279*0.8,279*1.2,N);
kr = np.random.uniform(0.31*0.8,0.31*1.2,N);

D11 = np.zeros(N);

for m in np.arange(0,N,1):
    output = odeint(odes, ic, time, args = (kf[m],kr[m]));
    plt.plot(time,output[:,0]);
    plt.xlabel("time (h)");
    plt.ylabel("Dimer concentration");
    D11[m]=output[-1,1]
```
# Fig 5
Computing the sensitivity of parameter to dimer concentration using the data generated above when the parameters were perturbed by 20% by linear regression
```
import statsmodels.api as sm
model = sm.OLS(a, X).fit()
print(model.summary())
```
Our fitted eqn is y =  0.0031811286448036463 kf +  -0.020499943928739533 kr
The above global sensitivity analysis indicates that kr is a much more sensitive parameter than kf and it affects the predicted dimer concentration most significantly.

### Bifurcation analysis
The most sensitive parameter, kr, was chosen for the bifurcation analysis of this system. kr was chosen pver kf because its sensitivity is very close to zero and it is not expected to chnage the output of the model significantly
# Fig last
The above plot shows that changing the parameter by 33% does not affect the system and its trajectory.

In conclusion,
The model fits backward rate constants well, but estimation of forward rate constant is limited by assumptions. Backward rate constant has higher sensitivity to estimated dimer concentration than forward rate constant.
For better understanding, the original model with five equations and six parameters which would relax the assumptions should be employed.
