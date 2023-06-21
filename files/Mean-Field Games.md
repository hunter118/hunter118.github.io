# Theory
## Notation
### Setting
- $\Delta(\mathcal{X})$: the set of disbutions over $\mathcal{X}$, $\mathcal{X}$ finite
- $\mathcal{P}(\mathcal{X})$: the set of disbutions over $\mathcal{X}$, $\mathcal{X}$ infinite
- N-player symmetric-anonymous game $(\mathcal{X}, \mathcal{A},r,P,\mu_0)$
	- $r:\mathcal{X}\times \mathcal{A}\times\Delta(\mathcal{X})\to \mathbb{R}$: reward function
	- $P:\mathcal{X}\times \mathcal{A}\times\Delta(\mathcal{X})\to \Delta(\mathcal{X})$: state transition function
	- $\mu_{0}\in \Delta(\mathcal{X})$: initial state
- In an N-player game, we denote by $\mathcal{N}$ the set of players.
- $\mathcal{T}$: the discrete set of times
### Policy
$\bar{\pi}:\mathcal{X}\to \Delta(\mathcal{A})$, $\bar{\pi}(x,a)$ is the probability of playing action $a$ while at state $x$. $\hat{\pi}\in\bar{\Pi}$. $\Pi$ is the set of deterministic policies: $\pi(x)=\delta_{a}$, or $\pi(x,a')=\mathbb{1}_{\{ a'=a \}}$. $\bar{\Pi}$ is the convex hull of $\Pi$. 
### Payoff
$J(\pi_{i},\pi_{-i})$ is the expected return for player $i$ with policy $(\pi_{i},\pi_{-i})$. $J(\pi_{i},\pi_{-i})=\sum_{t\in\mathcal{T}}\left<r_{i,t}^{\pi},\mu_{i,t}\right>$, where $\mu_{i,t}$ is the distribution of player i over states at time $t\in\mathcal{T}$, $r_{i,t}^{\pi}$ is their expected reward vector.
### Policy swap
$\mathcal{U}_{CE}:=\{ u:\Pi \to \Pi \}$, $\mathcal{U}_{CCE}:=\{ u:\Pi\to \Pi\mid u \text{ constant}\}$. Swaps do not need to be bijective.

## $N$-Player Games
### Equilibria in $N$-Player Games
#### $N$-Player Nash Equilibrium
**Definition.** Given $\epsilon>0$, we define an $\epsilon$-Nash Equilibrium $(\pi_{1},\dots,\pi_{n})\in\bar{\Pi}_{1}\times\dots \times \bar{\Pi}_{N}$ as an $n$-tuple of strategies such that 
$$
\max_{\pi_{i}'\in\Pi_{i}}J_{i}(\pi_{i}',\pi_{-i})-J_{i}(\pi_{i},\pi_{-i})\leq \epsilon,\quad\forall i\in \mathcal{N}.
$$
#### $N$-Player $\epsilon$-Correlated Equilibrium
Correlation device: coordinate agents' behaviors, render their recommendations stable in the presence of payoff maximizing player. 
If given a policy recommendation, and given knowledge of the probability distribution over the joint policies recommended by the correlation device, the player does not have an incentive to deviate and play something else, then it's correlated equilibrium.
**Definition.** Given $\epsilon>0$, we define an $\epsilon$-Correlated Equilibrium $\rho\in\Delta(\Pi_{1}\times\dots \times \Pi_{N})$ as a distribution over joint strategies such that 
$$
\mathbf{E}_{\pi\sim\rho}\left[J_{i}(u_{i}(\pi_{i})),\pi_{-i})-J_{i}(\pi_{i},\pi_{-i})\right]\leq \epsilon,\quad\forall u_{i}\in\mathcal{U}_{CE},i\in \mathcal{N}.
$$
#### $N$-Player $\epsilon$-Coarse Correlated Equilibrium
If the player doesn't have ability to a priori find a fixed deviating policy, independent of their received advice, so that they can improve their payoff without even taking their own recommendation into account, then it's coarse correlated equilibrium.
**Definition.** Given $\epsilon>0$, we define an $\epsilon$-Coarse Correlated Equilibrium $\rho\in\Delta(\Pi_{1}\times\dots \times \Pi_{N})$ as a distribution over joint strategies such that 
$$
\mathbf{E}_{\pi\sim\rho}\left[J_{i}(u_{i}(\pi_{i})),\pi_{-i})-J_{i}(\pi_{i},\pi_{-i})\right]\leq \epsilon,\quad\forall u_{i}\in\mathcal{U}_{CCE},i\in \mathcal{N}.
$$
Correlation device helps solving the equilibrium selection problem. When several Nash equilibria exist in a game, players must all somehow choose the same Nash equilibrium to receive any individual optimality guarantee.

