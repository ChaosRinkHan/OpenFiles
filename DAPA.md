## DAPA

### Divide & Conquer

Use recursive problem decomposition

-   Create sub-problems of the same kind, which are solved recursively
-   Combine sub-solutions to solve the original problem 
-   Define a base case for direct solution of simple instances 

Well-known examples: quicksort, mergesort, matrix multiply (Strassen)

### Pipelining 

Decompose operation into a sequence of *p* sub- operations and chain together processes (pipeline stages) for each sub-operation. 

### Scaling laws

#### Amdahl’s Law

Strong scaling. Inherently serial fraction $\alpha$. Run-time $T_p=\alpha T_s+(1-\alpha)T_s/p$

![image-20191208005426635](/Users/chaolinhan/Library/Application Support/typora-user-images/image-20191208005426635.png)

 𝑃 → ∞, s→$1/\alpha$

<img src="/Users/chaolinhan/Library/Application Support/typora-user-images/image-20191208005519748.png" alt="image-20191208005519748" style="zoom:67%;" />

Real-world scaling: the parallel fraction isn’t trivially parallelisable. Serial fraction is hard to determine.

#### Gustafson’s Law

Weak scaling: The problem size scales linearly with the number of processes. 

 $T(\alpha,P, N)=\alpha T_s+(1-\alpha)T_sN/p$, N is problem size.

$S(\alpha, P, P) = \alpha+(1-\alpha)P$, set P=N. 𝑃 → ∞, 𝑆 → ∞ 

  Real-world scaling: plus the problem size is not really scaling linearly with the number of processes. 

#### Generic scaling model

$T(\alpha,P,N)=\alpha T_s(N)+(1-\alpha)T(P,N)$

$T_s(1)$ constant: serial run-time for the minimal problem.must be measured. Note however, that it always cancels out if you calculate parallel speedup, since it defines the scale. 

$T_s(N)\propto T_s(1), T(P,N)\propto T_s(1)$

##### Amdahl’s Law

![image-20191208012629313](/Users/chaolinhan/Library/Application Support/typora-user-images/image-20191208012629313.png)

##### Gustafson’s Law

![image-20191208012652481](/Users/chaolinhan/Library/Application Support/typora-user-images/image-20191208012652481.png)

### Asymptotic analysis

Asymptotic (“big-O”) notation captures this idea as “upper”, “lower”, and “tight” bounds. **Constant factors are ignored.** 

![image-20191208013237909](/Users/chaolinhan/Library/Application Support/typora-user-images/image-20191208013237909.png)

𝑓(𝑛) is *no more than* 𝑔(𝑛). 𝑔(𝑛) is the *upper bound*. 

![image-20191208013442709](/Users/chaolinhan/Library/Application Support/typora-user-images/image-20191208013442709.png)

no less than; lower bound

![image-20191208013455753](/Users/chaolinhan/Library/Application Support/typora-user-images/image-20191208013455753.png)

is *approximately* equal to, tight bound

Θ(𝑁)
 • Scales like N, of order N. Tight bound. 

Ω(𝑁)
 • At least N, no less than N. Lower bound. 

𝑂(𝑁)
 • No more than N, no worse than N. Upper bound. 

### Architectures

#### Two dominant programming models

-   The *shared memory model* allows *threads* to interact directly through common memory locations. Care must be taken to ensure they don’t try to access the same memory location at the same time. 
-   The *message passing model* gives each process its own address space. Care must be taken to ensure that data is sent to the right place at the right time. 

#### Shared Address Space Parallelism

Real costs are complicated by cache coherence support, and congestion in the network. 

*Parallel Random Access Machine* (*PRAM)* model

### PRAM

Assumptions:

1.  𝑝 processes, synchronised for free whenever we like.
2.  𝑚 shared memory locations.
3.  Access to any memory location costs *unit time*.
4.  Memory clash resolution takes one of the following forms: 
    1.  EREW (exclusive-read, exclusive-write).
    2.  CREW (concurrent-read, concurrent-write).
    3.  CRCW (concurrent-read, concurrent-write). 

### CRCW write

Four variants for write clash resolution

Common (write same value), arbitrary (only one successes), priority, associative

### Metrics for Parallel Algorithms

Cost $C=pT_P$. Cost optimal: $pT_p = T_s$

Speedup: $S=Ts/T_p$. Cost optimal: S=p.

Parallel efficiency: $E=S/p$. Cost optimal: E=1.

### Brent’s Theorem

A PRAM algorithm involving 𝑡 time steps and performing a total of 𝑚 operations, can be executed by 𝑝 processes in no more than $t+\frac {m-t}{p}$ time steps. 

-   tells us that a better algorithm exists 
-   round robin scheduling and Brent’s theorem only apply asymptotically to CRCW-associative algorithms 

### Parallel computation primitives

to support a bottom-up approach to algorithm design

-   identify a collection of common operations and devise fast parallel implementations for each architecture
-   design algorithms with these primitives as reusable components

#### Reduction

values xi and an associative operator ⨁ 

Reduction computes $x_1⨁x_2⨁x_3⨁\cdots⨁x_n$

-   both (reduce-to-all or reduce-to-one) have the same cost

#### Prefix

Prefix (also called scan) computes $x_1. x_1⨁x_2, x_1⨁x_2⨁x_3, x_1⨁\cdots⨁x_n$

Each process has a *different value* when the prefix is done. 

The last process gets the same value as a reduction operation. 

### Parallel communication primitives

![image-20191208224014571](/Users/chaolinhan/Library/Application Support/typora-user-images/image-20191208224014571.png)

