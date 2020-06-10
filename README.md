# Keep static for the time being - shifting to a survey paper on RL

# Table of contents
* [Quote](#Quote)
* [Problems](#Problems)
* [Key Ideas](#Key-Ideas)
* [Books](#Books)
* [RL](#RL)
* [DL, Online and Bandits](#DL-Online-and-Bandits)
* [Classic Portfolio Selection Materials](#Classic-Portfolio-Selection-Materials)
* [Machine Learning based Portfolio Selection](#Machine-Learning-based-Portfolio-Selection)
* [Canonical Correlation Analysis](#Canonical-Correlation-Analysis)
* [Sample Efficient](#Sample-Efficient)

# Deliverables for transfer on PhD


# Quote

One should avoid solving more difficult intermediate problems when solving a target problem. Vladimir Vapnik, Statistical Learning Theory, 1998

# Problems

Related to stochastic optimal control - Can do model free with simulations RL and Deep RL

1) Merton Problem (Portfolio and consumption)
2) Optimal Execution - Liquidation Problem
3) Optimal Execution - Limit Order Placement
4) Optimal Stopping and Control
5) Optimal Execution for statistical arbitrage
6) Optimal execution targetting volume
7) Market Making problems
8) Pairs trading - optimal entry/ exit
9) Multi-period parametric policies (Brandt in mult-period)
10) Optimal hedging of derivatives with path dependency (JPM - explore the model and more, when is it better than monte carlo and greeks).

Simulation