### The Special Case of Symmetric $N$-Player Games
All symmetric games are anonymous. In symmetric games, all individual policy sets $\Pi_{i}$ are identical and equal to $\Pi$, and the payoff functions must not be impacted by player identities. This rewrites analogously as follows: the payoff that player i receives when playing $\pi_{i}$ only depends on the proportion of other players playing every policy in $\Pi$. 
**Definition (Population Distribution).** The Population Distribution of $N$ players playing policies in $\Pi$ is defined as $\nu_{N}=\frac{1}{N}\sum_{\pi}n_{\pi}\delta_{\pi}$, where $n_{\pi}$ is the number of players playing $\pi$, and $\delta_{\pi}$ is a dirac centered on $\pi$. The set of N-player population distributions is written $\Delta_{N}(\Pi)$. 
Denote $\nu_{-i}\in \Delta_{N-1}(\Pi)$ the distribution over policies in the population of all players except player $i$. Let $J_{i}(\pi_{i},\pi_{-i})=\mathcal{J}(\pi_{i},\mu_{-i})$.
**Definition (Symmetric Sampling).** When $N$ players sample from $\nu_{N}\in\Delta_{N}(\Pi)$, they are symmetrically assigned a policy from $\nu_{N}$ such that their population distribution is equal to $\nu_{N}$.
**Definition (Population Recommenders).** A population recommender $\rho$ is a distribution over population distributions, i.e. $\rho\in\Delta(\Delta_{N}(\Pi))$. A population distribution sampled by a population recommender is also called a population recommendation.
Rewrite (C)CE definitions.
**Definition ($N$-Player Symmetric $\epsilon$-(Coarse)-Correlated Equilibrium).** Define a symmetric $\epsilon$-(coarse)-correlated equilibrium $\rho$ as a distribution in $\Delta(\Delta_{N}(\Pi))$ such that $\forall i,\forall u\in\mathcal{U}_{(C)CE}$, 
$$
\mathbf{E}_{\nu\sim\rho,\pi_{i}\sim \nu}\left[\mathcal{J}(u(\pi_{i})),\nu_{-i})-\mathcal{J}(\pi_{i},\nu_{-i})\right]\leq \epsilon.
$$
We see below that symmetric equilibria are in fact equivalent to standard equilibria that are symmetric, i.e. that are in $\Delta_{sym}(\Pi^{N})=\{ \nu\in\Delta(\Pi^{N})\mid \forall\tau \text{ permutation},\nu \circ \tau=\nu\}$ the set of distributions over $\Pi^{N}$ that are invariant to player permutations. 
**Theorem (Equilibrium Equivalence).** In symmetric-anonymous N-player games, there is one to one correspondence between symmetric-anonymous $\epsilon$-(C)CE and $\epsilon$-(C)CE with symmetric correlating device, i.e. such that $\rho\in\Delta_{sym}(\Pi^{N})$. 
$N\to \infty,\Delta_{N}(\Pi)\to \Delta(\Pi),\Delta(\Delta_{N}(\Pi))\to \mathcal{P}(\Delta(\Pi))$.  

## Notions of Mean Field Equilibrium
The set of distribution flows $\Delta(\mathcal{X})^{\mathcal{T}}$ on the state space $\mathcal{X}$ over times in $\mathcal{T}$ is denoted by $\mathcal{M}$. Whenever every player in the population follows the policy $\pi\in\Pi$, the game generates a Mean-Field flow over $\mathcal{X}$ denoted by $\mu^{\pi}\in\mathcal{M}$. Formally, 
$$
\mu_{t+1}^{\pi}(x)=\sum_{x_{t}\in\mathcal{X}}\sum_{a\in\mathcal{A}}p(x\mid x_{t},a,\mu_{t}^{\pi})\pi(x_{t},a)\mu_{t}^{\pi}(x_{t}),\quad \forall t\in\mathcal{T},x\in\mathcal{X},
$$
with $\mu_{0}^{\pi}=\mu_{0}$ a initial state.
Given a Mean-Field flow $\mu\in\mathcal{M}$ of the population, the expected reward of a representative player playing policy $\pi\in\Pi$ is given by
$$
J(\pi,\mu)=\sum_{t\in \mathcal{T}}\sum_{x,a}r(x,a,\mu_{t})\mu_{t}^{\pi}(x)\pi(x,a)=\sum_{t\in\mathcal{T}}\left<r^{\pi}(\cdot,\mu_{t}^{\pi}),\mu_{t}^{\pi}\right>,
$$
where $\mu^{\pi}$ the expected state distribution of policy $\pi$ when the population follows the Mean-Field flow $\mu$ and $r^{\pi}(x,\mu)=\sum_{a}\pi(x,a)r(x,a,\mu)$. 
Given a fixed mean-field flow $\mu\in\mathcal{M}$, an individual player can maximise their expected return by solving the following Markov Decision Process (MDP) policy optimisation problem $\sup_{\pi\in\Pi}J(\pi,\mu)$. 
Whenever the population of players plays a distribution of strategies $\nu\in\Delta(\Pi)$, the induced Mean-Field flow over the state space $\mathcal{X}$ is denoted by $\mu(\nu)\in\mathcal{M}$. In the case when the dynamics depend on $\mu$, it is difficult to express $\mu(\nu)$ in closed form. However, in the $\mu$-independent-dynamics case, $\mu(\nu)$ can be expressed in closed form: 
**Lemma (Closed-form $\mu(\nu)$).** In the $\mu$-independent-dynamics case, $\mu(\nu)=\sum_{\pi\in\Pi}\nu(\pi)\mu^{\pi}$.
For $\nu\in\Delta(\Pi)$, we write $\pi(\nu)$ the stochastic policy defined by sampling a policy $\pi\in\Pi$ with probability $\nu(\pi)$ at every initial state of the game, and playing it until the end of the game. $\mu^{\pi(\nu)}=\mu(\nu)$. We note that the set $\{ \pi \mid \mu^{\pi}=\mu(\nu) \}$ may have more than one element, but the definition of $\pi(\nu)$ yields a unique policy. 
Given a policy $\bar{\pi}\in\bar{\Pi}$, we write $\nu_{\bar{\pi}}\in\Delta(\Pi)$ for the distribution such that $\pi(\nu_{\bar{\pi}})=\bar{\pi}$.
An equilibrium is only stable if no player has an incentive to deviate from its recommendations. Since all players are identical, we choose a random representative player. 

