## Brownian motion

### Definition
$B(t)$ Brownian motion (Wiener process)
- $B(0)=0$ a.s.
- $B(t)-B(s)\sim \mathcal{N}(0,t-s)$ for $t\geq s$
- For $0\leq t_{1}<t_{2}<\dots<t_{n}$, $B(t_{1}),B(t_{2}-t_{1}),\dots,B(t_{n}-t_{n-1})$ are independent
- Almost all paths of $B(t)$ are continuous

### Properties
1. $B(t)\sim \mathcal{N}(0,t)$, $\mathbf{E}(B(t)B(s))=t \wedge s$.
3. Translation invariance. $t_{0}\geq 0$, $\tilde{B}(t)=B(t+t_{0})-B(t_{0})$ is also BM.
4. Scaling invariance. For $\lambda>0$, $\tilde{B}(t)=\frac{1}{\sqrt{ \lambda }}B(\lambda t)$ is also BM.
5. $B(t)$ is a.s. nowhere differentiable. 

### Wiener Integral
$f$ deterministic. How to define $\int _{a}^{b}f(t)dB(t)$?
Unbounded variation case cannot use Riemann-Stieljies integral. 
$L^2[a,b]$ Hilbert space.

**Step 1.** Let $f(t)=\sum_{i=1}^n a_{i}\mathbf{1}_{[t_{i-1},t_{i})}$, $t_{0}=a,t_{n}=b$, Define $I(f)=\sum_{i=1}^n a_{i}(B(t_{i})-B(t_{i-1}))=\int _{a}^b f(t) dB(t)$. It's easy to check $I$ is linear for simple functions. 
**Lemma.** $I(f)$ is a Gaussian r.v. with $\mathbf{E}(I(f))=0$ and $V(I(f))=\mathbf{E}(I(f)^2)=\int _{a}^b |f(t)|^2 dt=||f||_{L^2[a,b]}^2$. 

**Step 2.** $L^2(\Omega)=\{ X:\Omega\to \mathbb{R}, \mathbf{E}(|X|^2)<\infty \}$ is a Hilbert space with $\left<X,Y\right>_{L^2(\Omega)}=\mathbf{E}(XY)=\int _{\Omega}XY dP$. Let $f\in L^2[a,b]$. 
Choose a sequence $\{ f_{n} \}$ of simple functions in $L^2[a,b]$, $f_{n}\to f$ in $L^2[a,b]$. So $\{ f_{n} \}$ is a Cauchy sequence in $L^2[a,b]$. $\forall \epsilon>0,\exists N>0, s.t. ||f_{n}-f_{m}||_{L^2[a,b]}<\epsilon$ for $n,m>N$. 
$|I(f_{n})-I(f_{m})|_{L^2(\Omega)}=|I(f_{n}-f_{m})|_{L^2(\Omega)}=|f_{n}-f_{m}|_{L^2[a,b]}<\epsilon$.
Thus, $\{ I(f_{n}) \}$ is a Cauchy sequence in $L^2(\Omega)$. Define $I(f)=\lim_{ n \to \infty }I(f_{n})$ in $L^2(\Omega)$. 
Check: $I(f)$ does not depend on the choice of the simple function sequence, using lemma.

**Definition.** $I(f)$ is called the **Wiener integral** of $f$ on $[a,b]$, denoted $I(f)=\int _{a}^b f(t)dB(t)$. 
**Lemma.** $I(af+bg)=aI(f)+bI(g)$. 
**Lemma.** $I(f)$ is a Gaussian r.v. with $\mathbf{E}(I(f))=0$ and $\mathbf{E}(I(f)^2)=\int _{a}^b|f(t)|^2 dt=||f||_{L^2[a,b]}^2$. 
**Theorem.** $I:L^2[a,b]\to L^2(\Omega)$ is an isometry and preserves inner product. 

**Theorem.** Let $f$ be a continuous function on $[a,b]$ with bounded variation. Then for almost all $\omega\in\Omega$, $(W)\int_{a}^b f(t)dB(t)=(RS)\int_{a}^b f(t)dB(t)$. 

## Martingale
Let T be either an interval in $\mathbb{R}$ or the set of positive numbers.
A **filtration** is an increasing family of $\sigma$-algebras $\{ \mathcal{F}_{t} \}$, $\mathcal{F}_{s}\subset \mathcal{F}_{t}$ if $s\leq t$. 
A s.p. $X(t)$ is said to be **adapted to** $\{ \mathcal{F}_{t} \}_{t\in T}$ if for each $t\in T$, $X(t)$ is $\mathcal{F}_{t}$-measurable.
**Definition.** Let $X(t)$ be a stochastic process on $T$, and adapted to $\{ \mathcal{F}_{t} \}_{t\in T}$. $\mathbf{E}(|X|)<\infty$. $X(t)$ is called a **Martingale** if for $s\leq t$, ($X_{t}=X(t)$)
$$
\mathbf{E}(X_{t}\mid \mathcal{F}_{s})=X_{s}\quad a.s.
$$
**Submartingale** $\mathbf{E}(X_{t}\mid \mathcal{F}_{s})\geq X_{s}\quad a.s.$
**Supermartingale** $\mathbf{E}(X_{t}\mid \mathcal{F}_{s})\leq X_{s}\quad a.s.$
If $X(t)$ is a martingale w.r.t. $\{ \mathcal{F}_{t} \}_{t\in T}$, then $\mathbf{E}(X(t))$ is constant. 

