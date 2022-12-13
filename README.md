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

### Parameter fitting
The parameter fitting was carried out by minimizing the root mean square function of the experimental data.
```
from scipy.optimize import minimize

sol1 = minimize(RMSE, x0 = (280, 0.1));

print(sol1);
```
 fun: 0.38108519866792356
 hess_inv: array([[0.41656698, 0.11359929],
       [0.11359929, 0.03246353]])
      jac: array([0.00011528, 0.00029674])
  message: 'Desired error not necessarily achieved due to precision loss.'
     nfev: 181
      nit: 9
     njev: 55
   status: 2
  success: False
        x: array([278.98170532,   0.3063763 ])

The parameter fit was obtained as (kf,kr) = (279, 0.31) and these values were used in further analysis. The following figure shows the plot of experimental data and model fit.