### Mean Field Nash Equilibrium
**Definition (Mean Field Nash Equilibrium, MFE).** Given $\epsilon>0$, a policy $\bar{\pi}\in\bar{\Pi}$ is an $\epsilon$-Mean Field Nash Equilibrium whenever
$$
\sup_{\pi'\in\bar{\Pi}}J(\pi',\mu^{\bar{\pi}})\leq J(\bar{\pi},\mu^{\bar{\pi}})+\epsilon.
$$
A Nash equilibrium is said to be pure if it's deterministic.
**Example (Two-Actions Hipster Game).** A unique mixed Nash equilibrium.
**Remark.** Plugging a Mean Field Nash equilibrium in an $N$-player game yields an $O\left( \frac{1}{\sqrt{ N }} \right)$-approximate Nash equilibrium, which is known in the continuous time and continuous space setting.
**Remark.** While the existence of Nash equilibria is a very straightforward property for MFGs to have, deriving the uniqueness of such equilibria in general is a difficult and tedious task.  Adding strong Lipschitz condition or monotonicity condition are possible approaches. 
**Example (Suits Game).** Inverted Hipster game. Three Nash equilibria.

### Mean-Field Correlation Device
**Definition (Population distribution/recommendation).** 
- A **population distribution, or population recommendation** $\nu\in\Delta(\Pi)$ is a distribution over the set of policies $\Pi$;
- Given a population distribution $\nu\in\Delta(\Pi)$, each player receives an **individual recommendation** $\pi\in\Pi$ uniformly sampled from $\nu$, so that the distribution of all individual recommendations over the population is $\nu$.
**Definition (Correlation device).** A correlation device is a distribution $\rho$ over $\Delta(\Pi)$. It encapsulates the possible population recommendations given to the population. We denote $\mathcal{P}(\Delta(\Pi))$ the set of correlation devices.
The exogenous recommender picks a realization of a random variable with distribution $\rho\in\mathcal{P}(\Delta(\Pi))$ and gives each player its own individual recommendation $\pi\in\Pi$ as a signal. All players know $\rho$ together with their own individual recommendation $\pi\in\Pi$, but do not have access to the population recommendation $\nu\in\Delta(\Pi)$ sampled by the recommender. Whenever a player receives $\pi\in\Pi$ as recommendation, their belief about $\nu$ shifts to $\rho(\cdot \mid \pi)$ defined by: 
$$
d\rho(\nu \mid \pi)=\frac{\nu(\pi)d\rho(\nu)}{\int _{\nu'\in\Delta(\Pi)} \nu'(\pi) d\rho(\nu') }.
$$
Define $\rho_{\Pi}(\pi)=\int _{\nu\in\Delta(\Pi)} \nu(\pi)d\rho(\nu)$, then $d\rho(\nu)=\sum_{\pi\in\Pi}\rho_{\Pi}(\pi)d\rho(\nu \mid \pi)$. 
By our definition, agents never observe $\nu$. However, we could also imagine that $\rho$ would send $\nu$ to each agent, and lets agents sample their policy from $\nu$ for the duration of an episode. In this case, agents all play the same policy $\pi(\nu)\in\bar{\Pi}$, and all know what the other agents are playing. We can therefore view $\rho$ as a distribution over the possible values of $\pi(\nu)$, i.e. over $\bar{\Pi}$. 
**Definition (Homogeneous correlation device).** A homogeneous correlation device $\rho_{h}\in\mathcal{P}(\bar{\Pi})$ is a special type of correlation device that samples stochastic policies, and only recommends one stochastic policy to all players in the population.

### Mean-Field Correlated Equilibrium
**Definition (Mean Field Correlated Equilibrium, MFCE).** Given $\epsilon>0$, a correlation device $\rho$ is an $\epsilon$-Mean Field Correlated Equilibrium if, $\forall u\in\mathcal{U}_{CE}$ 
$$
\mathbf{E}_{\nu\sim\rho,\pi \sim \nu}\left[J(u(\pi)),\mu(\nu))-J(\pi,\mu(\nu))\right]\leq \epsilon.
$$
**Proposition.** For all $\epsilon>0$, the set of $\epsilon$-MFCEs is convex.
Define the deviation set of homogeneous correlated equilibria $\mathcal{U}_{CE}^{h}=\{ u\mid u:\bar{\Pi}\to \bar{\Pi} \}$. 
**Definition (Homogeneous Mean Field Correlated Equilibrium).** Given $\epsilon>0$, a homogeneous correlation device $\rho$ is an $\epsilon$-Homogeneous Mean Field Correlated Equilibrium if, 
$$
\mathbf{E}_{\nu\sim\rho}\left[J(u(\pi(\nu)),\mu(\nu))-J(\pi(\nu),\mu(\nu))\right]\leq\epsilon,\quad\forall u\in\mathcal{U}_{CE}^{h}.
$$

### Mean-Field Coarse Correlated Equilibrium
Weaker, easier to compute. Player may only choose to deviate from their recommendation before having observed it, though players are still assumed to have knowledge of the correlation device’s behavior $\rho\in\mathcal{P}(\Delta(\Pi))$. This larger class of equilibria contains correlated equilibria and is more easily reachable by classical learning algorithms. 
**Definition (Mean Field Coarse Correlated equilibrium, MFCCE).**  Given $\epsilon>0$, a correlation device $\rho$ is an $\epsilon$-Mean Field Coarse Correlated Equilibrium if, $\forall u\in\mathcal{U}_{CCE}$ 
$$
\mathbf{E}_{\nu\sim\rho,\pi \sim \nu}\left[J(u(\pi)),\mu(\nu))-J(\pi,\mu(\nu))\right]\leq \epsilon.
$$
Recall that $\mathcal{U}_{CCE}$ denotes the set constant deviations over $\Pi$, i.e. the mappings from $\Pi$ to $\Pi$ with a fixed constant policy $\pi\in\Pi$. MFCCEs can also be defined in an alternative way. 
**Proposition (MFCCE characterization using best-responses).** A correlation device $\rho$ is an $\epsilon$-MFCCE if and only if,
$$
\sup_{\pi'\in\Pi}\mathbf{E}_{\nu\sim\rho}\left[J(\pi',\mu(\nu))\right]\leq\mathbf{E}_{\nu\sim\rho,\pi \sim \nu}\left[J(\pi,\mu(\nu))\right]+\epsilon.
$$
**Proposition.** The set of $\epsilon$-MFCE is included in the set of $\epsilon$-MFCCE.
**Proposition.** For all $\epsilon>0$, the set of $\epsilon$-MFCCEs is convex.
Similarly define the deviation set of homogeneous coarse correlated equilibria $\mathcal{U}_{CCE}^{h}=\{ u\mid u:\bar{\Pi}\to \bar{\Pi},u\text{ constant} \}$. 
**Definition (Homogeneous Mean Field Coarse Correlated Equilibrium).** Given $\epsilon>0$, a homogeneous correlation device $\rho$ is an $\epsilon$-Homogeneous Mean Field Coarse Correlated Equilibrium if, 
$$
\mathbf{E}_{\nu\sim\rho}\left[J(u(\pi(\nu)),\mu(\nu))-J(\pi(\nu),\mu(\nu))\right]\leq\epsilon,\quad\forall u\in\mathcal{U}_{CCE}^{h}.
$$