**Example.** $B(t)$ is a BM, $\mathcal{F}_{t}=\sigma(B(s),s\leq t)$, for $s\leq t$, $\mathbf{E}(B(t)\mid \mathcal{F}_{s})=\mathbf{E}(B(t)-B(s)\mid \mathcal{F}_{s})+\mathbf{E}(B(s)\mid \mathcal{F}_{s})=B(s)$ a.s.; $\mathbf{E}(B(t)^2\mid \mathcal{F}_{s})\geq(\mathbf{E}(B(t)\mid \mathcal{F}_{s}))^2=B(s)^2$. $B(t)^2$ is a submartingale. ($|B(t)|$ too)
**Example.** $\{ X_{m} \}_{m\geq 1}$ is a sequence of i.i.d. r.v.s, $S_{n}=X_{1}+\dots+X_{n}$. Sign of $\mathbf{E}(X_{1})$. 
**Example.** Let $Y$ be an integrable r.v., $\{\mathcal{F}_{n}\}_{n\geq 1}$ is a filtration. Take $X_{n}=\mathbf{E}(Y\mid \mathcal{F}_{n})$. $\{X_{n}\}_{n\geq 1}$ is a martingale. 
**Example.** Let $\{ X_{n} \}_{n\geq 1}$ be a increasing sequence of integrable r.v.s, $\{ \mathcal{F}_{n} \}_{n\geq 1}$ filtration. $\mathcal{F}_n=\sigma(X_{m},m\leq n)$. Submartingale. 
**Example.** Let $\{ X_{n} \}_{n\geq 0}$ be a submartingale. Then $\mathbf{E}(X_{n}-X_{n-1}\mid \mathcal{F}_{n-1})\geq 0$ a.s. Let $A_{n}=\sum_{k=1}^n \mathbf{E}(X_{n}-X_{n-1}\mid \mathcal{F}_{n-1})$, $M_{n}=X_{n}-A_{n}-X_{0}$. Then $\{ M_{n} \}$ is a martingale. 
$$
X_{n}=X_{0}+M_{n}+A_{n}. \text{(Doob's decomposition)}
$$
Easy to check: this decomposition is unique. 

**Theorem (Doob's decomposition).** Let $\{ X_{n} \}_{n\geq 0}$ be a submartingale. Then there exists a martingale $\{ M_{n} \}_{n\geq 0}$ and $\{ A_{n} \}_{n\geq 0}$, $A_{n}\leq A_{n+1}$ a.s., with $A_{n}$ being $\mathcal{F}_{n-1}$-measurable, such that $X_{n}=X_{0}+M_{n}+A_{n}, M_{0}=0, A_{0}=0$. Moreover, such decomposition is unique. 

**Theorem (Doob's first martingale inequality).** $\{ M_{n} \}_{n\geq 0}$ martingale. $\tilde{M}_{n}=\sup_{j\leq n}|M_{j}|$. Then
$$
P(\tilde{M}_{n}\geq\lambda)\leq \frac{1}{\lambda}\mathbf{E}(|M_{n}|).
$$
**Theorem (Doob's $L^p$ martingale inequality).** 
$$
\mathbf{E}(\tilde{M}_{n}^p)\leq c\cdot\mathbf{E}(|M_{n}|^p) \quad 1<p<+\infty
$$
where $c$ is a constant depending only on $p$. 
**Lemma.** $\mathbf{E}(X^p)=\int_{0}^{+\infty}p\lambda^{p-1}P(X\geq\lambda)d\lambda\quad 1<p<+\infty$. 
Hint. Take $X_{n}=|M_{n}|\mathbf{1}_{\{ |M_{n}|\geq\alpha/2\}}$, $Z_{j}=\mathbf{E}(X_{n}\mid \mathcal{F}_{j}),1\leq j\leq n$. $|M_{j}|\leq Z_{j}+\frac{\alpha}{2}$. $P(\tilde{M}_{n}\geq\alpha)\leq P(\tilde{Z}_{n}\geq\alpha/2)\leq \frac{2}{\alpha}\mathbf{E}(|{Z}_{n}|)=\frac{2}{\alpha}\mathbf{E}(X_{n})$. Use lemma. 

**Example.** $\int_{0}^1B(t)dt=(t-1)B(t)\bigg|_{0}^1-\int_{0}^1(t-1)dB(t)$
$\mathbf{E}\left( \int_{0}^1B(t)dt \right)=0$
$\mathbf{E}\left(\left(  \int_{0}^1B(t)dt  \right)^2\right)=\mathbf{E}\left( \left( \int_{0}^1(t-1)dB(t) \right)^2 \right)=\int_{0}^1(t-1)^2dt=\frac{1}{3}$
$\int_{0}^1B(t)dt\sim \mathcal{N}\left( 0,\frac{1}{3} \right)$