Stochastic optimal control assumes a model, simulations assume some knowledge of the world (say monte carlo), alternative and more robust simulation methods ? (for example GAN's for time series).



# Key Ideas

We are looking to allocate to assets or strategies in a manner that is better than the current state of the art and to get RL working in real world finance. Reinforcement learning is a method for solving MDP's in a model free fashion. There are many MDP problems in finance and a whole mathematical methodology such as stochastic optimal control. Applications are myriad and range from investment/ consumption decisions, derivative hedging, algorithmic trading and inventory management. Solutions may have particular value when there is path dependency on an agent's decisions into the future. 

In the derivative hedging method of finance, problems are usually solved in a step-wise fashion...often by calculating or adjusting the greeks, or in more awkward cases by monte carlo methods. Recent paper's hint at the ability to directly learn a hedging strategy in a greek free fashion from a simulation of the environment. In other words rather than a 2 step process - model the environment, solve the model, we can go straight from simulation to hedging, including where there are difficult real life problems such as transaction costs and path dependency and indeed complex risk adjusted functions of our final distribution of returns that we wish to maximise.

Allocation decisions within Finance lie within a most difficult environment. It is partially observed, noisy, and non-stationary, there may be outliers and regimes. Time also plays a key role and decisions again may have long term consequences. 
In contradistinction to standard methods we are not looking to apply single period prediction and then combine these predictions using an optimiser. This is akin to supervised learning, but in the real world our actions may have long term effects and indeed actions taken by our agents may be reacted against by the environment.

Most standard methods are single period and represent a two stage process, this involves two sets of parameters and forecast error is not utility, so we may even be optimising the wrong target. Other works give up upon some of our ability to predict and are thus more heuristic but more practical methods for allocation decisions, albeit pessimistic.

An information bottleneck is created between the supervised forecast error minimisation and the subsequent forecasts which are then used by an optimiser (some argue that this also serves as an error maximiser and indeed has its own parameters to be found). Given the noise inherent within finance and the fact that predictions are either very weak or indeed only exist for small windows of time then this makes the two stage process even more problematic.

Research has been created to address the two stage parameter estimation - Brandt and this enable a more aligned target.
However most current academic work applying RL to allocation decisions is either on a very small scale or ignores basic practical realities of markets (such as transaction costs). Moody et al. appear to have been the earliest to understand these issues and attempt to have one set of parameters, a single utility, include transaction costs and directly map from inputs to actions (rather than predict then optimise).

The Moody work was nearly 20 years ago and indeed he left academic in 2003 to set up a successful hedge fund (which continues to be successful).

My goal is to advance this work using the latest in deep reinforcement learning (and potentially deep learning).
The goal is to examine the state of the art, and advance it - particularly with a view to practicality, it is the author’s view that the current gap between the state of the art in RL in academia but applied within finance remains impractical. And in both parts of the research I am examining multi-period, path dependent decision making in difficult environments in a direct rather than 2 stage indirect fashion.

It should also be noted that explainability and sensitivity analysis is important in finance, black boxes are not widely trusted and indeed legally there may be cases where explainability is forced. I propose to also examine RL methods within this domain where sensitivity analysis and explainability is enabled.

A further question is if we are seeking to move directly from inputs to actions which in this case will be allocation weights with an objective of maximising say some long run utility, then there are practical questions as regards transaction costs, sparsity and indeed including practical constraints such as a draw down constraint. Also there are questions as regards throwing noisy time series into an RL agent and the best way to do this, for example if we go ‘deep’ do autoencoders have a part to play and should we be seeking to induce sparsity in our agent’s allocations?

Note that allocation problems, may in some cases be reduced to single state bandit problems and note that sometimes a poor model of the environment may be known and the agent may possibly be able to bootstrap from here. Allocations may be to experts, assets, or indeed strategies.


# Books

* (book) [Portfolio Selection](https://www.math.ust.hk/~maykwok/courses/ma362/07F/markowitz_JF.pdf), Markowitz (1952).
* (book) [Continuous Time Finance](https://www.amazon.co.uk/Continuous-Time-Finance-Macroeconomics-Robert-Merton/dp/0631185089/ref=sr_1_1?keywords=continuous+time+finance&qid=1552911190&s=gateway&sr=8-1), Merton (1992).
* (book) [Learning Bayesian Networks](http://www.cs.technion.ac.il/~dang/books/Learning%20Bayesian%20Networks(Neapolitan,%20Richard).pdf), Neopolitan (2003).
* (book) [Advances in Financial Machine Learning](https://www.amazon.co.uk/Advances-Financial-Machine-Learning-Marcos/dp/1119482089), De Marcos (2018).
* (book) [Active Portfolio Management](https://www.amazon.co.uk/Active-Portfolio-Management-quantative-producing/dp/0070248826/ref=sr_1_12?ie=UTF8&qid=1551529726&sr=8-12&keywords=portfolio+management), Grinold and Kahn (1999).
* (book) [Efficient Asset Management](https://www.amazon.co.uk/Management-Optimization-Allocation-Association-2008-03-20/dp/B01K0T9PLA/ref=sr_1_2?crid=HQUZ8WEPB4Q3&keywords=efficient+asset+management&qid=1552910379&s=gateway&sprefix=efficient+asset+%2Caps%2C132&sr=8-2), Michaud (2008).
* (book) [Probabilistic Graphical Models: A New Way of Thinking in Financial Modelling](https://www.amazon.co.uk/Probabilistic-Graphical-Models-Financial-Modelling/dp/1782720979/ref=sr_1_2?crid=3GE4YB6FPV1W8&keywords=probabilistic+graphical+models&qid=1552910436&s=gateway&sprefix=probabilistic+%2Caps%2C135&sr=8-2), Denev (2015).
* (book) [Portfolio Management under Stress](https://www.amazon.co.uk/Portfolio-Management-under-Stress-Bayesian-Net/dp/1107048117/ref=sr_1_fkmrnull_1?keywords=portfolio+management+under+stress&qid=1552910585&s=gateway&sr=8-1-fkmrnull), Rebonnato (2014).
* (book) [Risk Assessment and Decision Analysis with Bayesian Networks](https://www.amazon.co.uk/Assessment-Decision-Analysis-Bayesian-Networks/dp/1138035114/ref=sr_1_fkmrnull_1?crid=JRRYQZZZYNNZ&keywords=risk+assessment+and+decision+analysis+with+bayesian+networks&qid=1552910520&s=gateway&sprefix=risk+asses%2Caps%2C133&sr=8-1-fkmrnull), Fenton (2018).
* (book) [Portfolio Construction and Risk Budgeting](https://www.amazon.co.uk/Portfolio-Construction-Risk-Budgeting-5th/dp/1782721002/ref=sr_1_fkmrnull_1?keywords=portfolio+construction+and+risk+budgeting&qid=1552910729&s=gateway&sr=8-1-fkmrnull), Scherer (2015).
* (book) [Machine Learning for Algorithmic Trading](https://www.amazon.co.uk/Hands-Machine-Learning-Algorithmic-Trading/dp/178934641X/ref=sr_1_1?keywords=machine+learning+for+algorithmic+trading&qid=1552910896&s=gateway&sr=8-1), Jansen (2018).
* (book) [Financial Signal Processing and Machine Learning](https://www.amazon.co.uk/Financial-Signal-Processing-Machine-Learning/dp/1118745671/ref=sr_1_fkmrnull_1?keywords=financial+signal+processing+and+machine+learning&qid=1552911044&s=gateway&sr=8-1-fkmrnull), Akansu et al. (2016).
* (book) [Asset Management A Systematic Approach to Factor Investing](https://www.amazon.co.uk/Management-Systematic-Investing-Financial-Association/dp/0199959323/ref=sr_1_fkmrnull_1?crid=LA057841Z0CS&keywords=asset+management+a+systematic+approach+to+factor+investing&qid=1552911140&s=gateway&sprefix=asset+management+a+%2Caps%2C133&sr=8-1-fkmrnull), Ang (2014).
* (book) [Introduction to Risk Parity and Budgeting](https://arxiv.org/pdf/1403.1889.pdf), Roncalli (2013).
* (book) [The Misbehaviour of Markets a Fractal View of Risk, Ruin and Reward](https://www.amazon.co.uk/Mis-Behaviour-Markets-Fractal-Reward/dp/1846682622/ref=sr_1_1?crid=3AWHTN4WAXBMR&keywords=the+misbehaviour+of+markets&qid=1552911932&s=gateway&sprefix=the+misbehaviour%2Caps%2C299&sr=8-1), Mandelbrot (2008).
* (book) [Fooled by Randomness](https://www.amazon.co.uk/Fooled-Randomness-Hidden-Chance-Markets/dp/0141031484/ref=sr_1_1?crid=2K0IMWLWXCVE6&keywords=fooled+by+randomness&qid=1552912223&s=gateway&sprefix=fooled+by+%2Caps%2C132&sr=8-1), Taleb (2007).
* (book) [Red-Blooded Risk: The Secret History of Wall Street](https://www.amazon.co.uk/Red-Blooded-Risk-Secret-History-Street/dp/1118043863/ref=sr_1_1?keywords=red+blooded+risk&qid=1552912282&s=gateway&sr=8-1-spell), Brown (2011).


# Deep Hedging
# RL
* [Reinforcement learning in financial markets - a survey](https://www.econstor.eu/bitstream/10419/183139/1/1032172355.pdf), Fischer (2018).
* [Optimal Asset Allocation Using Adaptive Dynamic Programming](https://papers.nips.cc/paper/1121-optimal-asset-allocation-using-adaptive-dynamic-programming.pdf), Neuneier (1996).
* [Reinforcement Learning for Trading Systems and Portfolios](https://pdfs.semanticscholar.org/10f3/4407d0f7766cfb887334de4ce105d5aa8aae.pdf), Moody et al (1998).
* [PERFORMANCE FUNCTIONS AND REINFORCEMENT LEARNING FOR TRADING SYSTEMS AND PORTFOLIOS](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.87.8437&rep=rep1&type=pdf), Moody et al (1998).
* [Reinforcement Learning for Trading](http://papers.nips.cc/paper/1551-reinforcement-learning-for-trading.pdf), Moody et al. (1999).
* [Learning to trade via direct reinforcement](http://people.idsia.ch/~juergen/rnnaissance2003talks/MoodySaffellTNN01.pdf), Moody (2001).
* [Moody presentation](http://www.cs.cmu.edu/afs/cs/project/link-3/lafferty/www/ml-stat-www/moody.pdf), Moody (2003).
* [Stochastic Direct Reinforcement: Application to Simple Games with Recurrence](https://www.aaai.org/Papers/Symposia/Fall/2004/FS-04-02/FS04-02-004.pdf), Moody et al (2003).
* [Reinforcement Learning for Stochastic Control Problems in Finance](http://web.stanford.edu/class/cme241/), Rao (2018).
* [Deep Hedging](https://arxiv.org/pdf/1802.03042.pdf), BUEHLER et al. (2018).
* [Deep Hedging: Hedging Derivatives Under Generic Market Frictions Using Reinforcement Learning](https://poseidon01.ssrn.com/delivery.php?ID=699064116031077097087112121097105025123011062088031092022073127100022097028123112089013000007026033049005010005121089085004101102026033060067071107028113069028068020022001080013026079071105097107078018096065081067105125014124087106094118127009119065&EXT=pdf), Buehler (2019).
* [Model-Free Option Pricing with Reinforcement Learning](https://cfe.columbia.edu/files/seasieor/industrial-engineering-operations-research/IgorHalperin_Columbia_ML_in_finance_QLBS.pdf), Halperin, (2018).
* [QLBS: Q-Learner in the Black-Scholes(-Merton) Worlds](https://arxiv.org/pdf/1712.04609.pdf), Halperin (2019).
* [Agent Inspired Trading Using Recurrent Reinforcement Learning and LSTM Neural Networks](https://arxiv.org/pdf/1707.07338.pdf), Lu (2017).
* [A reinforcement learning approach for pricing derivatives](http://cs229.stanford.edu/proj2010/Grassl-AReinforcementLearningApproachForPricingDerivatives.pdf), Grassl, (2008).
* [Regime-switching recurrent reinforcement learning for investment decision making](http://doc.rero.ch/record/321803/files/10287_2011_Article_131.pdf), Maringer (2009).
* [Automating Transition Functions: A Way To Improve Trading Profits with Recurrent Reinforcement Learning](https://hal.inria.fr/hal-01391291/document), Zhang (2013).
* [Algorithm trading using q-learning and recurrent
reinforcement learning](http://cs229.stanford.edu/proj2009/LvDuZhai.pdf), Du et al. (2009).
* [RL for Portfolio Management - Thesis](https://arxiv.org/pdf/1909.09571.pdf), Filos (2018).
* [A Deep Reinforcement Learning Framework for the Financial Portfolio Management Problem](https://arxiv.org/pdf/1706.10059.pdf), Jiang (2017).
* [An Automated fx trading system using adaptive reinforcement learning](https://www.jbs.cam.ac.uk/fileadmin/user_upload/research/workingpapers/wp0418.pdf), Dempster (2004).
* [Model-based Deep Reinforcement Learning for Dynamic Portfolio Optimization](https://arxiv.org/pdf/1901.08740.pdf),  Yu et al (2019).
* [Cryptocurrency Portfolio Management with Deep Reinforcement Learning](https://arxiv.org/pdf/1612.01277.pdf), Jiang et al  (2017).
* [An adaptive portfolio trading system: A risk-return portfolio optimization using recurrent reinforcement learning with expected maximum drawdown](https://www.researchgate.net/profile/Steve_Yang2/publication/317622713_An_adaptive_portfolio_trading_system_A_risk-return_portfolio_optimization_using_recurrent_reinforcement_learning_with_expected_maximum_drawdown/links/59f3401da6fdcc075ec339c5/An-adaptive-portfolio-trading-system-A-risk-return-portfolio-optimization-using-recurrent-reinforcement-learning-with-expected-maximum-drawdown.pdf), Almahdi et al (2017).
* [Portfolio Choices with Orthogonal Bandit Learning](http://yugangjiang.info/publication/ijcai15-OBL.pdf), Shen et al. (2015)
* [Risk-Aware Multi-Armed Bandit Problem with Application to Portfolio Selection](https://arxiv.org/pdf/1709.04415.pdf), Huo (2017)
* [Application of stochastic recurrent reinforcement learning to index trading ](http://discovery.ucl.ac.uk/1339314/1/es2011-60%5B1%5D.pdf), Gorse (2011).
* [Testing different Reinforcement Learning configurations
for financial trading: Introduction and applications](https://pdf.sciencedirectassets.com/282136/1-s2.0-S2212567112X00042/1-s2.0-S2212567112001220/main.pdf?X-Amz-Security-Token=AgoJb3JpZ2luX2VjEHgaCXVzLWVhc3QtMSJHMEUCIFM%2Ft60m0FP5zqqIJYury%2BWGUH2qmQJooNgLQMZsU41sAiEAjcntQWo1Un6bJz32BA0IOgft5%2F8aiYaE29fX9c5HUjgq2gMIQRACGgwwNTkwMDM1NDY4NjUiDAD3VLuf0EW314iCdyq3AyqnwrQi6NpoKkOMjur1OfjVlJX%2BwRsgNP2v8QSiPSaY0wkAdUfOZyYDPj4hyWptbwK5O5icJQbYoGfH3mg5K6aQXGbJXFCgENaKsDi0YapzZLwq55oV0pFGQvgGGFMIdZ6GUQXoM0j54vIRo%2FPC60xDCtJfQj1Wxg4kENPoxLHr%2FsqCdmY7GX9EGW3Nj7657izJ8S9Ou0GnkkBwtcwhmse6QKJStftotgmIpuvgQvE%2FpEkstIsTK0opyfeYXSPGVzUVX1khd4aHAUPyLINvbSslekIEcIzL0BDQ5YMv9Zp%2F1AGjJm3n8sZ0mMkyUEwwKUvRfV9JU8I4%2FWnZlY6yUxFS39KEPEBARjlw1QJgIJ8xsmJVHtIUN6GgRSM1r5hwze8ZbV0L0ONySiO3ZXmMQIoaxV1aVWxw0DthRjl2Ds2P391nZxAPiwRNqYyFHslyMiRNz89SNFRoIA03Se3CNL6%2FvWSo6LmKUVLKCOzZnjzUHKgsj%2FaYRHdMx2t0MduKlhbwD3OkUd86ELGN7IiWN30hbNCmL1b0cr2Ei2QaKkqlNwIgyotWqnMNr%2FEeCMrptGdtWjQtGMww4df36wU6tAF7hsVWtgwWf3xeAomhR4eIL9sIStgT9z01xVY9h4jwQF1qIlBhz1bm53rvBnCLn4e5R2zVw12LGbABb1CSSfz780ZmzFy%2BgZXCfPwb%2FTBaKgJXO2%2BAy6kXTyDKXAJsubd4IuJ9DJrIuRosCOexglX5OcLRkUrvGky3oVhnaP6cCZAY0qr4FFM472WvnZW1aRH1MjHgTiDh8Ilm5cf4e7mQNmQbX7eN2%2BsVRlO5P9uxiIR%2BQsY%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20190915T083038Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAQ3PHCVTYQKNDAQHW%2F20190915%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=56b4003379943f5cd332add3aea57da65cf5b322aa73f3a4b2af686bad26fd8b&hash=61129b7967890d1bd6a8195ec8e12cd6cea96bcedc073fe7d3b8f30a13374bba&host=68042c943591013ac2b2430a89b270f6af2c76d8dfd086a07176afe7c76c2c61&pii=S2212567112001220&tid=spdf-07f94ef6-fa11-4ce2-bcf2-3b1999a259f9&sid=8f72a70b45b6524359780172d34111628b2dgxrqa&type=client), Bertolluzo et al, (2012).
* [An Investigation into the Use of Reinforcement Learning Techniques
within the Algorithmic Trading Domain](https://www.doc.ic.ac.uk/teaching/distinguished-projects/2015/j.cumming.pdf), Cumming (2015).
* [Financial Trading as a Game: A Deep Reinforcement Learning Approach](https://arxiv.org/pdf/1807.02787.pdf), Huang (2018).
* [Deep Reinforcement Learning for Foreign Exchange Trading](https://arxiv.org/pdf/1908.08036.pdf), Wang (2019).
* [Capturing Financial markets to apply Deep Reinforcement Learning](https://arxiv.org/pdf/1907.04373.pdf), Chakraborty (2019).
* [Reinforcement Learning For Automated Trading](http://www1.mate.polimi.it/~forma/Didattica/ProgettiPacs/BrambillaNecchi15-16/PACS_Report_Pierpaolo_Necchi.pdf), Necchi  (2016).
* [Towards Inverse Reinforcement Learning for Limit Order Book Dynamics](https://arxiv.org/pdf/1906.04813.pdf), Roa-Vicens et al (2019).
* [Multi-Period Trading via Convex Optimization](https://arxiv.org/pdf/1705.00109.pdf). Boyd et al. (2017).
* [Optimal Execution of Portfolio Transactions](https://www.math.nyu.edu/faculty/chriss/optliq_f.pdf), Chris (1999).
* [Deep Learning Volatility](https://arxiv.org/pdf/1901.09647.pdf), Horvath (2019).
* [Pricing options and computing implied volatilities using neural networks](https://arxiv.org/pdf/1901.08943.pdf), Liu (2019).
* [Machine Learning and Option Implied Information](https://spiral.imperial.ac.uk/bitstream/10044/1/57953/5/Yu-Z-2018-PhD-Thesis.pdf), Zheng (2018).
* [Hedged Monte-Carlo: low variance derivative pricing with objective probabilities](https://arxiv.org/pdf/cond-mat/0008147.pdf), Potter et al. (2000).
* [Dynamic Replication and Hedging: A Reinforcement Learning Approach](https://www.researchgate.net/publication/329435926_Dynamic_Replication_and_Hedging_A_Reinforcement_Learning_Approach), Ritter (2019).
* [Deep learning approach to hedging Thesis](https://www.natixis.com/natixis/upload/docs/application/pdf/2019-10/michal_kozyra_prix_natixis_2019_du_meilleur_memoire_de_master_en_finance_quantitative.pdf), Kozyra (2018).
* [Deep Hedging - Presentation](https://www.maths.ox.ac.uk/system/files/attachments/2019%2004%2024%20Deep%20Hedging%20Frontiers%20Imperial%202.1.pdf), Beuler (2018).
* [Pricing and Hedging Exotic Options with Monte Carlo Simulations](http://citeseerx.ist.psu.edu/viewdoc/download;jsessionid=E50E03046624FEC67933C3D86B01FA71?doi=10.1.1.194.9001&rep=rep1&type=pdf), Perilla Msc (2003).
* [The Four Horsemen of Machine Learning in Finance](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3453564), Halperin (2019).
* [Machine Learning for Trading](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3015609), Ritter (2017).
* [Reinforcement Learning With Continuous States](https://cims.nyu.edu/~ritter/ritter2018sarsa.pdf), Ritter (2018).
* [The Usefulness of Reinforcement Learning in Finance - Pres](https://www.iaqf.org/dev/files/IAQF-2018%20-%20slides.pdf), Ritter (2018).
* [Generative Bayesian neural network model for risk-neutral pricing of American index options](https://www.tandfonline.com/doi/pdf/10.1080/14697688.2018.1490807?needAccess=true), Jang et al. (2018).
* [Reinforcement Learning Applied to Option
Pricing - MSc](https://core.ac.uk/download/pdf/39674013.pdf), Martin (2014).
* [Quant GANs:Deep Generation of Financial Time Series](https://arxiv.org/pdf/1907.06673.pdf), Wiese et al. (2019).
* [Enhancing Time Series Momentum Strategies Using Deep Neural Networks](https://arxiv.org/pdf/1904.04912.pdf), Lim et al. (2019).
* [Deep Learning Approximation for Stochastic Control Problems](https://www.researchgate.net/publication/310672039_Deep_Learning_Approximation_for_Stochastic_Control_Problems/link/5a37c5a3aca272a6ec1e4fd1/download) Han et al. (2016).
* [Deep Reinforcement Learning for Trading](https://arxiv.org/pdf/1911.10107.pdf), Zhang (2019).
* [Model-based Reinforcement Learning for Predictions and Control for Limit Order Books](https://arxiv.org/pdf/1910.03743.pdf), Wei et al. (2019). 
* [Topics in Dynamic Portfolio Choice Problems -PhD Thesis](https://escholarship.org/content/qt9fc8j8rz/qt9fc8j8rz.pdf), Wimonkittiwat, (2013)
* [Reinforcement-Learning based Portfolio Management with Augmented Asset Movement Prediction States](https://arxiv.org/pdf/2002.05780.pdf), Ye et al. (2020).

# Machine-Learning-Asset-Allocation

# DL Online and Bandits

* [Reinforcement Learning for Stochastic Control Problems in Finance](http://web.stanford.edu/class/cme241/), Rao (2018).
* [Deep Learning in Finance](https://arxiv.org/abs/1602.06561), Heaton et al. (2015).
* [Deep Portfolio Theory](https://arxiv.org/abs/1605.07230), Heaton et al. (2016).
* [Deep Learning in Asset Pricing](https://arxiv.org/abs/1805.01104), Feng et al. (2018).
* [Adaptive Portfolio Asset Allocation Optimization with Deep Learning](http://www.thinkmind.org/download.php?articleid=intsys_v11_n12_2018_3) Obeidat et al. (2018).
* [Portfolio Optimisation in an Uncertain world](https://www.northinfo.com/documents/740.pdf), de Jong (2017).
* [Empirical Asset Pricing via Machine Learning](https://poseidon01.ssrn.com/delivery.php?ID=856093125087082084016102091092007100060006063087051074127084028094112096004004064108038021018041122035062067123102100071094080049045093023049072118096000064081103084062051035088126094099100013006118027020024030000097122082084074011113081006075109085069&EXT=pdf), Kelly et al (2018).
* [Real-valued (Medical) Time Series Generation with Recurrent Conditional GANs](https://arxiv.org/abs/1706.02633), Estaban (2017).
* [Portfolio Choices with Orthogonal Bandit Learning](http://yugangjiang.info/publication/ijcai15-OBL.pdf), Shen et al. (2015)
* [Risk-Aware Multi-Armed Bandit Problem with Application to Portfolio Selection](https://arxiv.org/pdf/1709.04415.pdf), Huo (2017)
* [Structured Online Learning with Full and Bandit Information](https://conservancy.umn.edu/bitstream/handle/11299/183364/Johnson_umn_0130E_17619.pdf?sequence=1&isAllowed=y), Johnson PhD Thesis (2016).
* [Censored exploration and the dark pool problem](https://www.cis.upenn.edu/~mkearns/papers/darkpools-final.pdf), Ganchev et al. (2010).
* [Adaptive Execution:Exploration and Learning of Price Impact](https://arxiv.org/pdf/1207.6423.pdf), Park et al (2012).
* [Online Portfolio Selection: A Survey](https://arxiv.org/pdf/1212.2129.pdf), Li et al (2013).
* [Conditional time series forecasting with convolutional neural networks](https://arxiv.org/pdf/1703.04691.pdf),  Borovykh et al (2018).
* [PAGAN: Portfolio Analysis with Generative Adversarial Networks](https://arxiv.org/pdf/1909.10578.pdf), Mariani et al (2019).
* [A Survey of Inverse Reinforcement Learning: Challenges, Methods and Progress](https://arxiv.org/pdf/1806.06877.pdf), Arora (2019).
* [Algorithms for inverse reinforcement learning](https://ai.stanford.edu/~ang/papers/icml00-irl.pdf), Ng at al. (2000).
* [An Empirical Comparison of Machine Learning Models for Time Series Forecasting](https://www.researchgate.net/publication/227612766_An_Empirical_Comparison_of_Machine_Learning_Models_for_Time_Series_Forecasting), Ahmed et al. (2010).
* [A Signal Processing Perspective on Financial Engineering](https://palomar.home.ece.ust.hk/papers/2016/Feng&Palomar-FnT2016.pdf)
, Feng et al. (2017).
* [Fourier Policy Gradients](https://arxiv.org/pdf/1802.06891.pdf), Fellows et al. (2018).
* [Expected Policy Gradients](http://www.ciosek.net/dwnl/ciosek-whiteson-epg.pdf), Kiosek et al. (2018).


# Classic Portfolio Selection Materials
* [Portfolio Selection](https://www.math.ust.hk/~maykwok/courses/ma362/07F/markowitz_JF.pdf), Markowitz (1952).
* [Capital Asset Prices: A Theory of Market Equilibrium under Conditions of Risk](https://psc.ky.gov/pscecf/2012-00221/rateintervention@ag.ky.gov/10252012f/sharpe_-_CAPM.pdf), Sharpe (1964).
* [The Arbitrage Theory and Capital Asset Pricing](https://www.top1000funds.com/wp-content/uploads/2014/05/The-Arbitrage-Theory-of-Capital-Asset-Pricing.pdf), Ross (1976).
* [Continuous Time Finance](https://www.amazon.co.uk/Continuous-Time-Finance-Macroeconomics-Robert-Merton/dp/0631185089/ref=sr_1_1?keywords=continuous+time+finance&qid=1552911190&s=gateway&sr=8-1), Merton (1992).
* [Hot Spots and Hedges](https://search.proquest.com/openview/bb7a5042a966f7e5415aca3521f74718/1?pq-origsite=gscholar&cbl=49137), Litterman (1996).
* [Global Portfolio Optimisation](http://www.sef.hku.hk/tpg/econ6017/2011/black-litterman-1992.pdf) Black, Litterman (1992).
* [On the Inverse of the Covariance Matrix in Portfolio Analysis](https://www.federalreserve.gov/pubs/ifdp/1995/528/ifdp528.pdf), Stevens (1998).
* [Improved Estimation of the Covariance Matrix of Stock Returns With an Application to Portfolio Selection](http://www.ledoit.net/ole2.pdf), Le Doit et al. (2001).
* [Portfolio Constraints and the Fundamental Law of Active Management](https://faculty.fuqua.duke.edu/~charvey/Teaching/BA491_2005/Transfer_coefficient.pdf), Clarke et al. (2002).
* [Optimal Versus Naive Diversification:How Inefficient is the 1/N Portfolio Strategy](http://faculty.london.edu/avmiguel/DeMiguel-Garlappi-Uppal-RFS.pdf), DeMiguel et al. (2009).
* [Enhancing mean-variance portfolio selection by modeling distributional asymmetries](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2259073) Kwong Yee Low et al. (2015).
* [Risk management under Omega measure](https://arxiv.org/abs/1510.05790), Metel et al. (2015). 
* [From Portfolio Optimisation to Risk Parity](http://www.thierry-roncalli.com/download/engref-risk-parity.pdf) Roncalli (2012).
* [Risk Parity Portfolios with Risk Factors](http://www.thierry-roncalli.com/download/risk-factor-parity.pdf), Roncalli (2014).
* [Introducing Expected Returns into Risk Parity](http://www.thierry-roncalli.com/download/active-risk-parity.pdf), Roncalli (2014).
* [Why Indexing works](https://arxiv.org/abs/1510.03550), Heaton (2015).
* [Noise Dressing of Financial Correlation Matrices](https://arxiv.org/pdf/cond-mat/9810255.pdf), Laloux (1998).
* [Random Matrix Theory and Cross-correlations in Global Financial Indices and Local Stock Market Indices](https://arxiv.org/pdf/1302.6305.pdf), Nobi (2013).
* [Analysis of cross-correlations between financial markets after the 2008 crisis](http://yoksis.bilkent.edu.tr/pdf/files/13413.pdf), Sensoy (2013).
* [Financial Applications of Random Matrix Theory: a short review](https://arxiv.org/abs/0910.1205), Bouchard et al. (2009).
* [Do High-Frequency Data Improve High-DimensionalPortfolio Allocations](https://poseidon01.ssrn.com/delivery.php?ID=386104017119025100081065083026091007006004057060022070075030124112069093092004111119107060037031026002028123067090074086088099118014013047021116115069116015095096119050069001083095111115117076123083099120117113031123030121029097099116095104012008113006&EXT=pdf), Hautsche (2013).
* [Shrinking the Cross Section](https://poseidon01.ssrn.com/delivery.php?ID=694020101096117116121029071112113121063069052046032018081091009105097031092075066125020120023035008127018120007125126125122084111073005045021069008000120072123082001007035067024100004085124013126031089018025091082089012071104102015113109087114097026072&EXT=pdf), Kozak (2018)
* [Random Matrix Theory](https://web.eecs.umich.edu/~rajnrao/Acta05rmt.pdf), Edelman (2005).
* [Characteristics are Covariances](https://poseidon01.ssrn.com/delivery.php?ID=004020091089127113024084007093003075120015077012021005105005102113075120101113111030041107053119007034112080093107127066026013053026022082043006065000112066079100090015042078012127115093018075121098097107013110121110090010070123013109119013082097017&EXT=pdf), Kelly et al (2018).
* [Arbitrage Portfolios](https://poseidon01.ssrn.com/delivery.php?ID=155119021069074117123119117013104011000056041004079034011123115091083114025090014106005026024030117063044089108090072087024020029059043064055127086115066104116047089039064103023126113093101006064113101085014022107098118105020114005026086104122094&EXT=pdf), Kim (2019).
* [Estimating Latent Asset Pricing Factors](https://poseidon01.ssrn.com/delivery.php?ID=961082017006096116115106083103105127056008077033052025098098127104083074073002078064102023115106011025018102004113100030079121000073035049088096081004027075097097084071081037089088072000067091086014069095117021105093099066118119119074110026069065121121&EXT=pdf), Lettau (2018).
* [Dissecting Characteristics Nonparametrically](http://faculty.chicagobooth.edu/michael.weber/research/pdf/nonparametrics.pdf), Freyberger (2019).
* [Dynamics of competition between collectivity and noise in the stock market](https://arxiv.org/abs/cond-mat/9911168), Drozdz (2018).
* [Markowitz Revisited: Single-Period and Multi-Period Mean-Variance Models](https://opus4.kobv.de/opus4-zib/frontdoor/deliver/index/docId/418/file/SC-99-30.pdf), Steinback (1999).
* [Sparse and Stable Markowitz Portfolios](https://www.ecb.europa.eu/pub/pdf/scpwps/ecbwp936.pdf), De Moi et al.
* [Portfolio Choice Problems](https://faculty.fuqua.duke.edu/~mbrandt/papers/published/portreview.pdf), Brandt
* [Variable Selection for Portfolio Choice](https://www.princeton.edu/~yacine/varselect.pdf), Ait-Sahalia and Brandt (2001).
* [Parametric Portfolio Policies:Exploiting Characteristics in the Cross-Section of Equity Returns](https://www.nber.org/papers/w10996.pdf), Brandt (2004).
* [Dynamic Portfolio Selection by Augmenting the Asset Space](https://www.nber.org/papers/w10372.pdf), Brandt and Santa Clara (2004).
* [Testing Portfolio Efficiency with Conditioning Information](https://www.marshall.usc.edu/sites/default/files/ferson/intellcont/TESTS%20Ferson%20Siegel-1.pdf), Ferson and Siegel (2007).


# Machine Learning based Portfolio Selection

* [Sparse and Stable Markowitz Portfolios](https://www.ecb.europa.eu/pub/pdf/scpwps/ecbwp936.pdf), Brodie et al. (2009).
* [A generalised approach to Portfolio Optimisation](https://pdfs.semanticscholar.org/e1d6/d5b5ea4ee63c7687721990cb301788812a7f.pdf?_ga=2.109794565.1679363491.1552914144-582257270.1544270264), DeMiguel (2009).
* [Optimal Portfolio Selection using regularisation](https://www.researchgate.net/publication/267400011_Optimal_Portfolio_Selection_using_Regularization), Carrasco et al. (2012).
* [Lp Regularised Portfolio Optimisation](https://arxiv.org/pdf/1404.4040.pdf), Caccioli et al. (2014).
* [Bayesian Regularisation from Tikhonov to Horsehoe](https://arxiv.org/abs/1902.06269), Polson (2019).
* [Construction, management, and performance of sparse Markowitz portfolios](https://poseidon01.ssrn.com/delivery.php?ID=019121024026085009092118080105125111054025070085022092087021080091122074023066029075114117055044051060015072084099001091089125016084042033015116108108081006022123104019077079093091097119123000127109116006110078120029123094014074119106125074005004073127&EXT=pdf), Henriques et al. (2014).
* [Portfolio Selection using Tikhonov Filtering to estimate the Covariance Matrix](https://www.cs.umd.edu/sites/default/files/scholarly_papers/Sungwoo%2520Park_Scholarly%2520Paper_1.pdf), Park (2010).
* [Sparse recovery under Matrix Uncertainty](https://arxiv.org/abs/0812.2818), Rosenbaum (2008).
* [Financial Applications of Gaussian Processes and Bayesian Optimization](https://arxiv.org/pdf/1903.04841.pdf), Gonzales et al. (2019).
* [Applications of Gaussian Processes in Finance](https://openreview.net/pdf?id=ryEquiR9KX), Anonymous under review (2019).
* [Portfolio Optimisation Models](https://bura.brunel.ac.uk/bitstream/2438/10343/1/FulltextThesis.pdf), Valle PhD Thesis (2013).
* [Optimal Financial Portfolio Selection](https://georgederpa.github.io/research/MSthesis_GD.pdf), Derpanopoulos, (2018).
* [Markowitz Minimum Variance Portfolio Optimization using New Machine Learning Methods](http://discovery.ucl.ac.uk/1474136/1/PhDThesis_ToyinAwoye.pdf), Awoye PhD Thesis (2016).
* [Sparse Portfolio Selection via the sorted L1 norm](https://arxiv.org/pdf/1710.02435.pdf), Kremer et al. (2017).
* [Machine Learning and Portfolio Optimization](http://www.optimization-online.org/DB_FILE/2014/11/4625.pdf), Ban et al (2016).
* [Reducing Estimation Risk in Mean-Variance Portfolios with Machine Learning](https://arxiv.org/abs/1804.01764), Kinn (2018).
* [Building Diversified Portfolios that outperform out of sample](https://poseidon01.ssrn.com/delivery.php?ID=410125074122122069104121102002097106032052042041037011126100091027097122025125095029007042096016033108114103082098099082100064116002063019007088113078122014076024039013045127086119095114086095070001002024107085104088003079100020028076092095119090098&EXT=pdf), DeLopez (2016).
* [A Constrained Hierarchical Risk Parity Algorithm with Cluster-based Capital Allocation](https://finmx.nfkatzke.com/Projects/HRP.pdf), Pfitzinger et al. (2017).
* [Hierarchical Clustering based Asset Allocation](https://poseidon01.ssrn.com/delivery.php?ID=035082020017064121030104030102079073062005049007084090076020123111094072090085106072053057049122058038019123010086069029102066016009043022084022125117092083127118091032009009065113072100113116107119022114019072016029004070015025084006107110125071000017&EXT=pdf), Raffinot (2017).
* [Portfolio Selection via Subset Resampling](https://www.aaai.org/ocs/index.php/AAAI/AAAI17/paper/download/14443/13945), Shen (2017).
* [Kernel Principal Component Analysis and Random Matrix Theory in Portfolio Selection](https://editorialexpress.com/cgi-bin/conference/download.cgi?db_name=XVIIIEBFin&paper_id=106), Peng et al (2017).
* [Asset Allocation in Finance:  A Bayesian Perspective](http://faculty.chicagobooth.edu/nicholas.polson/research/papers/Asset.pdf), Jacquier et al (2011).
* [Estimation of Covariance Matrices for Portfolio Optimization using Gaussian Processes](https://arxiv.org/abs/1806.03294), Nirwan et al. (2018).
* [Bayesian mean-variance analysis: Optimal portfolio selection under parameter uncertainty](https://arxiv.org/abs/1803.03573), Bauder (2018).
* [Asset Allocation, Economic Cycles and Machine Learning](https://tel.archives-ouvertes.fr/tel-01872176/document),Raffinot PhD Thesis (2018).

# Canonical Correlation Analysis
* [Comparison of Penalty Functions for Sparse Canonical Correlation Analysis](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3185379/pdf/nihms316504.pdf), Chalise et al. (2012).
* [Comparison of Canonical Variate Analysis and Principal Component
Analysis on 422 descriptive sensory studies](https://www.dropbox.com/home/CCA%20References?preview=1-s2.0-S0950329314000871-main.pdf), Peltier et al. (2014).
* [Enhancing canonical variate analysis by taking the scaling effect into account](https://www.dropbox.com/home/CCA%20References?preview=1-s2.0-S0950329317302586-main.pdf), Peltier et al. (2017).
* [Comparison of variants of canonical correlation analysis and partial least squares for combined analysis of MRI and genetic data](https://www.dropbox.com/home/CCA%20References?preview=1-s2.0-S1053811914010179-main+2.pdf), Grellmann et al. (2014).
* [Multiway canonical correlation analysis of brain data](https://www.dropbox.com/home/CCA%20References?preview=1-s2.0-S1053811918321049-main.pdf), Chevaigne et al. (2018).
* [Kernel Canonical Variate Analysis for Nonlinear Dynamic Process Monitoring](https://www.dropbox.com/home/CCA%20References?preview=1-s2.0-S2405896315011155-main.pdf), Samuel et al. (2015).
* [A Least Squares Formulation for Canonical Correlation Analysis](https://www.dropbox.com/home/CCA%20References?preview=5c97d647181ea1079be3638133f8835f8f50.pdf), Ji et al. 
* [Inference for Robust Canonical Variate Analysis](https://www.dropbox.com/home/CCA%20References?preview=9feabf56d26517c6f2c80f02ebcaeb92d091.pdf), Aest et al. 
* [Correlation Analysis 1](https://www.dropbox.com/home/CCA%20References?preview=10-cor1.pdf), Tibshirani, (2013).
* [Correlation Analysis 2](https://www.dropbox.com/home/CCA%20References?preview=11-cor2.pdf), Tibshirani, (2013).
* [Optimisation of Trading Strategies using Parameterised Decision Rules](https://www.dropbox.com/home/CCA%20References?preview=10.1.1.41.8166.pdf), Towers et al. (1998).
* [On the Equivalence Between Canonical Correlation Analysis and Orthonormalized Partial Least Squares](https://www.dropbox.com/home/CCA%20References?preview=207.pdf), Sun et al.
* [A Least Squares Formulation for Canonical Correlation Analysis](https://www.dropbox.com/home/CCA%20References?preview=270CCA+by+LS.pdf), Sun et al. 
* [A Probabilistic Interpretation of Canonical Correlation Analysis](https://www.dropbox.com/home/CCA%20References?preview=688.pdf), Bach et al. (2005).
* [Moments and Absolute Moments of the Normal Distribution](https://www.dropbox.com/home/CCA%20References?preview=1209.4340.pdf), Winkelbauer, (2014).
* [Large Scale Canonical Correlation Analysis with Iterative Least Squares](https://www.dropbox.com/home/CCA%20References?preview=1407.4508.pdf), Lu, (2014).
* [Sparse canonical correlation analysis from a predictive point of view](https://www.dropbox.com/home/CCA%20References?preview=1501.01231.pdf), Wilms et al. (2015).
* [Variational Analysis of the Ky Fan k-norm](https://www.dropbox.com/home/CCA%20References?preview=1601.07430.pdf), Ding, (2015).
* [Canonical correlation analysis of high-dimensional data with very small sample support](https://www.dropbox.com/home/CCA%20References?preview=1604.02047.pdf), Song, (2016).
* [FDR-Corrected Sparse Canonical Correlation Analysis with Applications to Imaging Genomics](https://www.dropbox.com/home/CCA%20References?preview=1705.04312.pdf), Gossman, (2018).
* [Acoustic Feature Learning via Deep Variational Canonical Correlation Analysis](https://www.dropbox.com/home/CCA%20References?preview=1708.04673.pdf), Tang et al. (2018).
* [A Tutorial on Canonical Correlation Methods](https://www.dropbox.com/home/CCA%20References?preview=1711.02391+tutorial+CCA.pdf), Uurtio et al. (2018).
* [Change Point Analysis of Correlation in Non-stationary Time Series](https://www.dropbox.com/home/CCA%20References?preview=1801.10478+2.pdf), Dette, (2018).
* [Pricing without martingale measure](https://www.dropbox.com/home/CCA%20References?preview=1807.04612.pdf), Batiste, (2018).
* [Canonical Analysis, A review with applications in Ecology](https://www.dropbox.com/home/CCA%20References?preview=1986_Article_CanonicalAnalysisAReviewWithAp.pdf), Gittins ,(1986).
* [The Estimation of Prediction Error: Covariance Penalties and Cross-Validation](https://www.dropbox.com/home/CCA%20References?preview=2004PredictionErrorRev_May.pdf), Efron.
* [On the Moreau-Yosida regularization of the vector k-norm related functions](https://www.dropbox.com/home/CCA%20References?preview=2978.pdf), Wu et al. (2011).
* [Gen-Oja: A Simple and Efficient Algorithm for Streaming Generalized Eigenvector Computation](https://www.dropbox.com/home/CCA%20References?preview=7933-gen-oja-simple-efficient-algorithm-for-streaming-generalized-eigenvector-computation.pdf), Bhatia et al. (2018).
* [Robust sparse canonical correlation analysis](https://www.dropbox.com/home/CCA%20References?preview=12918_2016_Article_317.pdf), Wilms et al. (2016).
* [The Geometry of Canonical Variant Analysis](https://www.dropbox.com/home/CCA%20References?preview=2413249.pdf), Campbell et al. (1981).
* [Estimation and Hypothesis Testing of Cointegration Vectors in Gaussian Vector Autoregressive Models](https://www.dropbox.com/home/CCA%20References?preview=2938278.pdf), Johannsen, (1991).
* [Sufficient Canonical Correlation Analysis](https://www.dropbox.com/home/CCA%20References?preview=07448411.pdf), Guo et al. (2016).
* [Some properties of canonical correlations and variates in infinite dimensions](https://www.dropbox.com/home/CCA%20References?preview=82529111+2.pdf), Cupidon et al. (2007).
* [High Dimensional Asymptotic expansions for the distributions of canonical correlations](https://www.dropbox.com/home/CCA%20References?preview=82813427.pdf), Fujikoshi el al. (2008).
* [A Canonical Correlation Analysis of Intelligence and Executive Functioning](https://www.dropbox.com/home/CCA%20References?preview=A+Canonical+Correlation+Analysis+of+Intelligence+and+Executive+Functioning.pdf), Davis et al. (2011).
* [A Closed Testing Procedure for Canonical Correlations](https://www.dropbox.com/home/CCA%20References?preview=A+Closed+Testing+Procedure+for+Canonical+Correlations.pdf), Calinski et al. (2006).
* [A Comparison of Some Tests for Determining the Number of Nonzero Canonical Correlations](https://www.dropbox.com/home/CCA%20References?preview=A+Comparison+of+Some+Tests+for+Determining+the+Number+of+Nonzero+Canonical+Correlations.pdf), Calinski et al. (2006).
* [A New Perspective On Sequential Testing Procedures In Canonical Analysis: A Monte Carlo Evaluation](https://www.dropbox.com/home/CCA%20References?preview=A+New+Perspective+On+Sequential+Testing+Procedures+In+Canonical+Analysis+A+Monte+Carlo+Evaluation.pdf), Mendoza et al. (1978).
* [A modification of canonical variates analysis to handle highly collinear multivariate data](https://www.dropbox.com/home/CCA%20References?preview=A_modification_of_canonical_variates_ana+-+repaired.pdf), Norgaard et al. (2006).
* [Consistency of log-likelihood-based information criteria for selecting variables in high-dimensional canonical correlation analysis under nonnormality](https://www.dropbox.com/home/CCA%20References?preview=AA1540025003.pdf), Fukui, (2015).
* [An analysis of the total least squares problem](https://www.dropbox.com/home/CCA%20References?preview=Analysis.total.least.squares.prob.pdf), Golub, (1980).
* [Bayesian Canonical Correlation Analysis](https://www.dropbox.com/home/CCA%20References?preview=Bayes+CCA.pdf), Klami et al. (2013).
* [Canonical Variate Analysis and Related Methods with Longitudinal Data](https://www.dropbox.com/home/CCA%20References?preview=beaghenthesis.pdf), Beaghan PhD thesis (1997).
* [Dynamic Portfolio Selection by Augmenting the Asset Space](https://www.dropbox.com/home/CCA%20References?preview=brandt_santaclara_dynamic_portfolio_jf.pdf), Brandt, (2006).
* [Canonical Correlation Clarified by Singular Value Decomposition](https://www.dropbox.com/home/CCA%20References?preview=CanonCorrBySVD.pdf), Press, (2011).
* [Chapter 8, Multivariate Data Analysis](https://www.dropbox.com/home/CCA%20References?preview=Canonical_Correlation_6e+2.pdf), Anderson et al. (1998).
* [Multivariate Data Analysis](https://www.dropbox.com/home/CCA%20References?preview=canonical_correlation_7e.pdf), Anderson et al. (1998).
* [NCSS Stat software explanation](https://www.dropbox.com/home/CCA%20References?preview=Canonical_Correlation.pdf)
* [Canonical Correlation Analysis](https://www.dropbox.com/home/CCA%20References?preview=canonicalcorrelationanalysis.pdf), Weenink, (2003).
* [CCA for Optimal Signal Combination in Algorithmic Trading](https://www.dropbox.com/home/CCA%20References?preview=CCA_plus_notes.pdf), Firoozye, (2019).
* [Canonical Correlation: A Tutorial](https://www.dropbox.com/home/CCA%20References?preview=CCA_tutorial.pdf), Borga, (2001).
* [Convex Estimation of Cointegrated VAR Models by a Nuclear Norm Penalty](https://www.dropbox.com/home/CCA%20References?preview=Cointegration+Nuclear+Penalty.pdf), Signoretto et al. (2012).
* [A modified information Criterion for Cointegration Tests based on a VAR approximation](https://www.dropbox.com/home/CCA%20References?preview=CointRankCriterion.pdf), Qu et al. (2007).
* [Convergence analysis of kernel Canonical Correlation Analysis: Theory and practice](https://www.dropbox.com/home/CCA%20References?preview=convergence-analysis-of-kernel-canonical-correlation-analysis-theory-and-practice.pdf), Hardoon et al. (2009).
* [Canonical Variates Analysis - ch 5 book extract](https://www.dropbox.com/home/CCA%20References?preview=CTS_Chapter5_4_Students.pdf)
* [Extreme Canonical Correlations and high dimensional cointegration analysis](https://www.dropbox.com/home/CCA%20References?preview=cwpe1805.pdf), Onatski et al. (2018).
* [DynOpt: Incorporating Dynamics into Mean-Variance Portfolio Optimization](https://www.dropbox.com/home/CCA%20References?preview=DynamicMeanVarPenalty.pdf), Signoretto.
* [The efficient use of conditioning information in Portfolios](https://www.dropbox.com/home/CCA%20References?preview=effic.pdf), Ferson et al. (2001).
* [Correlations and canonical forms of bivariate distributions](https://www.dropbox.com/home/CCA%20References?preview=euclid.aoms.1177704165.pdf), Lancaster, (1962).
* [Convex optimization methods for dimension reduction and coefficient estimation in multivariate linear regression](https://www.dropbox.com/home/CCA%20References?preview=fesalg.final.pdf), Lu et al. (2008).
* [Statistical Consistency of Kernel Canonical Correlation Analysis](https://www.dropbox.com/home/CCA%20References?preview=fukumizu07a.pdf), Fukumizu et al. (2007).
* [Generalized canonical analysis based on optimizing matrix correlations and a relation with IDIOSCAL](https://www.dropbox.com/home/CCA%20References?preview=Generalized_canonical_analysis_based_on.pdf), Kiers et al. (1991).
* [Determination of vector error correction models in
high dimensions](https://www.dropbox.com/home/CCA%20References?preview=High+Dim+VEC.pdf), Liang et al. (2019).
* [Partial Sparse Canonical Correlation Analysis (PSCCA) for Population Studies in Medical Imagine](https://www.dropbox.com/home/CCA%20References?preview=isbi_cca.pdf), Dhillon et al.
* [The Convex Algebraic Geometry of rank minimization](https://www.dropbox.com/home/CCA%20References?preview=ISMP2009.pdf), Parrilo, (2009).
* [Fitting method based on correlation maximization: Applications in space physics](https://www.dropbox.com/home/CCA%20References?preview=jgra.50304.pdf), Livadiotis et al. (2012).
* [Kernel Canonical Correlation Analysis](https://www.dropbox.com/home/CCA%20References?preview=kCCA.pdf), Welling.
* [Controlling Singular Values with Semidefinite Programming](https://www.dropbox.com/home/CCA%20References?preview=kovalsky_et_al_-_controlling_singular_values_with_semidefinite_programming.pdf), Kovalsky et al. (2014).
* [Lecture 7: Analysis of Factors and Canonical Correlations](https://www.dropbox.com/home/CCA%20References?preview=L7.pdf), Thulin.
* [Guaranteed Minimum-Rank Solutions of Linear Matrix Equations via Nuclear Norm Minimization](https://www.dropbox.com/home/CCA%20References?preview=LowRankMatDecompNukeNorm.pdf), Recht et al. (2008).
* [L1-Regularized Multiway Canonical Correlation Analysis for SSVEP-based BCI](https://www.dropbox.com/home/CCA%20References?preview=mafiadoc.com_l1-regularized-multiway-canonical-correlation-_5b450b2d097c47cf588b45ff.pdf), Zhang et al. (2013).
* [Canonical Correlation Analysis - ETFs](https://www.dropbox.com/home/CCA%20References?preview=Malacarne.pdf), Mathematica journal.
* [Stochastic PCA with L1 and L2 Regularization](https://www.dropbox.com/home/CCA%20References?preview=mianjy18a+2.pdf), Mianji (2018).
* [Stochastic PCA with L1 and L2 Regularization - supplement](https://www.dropbox.com/home/CCA%20References?preview=mianjy18a-supp.pdf), Mianji (2018).
* [Iterative Reweighted Algorithms for Matrix Rank Minimization](https://www.dropbox.com/home/CCA%20References?preview=MohanFazel-11.pdf), Mohan et al. 
* [A Rank Minimization Heuristic with Application to Minimum Order System Approximation](https://www.dropbox.com/home/CCA%20References?preview=nucnorm_acc_final+2.pdf), Fazel et al.
* [Ridge-Penalty Regularization for Kernel-CCA](https://www.dropbox.com/home/CCA%20References?preview=PubDat_119607+2.pdf), Rieter et al.
* [Canonical Correlation Forests](https://www.dropbox.com/home/CCA%20References?preview=rainforth2015canonical.pdf), Rainforth, (2015).
* [Constrained Singular Value Decomposition](https://www.dropbox.com/home/CCA%20References?preview=report_sep23.pdf), Zollman et al. (2009).
* [Large-Scale Convex Minimization with a Low-Rank Constraint](https://www.dropbox.com/home/CCA%20References?preview=ShalevGoSh11.pdf), Shalev-Schwartz et al. (2011).
* [Sparse Canonical Correlation Analysis: New Formulation and Algorithm](https://www.dropbox.com/home/CCA%20References?preview=SparseCCA_TPAMI_Final.pdf), Chu et al.
* [Sparse CCA via Precision Adjusted Iterative Thresholding](https://www.dropbox.com/home/CCA%20References?preview=sparseCCA.pdf), Choi et al. (2017).
* [Generalised Canonical Regression](https://www.dropbox.com/home/CCA%20References?preview=sr288.pdf), Estrella, (2007).
* [Statistics Methods and Applications - Book](https://www.dropbox.com/home/CCA%20References?preview=Statistics_Methods_and_Applications.pdf), Lewicki.
* [Structured Sparse Canonical Correlation Analysis](https://www.dropbox.com/home/CCA%20References?preview=StructuredSparseCanonicalCorrelationAnalysisAISTATS2012.pdf), Chen et al. (2012).
* [A singular value thresholding algorithm for matrix completion](https://www.dropbox.com/home/CCA%20References?preview=SVT.pdf), Cai et al. 
* [The Geometry Of Kernel Canonical Correlation Analysis](https://www.dropbox.com/home/CCA%20References?preview=upload_22685_TR-108.pdf),Kuss et al. (2003).
* [Variants of Canonical Correlation Analysis](https://www.dropbox.com/home/CCA%20References?preview=varCCA.pdf), Choi (2016).
* [Variable selection and interpretation in canonical correlation analysis](https://www.dropbox.com/home/CCA%20References?preview=variable-selection-and-interpretation-in-canonical-correlation-analysis.pdf), Al-Khandari (1997).
* [On the Variance, Reliability and Importance of Canonical Variates](https://www.dropbox.com/home/CCA%20References?preview=yujorn14p267-284.pdf), Momirovic.
* [The asymptotic distribution of canonical correlations and variates in cointegrated models](https://www.dropbox.com/home/CCA%20References/CCA2?preview=2000_AsymptoticDist.pdf), Anderson (2000).
* [Canonical correlation analysis based on sparse penalty and through rank-1 matrix approximation](https://www.dropbox.com/home/CCA%20References/CCA2?preview=52838511.pdf), El Bey et al. (2015).
* [Canonical Correlation Analysis - Slides](https://www.dropbox.com/home/CCA%20References/CCA2?preview=CanonicalCorrelation.pdf), Stieiger.
* [Comparison of Penalty Functions for Sparse Canonical Correlation Analysis](https://www.dropbox.com/home/CCA%20References/CCA2?preview=nihms316504.pdf), Chalise et al. (2012).
* [Use of Smoothly Clipped Absolute Deviation (SCAD) Penalty on Sparse Canonical Correlation Analysis](https://www.dropbox.com/home/CCA%20References/CCA2?preview=SCAD_Documentation.pdf), Very short paper, some R.
* [Developing Long/Short ETF Strategies - CCA](http://jonathankinlay.com/2018/10/developing-etf-longshort-strategies/), Kinlay.
* [Identifying Small Mean Reverting Portfolios](https://www.di.ens.fr/~aspremon/PDF/MeanRevVec.pdf), Aspremont (2008).
* [Sparse Canonical Correlation Analysis](https://link.springer.com/content/pdf/10.1007/s10994-010-5222-7.pdf), Hardoon (2010).
* [A kernel method for canonical correlation analysis](https://arxiv.org/pdf/cs/0609071.pdf), Akaho, (2007).
* [Avoiding Backtesting Overfitting by Covariance-Penalties: An Empirical Investigation of the Ordinary and Total Least Squares cases](https://www.researchgate.net/profile/Nick_Firoozye/publication/332974078_AVOIDING_BACKTESTING_OVERFITTING_BY_COVARIANCE-PENALTIES_AN_EMPIRICAL_INVESTIGATION_OF_THE_ORDINARY_AND_TOTAL_LEAST_SQUARES_CASES/links/5cd4807f299bf14d958590b3/AVOIDING-BACKTESTING-OVERFITTING-BY-COVARIANCE-PENALTIES-AN-EMPIRICAL-INVESTIGATION-OF-THE-ORDINARY-AND-TOTAL-LEAST-SQUARES-CASES.pdf?origin=publication_detail),Koshiyama et al. (2019).
* [Deep Canonical Correlation Analysis](https://ttic.uchicago.edu/~klivescu/papers/andrew_icml2013.pdf), Andrew et al. (2013).
* [Deep Generalized Canonical Correlation Analysis](https://arxiv.org/pdf/1702.02519.pdf), Benton et al. (2017).
* [Multiview Canonical Correlation Analysis](https://pdfs.semanticscholar.org/94fd/74be648857ae6355b99528b48b6085505df5.pdf), Rupnik (2016).
* [Multiview Canonical Correlation Analysis - Phd Thesis](http://slais.ijs.si/theses/2016-06-17-Rupnik.pdf), Rupnik (2016).
* [Generative Adversarial Networks for FinancialTrading Strategies Fine-Tuning and Combination](https://arxiv.org/pdf/1901.01751.pdf), Koshiyama (2019).
* [Temporal Kernel CCA and its Application in MultimodalNeuronal Data Analysis](http://www.cs.cmu.edu/~arthurg/papers/tkCCA.pdf), Bierman et al. (2009)

# Sample Efficient

* [Compressed Conditional Mean Embeddings for Model-Based Reinforcement Learning](https://www.semanticscholar.org/paper/Compressed-Conditional-Mean-Embeddings-for-Learning-Lever-Shawe-Taylor/5ddd28f0370aa8d2a322a329b1373344aaea9ace), Lever et al. (2016).
* [ACCME: Actively Compressed Conditional Mean Embeddings for Model-Based Reinforcement Learning](https://ewrl.files.wordpress.com/2018/09/ewrl_14_2018_paper_47.pdf), Stafford et al. (2018).
* [Kernel Mean Embedding of Distributions: A Review and Beyond](https://arxiv.org/abs/1605.09522), Muandet et al. (2016).
* [Learning via Hilbert Space Embedding of Distributions - PhD Thesis](https://www.cc.gatech.edu/~lsong/papers/lesong_thesis.pdf), Le Song (2008).
* [Kernel Embeddings of Conditional Distributions](https://www.cc.gatech.edu/~lsong/papers/SonFukGre13.pdf), Le Song et al, (2013).
* [Modelling Policies in MDPs in Reproducing Kernel Hilbert Space](http://proceedings.mlr.press/v38/lever15.pdf), Lever et al (2015).
* [Kernel-Based Reinforcement Learning](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.464.7812&rep=rep1&type=pdf), Ormoneit et al. (2002).
* [Practical Kernel-Based Reinforcement Learning](https://arxiv.org/pdf/1407.5358.pdf), Barreto et al. (2014).
* [Reinforcement Learning using Kernel-Based Stochastic Factorization](https://www.cs.mcgill.ca/~jpineau/files/barreto-nips11.pdf), Barreto et al. (2011).
* [Conditional mean embeddings as regressors](http://www.gatsby.ucl.ac.uk/~gretton/papers/GruLevBalPatetal12.pdf), Grunewalder et al. (2012).
* [Modelling transition dynamics in mdps with rkhs embeddings](https://arxiv.org/pdf/1206.4655.pdf), Grunewalder et al. (2012).
* [Kernel-Based Reinforcement Learning on Representative States](https://www.aaai.org/ocs/index.php/AAAI/AAAI12/paper/viewFile/4967/5509), Kveton et al. (2012).
* [Least-Squares Policy Iteration](http://www.jmlr.org/papers/volume4/lagoudakis03a/lagoudakis03a.pdf),  Lagoudakis et al. (2003).
* [An Analysis of Linear Models, Linear Value-Function Approximation, and Feature Selection for Reinforcement Learning](https://users.cs.duke.edu/~parr/icml08.pdf), Parr et al. (2008).
* [Pseudo-MDPs and Factored Linear Action Models](https://sites.ualberta.ca/~szepesva/papers/ieee_adprl2014.pdf), Yao et al. (2008).
* [Approximate policy iteration: A survey and some new methods](https://dspace.mit.edu/handle/1721.1/73485), Bertsekas (2012).
* [Continuous Deep Q-Learning with Model-based Acceleration](https://arxiv.org/pdf/1603.00748.pdf),Gu et al. (2016).
* [Learning of Non-Parametric Control Policies with High-Dimensional State Features](http://proceedings.mlr.press/v38/vanhoof15.pdf), Van Hoof et al. (2015).
* [Learning Transition Dynamics in MDPs with Online Regression and Greedy Feature Selection](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.717.6587&rep=rep1&type=pdf), Lever et al. (2015).