## Properties of MF(C)CEs
### (Coarse) Correlated Equilibria and Nash Equilibria
#### From E to CE
**Proposition (Nash-derived Correlated Equilibrium).** Every ϵ-Nash equilibrium ($\pi^*\in\bar{\Pi}$) can be transformed into a Correlated Equilibrium ($\rho=\delta_{\nu_{\pi^*}}$). 
#### From CCE to E
Possible when the correlated equilibrium is Dirac.
**Proposition (Coarse correlated equilibrium-derived Nash equilibrium).** Assume $\rho=\delta_{\nu}$, with $\nu\in\Delta(\Pi)$, is an $\epsilon$-coarse correlated equilibrium. Then $\pi(\nu)$ is an $\epsilon$-Nash equilibrium.
In certain classes of games, the marginalization of an $\epsilon$-MFCCE yields an $\epsilon$-Nash equilibrium.
**Definition (Correlation Device Marginalization).** The marginalization $\hat{\pi}$ of a correlation device $\rho$ is defined as the policy whose distribution is equal to $\int _{\nu}\mu(\nu) d\rho(\nu)$.
Note that it always exists when the dynamics do not depend on the distribution.
**Proposition (Existence of the marginalization).** In games where the dynamics do not depend on the mean field flow, the marginalization of a correlation device always exists, and is equal to
$$
\hat{\pi}_{t}(s,a)=\sum_{\pi\in\Pi}\frac{\int _{\nu}\nu(\pi)\mu_{t}^\pi(s)d\rho(\nu)}{\sum_{\pi'\in\Pi}\int _{\nu'}\nu'(\pi')\mu_{t}^{\pi'}(s)d\rho(\nu')}\pi(s,a).
$$
**Definition (Monotonicity).** A mean field game is said to be monotonic if
$$
\left<\mu-\mu',r(\cdot,\mu)-r(\cdot,\mu')\right>\leq 0,\quad\forall\mu,\mu'\in\mathcal{M}.
$$
**Proposition.** In monotonic games where the reward function is affine with respect to $\mu$, the marginalization of an $\epsilon$-MFCCE, if it exists, is a $2\epsilon$-MFE.

