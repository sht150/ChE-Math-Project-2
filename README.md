# ChE-Math-Project-2
## Mathematical modeling of dimer exhange assay of estrogen receptors
Reference: Goulet, D., 2016. Modeling, simulating, and parameter fitting of biochemical kinetic experiments. siam REVIEW, 58(2), pp.331-353.

Estrogen receptor $ER\alpha$ is found in various cell types in human body. Understanding the rates of formation of these receptors is of particular interest due to their correlation with breast cancer. Typically, the dimer exchange assay protocol is employed for the laboratory studies of estrogen receptors.

The ligand binding protein domain of the estrogen receptor is a monomer $(M_{1})$ which rapidly dimerizes $(D_{11})$ in solution. The equilibrium of the monomer-dimer solution is achieved rapidly and thus, the kinetics of formation of dimer cannot be observed experimentally. Thus, the dimer exchange assay protocol is employed which involves addition of maltose binding protein monomer $(M_{2})$ to the ligand binding protein. This results in sufficiently high equilibriation times to allow the kinetics to be recorded. However, this also results in formation of two other dimers - the fusion dimer $(D_{22})$ and the heterodimer $(D_{12})$.

$
1.$ M_{1} + M_{1} \leftrightarrow D_{11}$
$
\begin{align}
2. M_{2} + M_{2} \leftrightarrow D_{22}
\end{align}
\begin{align}
3. M_{1} + M_{2} \leftrightarrow D_{12}
\end{align}
Let $k_{1f}$ and $k_{1r}$ be forward and backward rate constants for the first reaction. Similarly, $k_{2f}$ and $k_{2r}$ for second reaction and $k_{3f}$ and $k_{3r}$ for third reaction. 

Using the law of mass action, we can get the following species balance equations:

\begin{align}
\frac{dM_{1}}{dt}=-2k_{1f}(M_{1})^{2}+2k_{1r}(D_{11})-k_{3f}(M_{1})(M_{2})+k_{3r}(D_{12})
\end{align}

\begin{align}
\frac{dM_{2}}{dt}=-2k_{2f}(M_{2})^{2}+2k_{2r}(D_{22})-k_{3f}(M_{1})(M_{2})+k_{3r}(D_{12})
\end{align}

\begin{align}
\frac{dD_{11}}{dt}=k_{1f}(M_{1})^{2}-k_{1r}(D_{11})
\end{align}

\begin{align}
\frac{dD_{22}}{dt}=k_{2f}(M_{2})^{2}-k_{2r}(D_{22})
\end{align}

\begin{align}
\frac{dD_{12}}{dt}=k_{3f}(M_{1})(M_{2})-k_{3r}(D_{12})
\end{align}
The above model can be reduced based on the fact that monomesr are never destroyed, they are simply incorporated into dimers.
Thus,
\begin{align}
\frac{d(M_{1}+2D_{11}+D_{12})}{dt}=0
\end{align}

\begin{align}
\frac{d(M_{2}+2D_{22}+D_{12})}{dt}=0
\end{align}

##### Assumptions
1. Addition of maltose binding protein to ligand binding protein does not significantly alter dimerization kinetic parameters. Thus, $k_{1f} = k_{2f} = k_{3f}/2 = k_{f}$ and $k_{1r} = k_{2r} = k_{3r} = k_{r}$
2. Initial monomer concenrations are negligible

Incorporating the above assumptions in the system of ordinary differential equations of species balance, the model can be reduced to the following three equations:

\begin{align}
\frac{dD_{11}}{dt}=k_{f}(2D_{11}(t_{0})+D_{12}(t_{0})-2D_{11}+D_{12})^{2}-k_{r}(D_{11})
\end{align}

\begin{align}
\frac{dD_{22}}{dt}=k_{f}(2D_{22}(t_{0})+D_{12}(t_{0})-2D_{22}+D_{12})^{2}-k_{r}(D_{22})
\end{align}

\begin{align}
\frac{dD_{12}}{dt}=2k_{f}(2D_{11}(t_{0})+D_{12}(t_{0})-2D_{11}+D_{12})(2D_{22}(t_{0})+D_{12}(t_{0})-2D_{22}+D_{12})-k_{r}(D_{12})
\end{align}
where, $t_{0}$ is initial time