### Existence of (C)CE
**Theorem ((Coarse) Correlated equilibrium existence).** If the reward function $r$ and the dynamics kernel function $p$ are continuous with respect to $\mu$, then the game admits at least one (coarse) correlated equilibrium.
**Example (Reward for the few).** Neither correlated nor coarse correlated equilibria exist!
**Theorem (Existence of $\epsilon$-(coarse) correlated equilibria).** For all $\epsilon>0$ small enough, there exists $\epsilon$-(coarse) correlated equilibria in all games. 

### Uniqueness of (C)CE
**Definition (Strictly-dominant strategy).** A strategy $\pi^*\in\bar{\Pi}$ is said to be strictly dominant if
$$
J(\pi^*,\mu)>J(\pi,\mu),\quad\forall\pi\in\Pi,\mu\in\Delta(\mathcal{X})^{\mathcal{T}}.
$$
**Proposition ((Coarse) Correlated equilibria uniqueness).** If there exists a strictly dominant strategy $\pi^*$ in the game, then the game only admits a unique coarse correlated equilibrium, and therefore a unique correlated equilibrium, which only recommends $\nu^*\in\Delta(\Pi)$ such that $\pi(\nu^*)=\pi^*$. 

### Homogeneous CE Characterization
**Proposition.** Let $\epsilon\geq 0$ and $\rho$ be a homogeneous $\epsilon$-MFCE. Then all $\pi\in\Pi$ atoms of $\rho$ are $\frac{\epsilon}{\rho(\pi)}$-MFE.
**Proposition.** Any homogeneous correlation device recommending only $\epsilon$-MFE is an $\epsilon$-MFCE.

## Connections between $N$-Player and Mean-Field Equilibria
### Mean-Field Games to $N$-Player Games
The population recommendation framework is very straightforward to use in $N$-player games: just like in Mean-Field games, we first sample a population recommendation $\nu\sim\rho$, and then for each player, sample a policy from $\nu$. Since there are now only $N$ players, sampling $N$ policies from $\nu$ yields $\nu_{N}\in\Delta_{N}(\Pi)$, a random variable with a law determined by $\nu$ and $N$. This means that we can view $\rho$ as a distribution over $\Delta_{N}(\Pi)$, i.e. $\rho\in\mathcal{P}(\Delta_{N}(\Pi))$: $\rho$ is an $N$-player correlation device. When sampling an $N$-player population recommendation $\nu_{N}$ from a Mean-Field population recommendation $\nu\in\Delta(\Pi)$, we will use the abusive notation $\nu_{N}\sim \nu$.
**Proposition (Mean-Field to N-player equilibria).** Taking $\rho$ a Mean-Field correlation device, and $\rho_{N}$ its $N$-player version, we have that
$$
\mathbf{E}_{\nu\sim\rho,\nu_{N}\sim \nu,\pi\sim \nu_{N}}\left[\mathbf{E}_{\mu^N\sim \mu(\nu)}[J(u(\pi),\mu_{N})]\right]=\mathbf{E}_{\nu_{N}\sim\rho_{N},\pi\sim \nu_{N}}[J(u(\pi),\mu_{N})],\quad\forall u:\Pi\to \Pi.
$$

### $N$-Player to Mean-Field Equilibria
**Theorem(N-player CEs to Mean-Field CEs).** Let (ρN)N be a sequence of ϵN-correlated equilibria in the corresponding N-player game. If the reward function and state transition functions are continuous in µ, and if ϵN → 0, then the limit of the sequence (ρN)N is a Mean-Field correlated equilibrium.
Campi and Fischer.
**Theorem (N-player CCEs to Mean-Field CCEs).** A similar statement holds for coarse correlated equilibria.

### Mean-Field Equilibria in $N$-Player Games
Transitions do not depend on $\mu$ $\to$ Transition functions are Lipschitz w.r.t. $\mu$, $\rho$ sum of Diracs $\to$ All correlating devices
**Theorem.** Let $\rho$ be an $\epsilon\geq 0$-Mean-Field (coarse) correlated equilibrium. If
- the reward function is $\gamma_{r}$-Lipschitz in $\mu$ for the $L_{2}$ norm, and
- the transition function does not depend on $\mu$,
then $\rho$ is an $\epsilon+\frac{2\gamma_{r}T\left(1+\sqrt{ \frac{1}{2N} }\right)}{\sqrt{ N }}$-(coarse) correlated equilibrium of the corresponding $N$-player game.
**Theorem.** Let $\rho$ be an $\epsilon\geq 0$-Mean-Field (coarse) correlated equilibrium. If
- the reward and transition functions are lipschitz in $\mu$ for the $L_{2}$ norm, and
- $\rho$ is a finite sum of diracs,
then $\rho$ is an $\epsilon+O\left( \frac{1}{\sqrt{ N }} \right)$-(coarse) correlated equilibrium of the corresponding $N$-player game.
**Theorem.** Let $\rho$ be an $\epsilon\geq 0$-Mean-Field (coarse) correlated equilibrium. If
- the reward and transition functions are lipschitz in $\mu$ for the $L_{2}$ norm
then $\rho$ is an $\epsilon+O\left( \frac{1}{N^{\frac{1}{4}}} \right)$-(coarse) correlated equilibrium of the corresponding $N$-player game.

# Application
## Regret Minimization
### Empirical Play
**Definition (Empirical Play).** The **empirical play** $\hat{\rho}\in\mathcal{P}(\Delta(\Pi))$ of the sequence of policies $(\pi_{s})_{0\leq s\leq t}$ is the correlation device resulting from uniformly recommending each component. Formally, in the continuous case,
$$
\hat{\rho}(A)=\frac{1}{t}\int _{0}^t \mathbb{1}\{ \nu\in A\mid \pi_{s}=\pi(v) \} ds. 
$$
In the discrete case,
$$
\hat{\rho}(\nu)=\frac{1}{t}\sum_{s=1}^t \delta_{\pi_{s}=\pi(\nu)}.
$$
Motivation: good empirical play ~ MFE
To evaluate how close to optimal the empirical play is, we define policy alterations.
**Definition (Policy Alterations).** The set of Policy Alterations $\mathcal{U}_{A}$ is the set of functions $\bar{\Pi}\to \bar{\Pi}$ such that $u\in \mathcal{U}_{A}$ is a policy alteration if there exists a function $u'\in\mathcal{U}_{CE}$ such that for all $\bar{\pi}=\sum_{\pi\in\Pi}\alpha_{\pi}\pi,u(\bar{\pi})=\sum_{\pi\in\Pi}\alpha_{\pi}u'(\pi)$. Similarly we have Coarse Policy Alterations. 
### External Regret and Coarse Correlated Equilibria
Consider a representative agent in a Mean-Field game, using policy $\pi_{s}$ at time $s$, against a population distribution $\mu_{s}$. The cumulative return of the agent over a time interval $[0,t]$ is given by
$$
\int _{0}^t J(\pi_{s},\mu^s)ds.
$$
**Definition (External Regret).** Given a sequence of population distributions $(\mu_{s})_{0\leq s\leq t}$, the external regret of a policy sequence $(\pi_{s})_{0\leq s\leq t}$ is given by
$$
ExtReg((\pi_{s})_{0\leq s\leq t},(\mu^{s})_{0\leq s\leq t})=\sup_{\pi\in\Pi}\int _{0}^t J(\pi,\mu^s)ds-\int _{0}^t J(\pi_{s},\mu^s)ds.
$$
Of particular interest are methods for selecting policy sequences $(\pi_{s})_{s\geq 0}$ in the presence of a population sequence $(\mu_{s})_{s\geq 0}$ such that the external regret grows as $o(t)$; such a policy sequence is said to be no-regret. 
**Proposition.** Let $\epsilon>0$ and $(\pi_{s})_{0\leq s\leq t}$ be a sequence of policies. Then the following propositions are equivalent.
* $\frac{1}{t}ExtReg((\pi_{s})_{0\leq s\leq t},(\mu^{\pi_{s}})_{0\leq s\leq t})\leq \epsilon$;
* The Empirical Play of $(\pi_{s})_{0\leq s\leq t}$ is an $\epsilon$-Mean Field Coarse Correlated Equilibrium.
Does an asymptotically no-regret algorithm indeed get closer to the set of coarse correlated equilibria as it minimizes regrets, or could it actually remain “away” from this set?
**Proposition.** Let $(\pi_{s})_{0\leq s\leq t}$ be such that $\lim_{ t \to \infty } \frac{1}{t}ExtReg((\pi_{s})_{0\leq s\leq t},(\mu^{\pi_{s}})_{0\leq s\leq t})=0$, and assume the reward function $r$ is bounded and the set of coarse correlated equilibria is non-empty. Then the empirical play of $\pi$, $\hat{\rho}_{\pi}^t$, converges to the set of coarse correlated equilibria $\mathcal{C}$, i.e. $\inf_{\rho_{0}\in\mathcal{C}}d_{\mathcal{W}_{2}}(\hat{\rho}_{\pi}^t,\rho_{0})\to 0$, where $d_{\mathcal{W}_{2}}$ is the Wasserstein-2 distance. 
### Swap Regret and Correlated Equilibria
**Definition (Swap Regret).** Given a sequence of policies $(\pi_{s})_{1\leq s\leq t}$ and a sequence of population distributions $(\mu_{s})_{1\leq s\leq t}$, we define swap regret as
$$
SwapReg((\pi_{s})_{1\leq s\leq t},(\mu_{s})_{1\leq s\leq t})=\sup_{u\in\mathcal{U}_{A}}\int _{s} J(u(\pi_{s}),\mu^s)ds-\int _{s} J(\pi_{s},\mu_{s})ds.
$$
**Proposition.** Let $\epsilon>0$ and $(\pi_{s})_{0\leq s\leq t}$ be a sequence of policies. Then the following two propositions are equivalent.
* $\frac{1}{t}SwapReg((\pi_{s})_{0\leq s\leq t},(\mu^{\pi_{s}})_{0\leq s\leq t})\leq \epsilon$;
* The Empirical Play of $(\pi_{s})_{0\leq s\leq t}$ is an $\epsilon$-Mean Field Correlated Equilibrium.
**Proposition.** Let $(\pi_{s})_{0\leq s\leq t}$ be such that $\lim_{ t \to \infty } \frac{1}{t}SwapReg((\pi_{s})_{0\leq s\leq t},(\mu^{\pi_{s}})_{0\leq s\leq t})=0$. Then the empirical play of $\pi$, $\hat{\rho}_{\pi}^t$, converges to the set of correlated equilibria $\mathcal{C}$, i.e. $\inf_{\rho_{0}\in\mathcal{C}}d_{\mathcal{W}_{2}}(\hat{\rho}_{\pi}^t,\rho_{0})\to 0$. 

## Learning Weak Equilibria in Mean Field Games
**Remark.** They do not require any monotonicity or contractivity properties to be true.
### Mean-Field Joint Fictitious Play
#### Continuous time Joint Fictitious Play Algorithm
In Joint Fictitious Play (Joint FP), at every step, the agents all play simultaneously the same policy which is sampled from the past best responses. In continuous time, at time $s$, each best response is computed as:
$$
\pi_{\tau}^{BR}=\text{argmax}_{\pi'\in\Pi}\int _{0}^{\tau}\left<\mu^{\pi'},r^{\pi'}(\cdot,\mu^{\pi_{s}})\right>ds, 
$$
$$
\mu^{\pi_{\tau}}(x)= \frac{1}{\tau}\int _{0}^{\tau}  \mu^{\pi_{s}^{BR}}(x)ds.
$$
**Remark.** While Joint FP and FP are the same in the N-player setting, they are different here, and only Joint FP directly minimizes external regret.
#### Regret minimization
**Proposition.** For continuous time JFP, at time $\tau$, the regret $ExtReg((\pi(s))_{0\leq s\leq \tau},(\mu^{\pi(s)})_{0\leq s\leq \tau})$ of the continuous time FP policy is of order $O\left( \frac{1}{t} \right)$.
#### Discrete time Joint Fictitious Play Algorithm
![[1.png]]
#### Dominated Strategy Exclusion
**Proposition (Fictitious Play Pareto-Optimality).** Let $(\pi_{t})_{t\in[0,T]}$ be the policies produced by Fictitious Play by time $T>0$. Then a policy sampled from this set will asymptotically almost-surely never be dominated as $T\to \infty$, and the probability of sampling a dominated strategy is $\leq \frac{1}{T}$.

### Mean-Field Online Mirror Descent
#### Discrete time Mean Field Online Mirror Descent
For the Online Mirror Descent algorithm, we introduce a regularizer $h:\Delta(\mathcal{A})\to \mathbb{R}$, that is assumed to be $\rho$-strongly convex for some constant $\rho>0$. Its conjugate $h^*:\mathbb{R}^\mathcal{A}\to \mathbb{R}$ is defined as $h^*(y)=\max_{\pi\in\Pi}[<y,\pi>-h(\pi)]$. When $h$ has good properties we have
$$
\Gamma(y):=\nabla h^*(y)=\underset{\pi}{\arg \max }[<y, \pi>-h(\pi)]
$$
The continuous-time Online Mirror Descent dynamics are defined as
$$
\begin{aligned}
& y_t(x, a, \tau)=\int_0^\tau Q_t^{\pi(s), \mu^{\pi(s)}}(x, a) d s, \quad t \in \mathcal{T} \\
& \pi_t(. \mid x, \tau)=\Gamma\left(y_n(x, ., \tau)\right), \quad t \in \mathcal{T}
\end{aligned}
$$
where we define $Q^{\pi, \mu}=\left(Q_t^{\pi, \mu}\right)_{t \in \mathcal{T}}$ and, with $T=\max _{t \in \mathcal{T}} t$ :
$$
\left\{\begin{array}{l}
Q_T^{\pi, \mu}(x, a)=0 \\
Q_t^{\pi, \mu}(x, a)=r\left(x, a, \mu_t\right)+\sum_{x^{\prime} \in \mathcal{X}} p\left(x^{\prime} \mid x, a, \mu_t\right) \sum_{a^{\prime}} \pi_t\left(x, a^{\prime}\right) Q_{t+1}^{\pi, \mu}\left(x^{\prime}, a^{\prime}\right) \\
\quad t=T-1, T-2, \ldots, 0
\end{array}\right.
$$
where we assume, without loss of generality, that $\mathcal{T}$ is the sequence $0, \ldots, T$.![[2.png]]
#### Convergence Properties
**Theorem.** Online Mirror Descent is a regret minimizing strategy in Mean Field games (no monotonicity required): 
$$
\frac{1}{\tau}ExtReg((\pi(s))_{0\leq s\leq \tau};(\mu^{\pi(s)})_{0\leq s\leq \tau})=O\left( \frac{1}{\tau} \right)
$$
#### Dominated strategy exclusion
**Proposition (Online-Mirror Descent Optimality).** As $t$ tends to infinity, a policy $\pi$ uniformly sampled from $(\pi_{t})_{t\in[0;T]}$ produced by OMD with entropy regularizer almost-surely never takes $0<\epsilon$-dominated actions.
**Remark.** Neither algorithm presented above converges towards a mean-field correlated equilibrium.

### Mean-Field PSRO and Derived Algorithms
#### Adversarial Regret Minimizers
**Adversarial regret minimization**: imagine we are tasked with finding a probability distribution over $N$ actions to maximize a given return. We have to do this $T$ times; while another player chooses an observed reward vector $r_{t}\in\mathcal{R}\subset \mathbb{R}^N$ at each time $t$, with $\mathcal{R}$ a compact subset of $\mathbb{R}^N$.
One can run a regret-minimizing algorithm on the following bandit problem:
At each round, given regret-minimizing algorithm $A$,
1. Get probability distribution $\nu\in\Delta(\Pi)$ over deterministic policies from $A$.
2. Observe reward vector $J(\cdot,\mu(\nu))$.
3. Return reward vector $J(\cdot,\mu(\nu))$ to $A$.
This procedure is then looped over until the algorithm has reached low-enough average regret. In this paper, we show examples of two external regret-minimizing algorithms, Polynomial Weights, and Regret Matching, presented in Algorithm 3 and 4. These two algorithms have, after $T$ iterations, $O\left( \frac{1}{\sqrt{T}} \right)$ regret.
![[3.png]]
![[4.png]]
#### Mean-Field PSRO
Mean-Field PSRO, an adaptation of PSRO to the Mean-Field case, proceeds following the usual PSRO scheme, described in Algorithm 5.
![[5.png]]
Briefly, the algorithm proceeds as follows:
1. Compute a best-response / best-responses to the current distribution / correlation device in a certain way;
2. Integrate this best-response / these best responses to the policy pool;
3. Recompute a new distribution / correlation device;
4. Loop until no new best-response is found / no value improvement is found.
The exact best-response computation type in step 1 depends on whether we compute a correlated equilibrium - in which case a best-response is computed for every policy with non-zero play probability, quantifying the payoff for deviating from being recommended that policy - or a coarse correlated equilibrium / a Nash equilibrium - where a unique best-response is computed against the correlation device / the distribution.
The difficulty in bringing PSRO to the Mean-Field case is the sudden non-linearity of the game with respect to the distribution of policy played by agents: the Mean-Field reward term can now be heavily non-linear. This renders payoff-table-based equilibrium computations impossible, unless one creates an entry for every possible strategy mixture - which is of course impossible. Muller et al. and Wang and Wellman go around this issue by computing equilibria without using payoff tables:
* To compute Nash equilibria, they use either existing Nash-converging algorithms (Wang and Wellman) or black-box approaches (Muller et al.);
* To compute correlated or coarse correlated equilibria, Muller et al. use a distribution generated from the play of adversarial regret minimizers.
The intuition behind using adversarial regret minimizers is the following: if a no-adversarial-regret algorithm minimizes regret against any type of adversary, then it can minimize regret against its own state-distribution-induced reward changes, and thus converge towards coarse correlated and correlated equilibria. 
Both approaches are shown to work theoretically:
**Theorem.** When using a no-swap/external-regret meta-solver with average regret threshold $\epsilon$, and the "right" best-response concept, Mean-Field PSRO converges to an $\epsilon$-MFCE/MFCCE. 
#### Dominated Strategy Exclusion
**Proposition (Mean-Field PSRO’s CE-optimality).** Mean-Field PSRO used to compute Mean-Field correlated equilibria can never recommend a dominated strategy at convergence.
**Proposition (Mean-Field PSRO: Optimality Modification).** Either of the following two PSRO modifications ensures that PSRO never recommends strictly dominated strategies, while keeping PSRO’s convergence guarantees:
* Ensure that all of PSRO’s initial policies are not strictly dominated.
or
* After PSRO’s first iteration, remove all initial policies from the pool and only keep the best-responses.