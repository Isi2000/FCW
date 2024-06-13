# Flexible Chainlike Walker systems in python

This repository contains a Python implementation of the Flexible Chain-like Walker (FCW) model. The FCW model simulates a series of connected particles, resembling a chain, that move on a 2D lattice with periodic boundary conditions. This dynamic system is used to study mobility and clustering phenomena in grid-based environments.

## Description of the model

At its core, the model consists of a series of connected particles that resem-
ble a chain. The movement of the walker is initiated by the head, which navigates the
grid moving in free adjacent spots with equal probability. As the head moves, the parti-
cles behind it, representing the body, maintaining their relative positions to one another
while following the motion


## Features

- **Flexible chain dynamics:** Simulate chain-like walkers that navigate a grid.
- **Periodic boundary conditions:** Enable seamless transitions across the grid's edges.
- **Mobility measurement:** Calculate the system's mobility based on the movement of chain heads.
- **Locking phenomena:** Study mutual and self-locking configurations that affect mobility.
- **Visualization:** Generate visual representations of the chain movements.

## Description of the Model

The FCW model consists of a series of connected particles (chains) moving on a grid. The head of each chain moves to a free adjacent spot with equal probability, while the rest of the chain follows, maintaining their relative positions. The grid uses periodic boundary conditions, meaning particles moving off one edge reappear on the opposite edge.

### Key Concepts

- **Mobility ($M(t)$):** The ratio of chains able to move at time $t$. $M(\bar{t}) = 1$ for a time step $\bar{t}$ means that each chain has at least one free spot near it and will perform a step. Clustering arises when chains cannot move and are bound to a cluster. Measuring mobility provides insights into the clustering properties of the system.

### Locking Phenomena

Before estimating mobility under different conditions, it's necessary to analyze the phenomena of locking, which can be of two kinds: mutual locking and self-locking.

- **Mutual Locking:** Occurs when two chains block each other's heads (Figure \ref{fig:mutual_locking}).
- **Self-Locking:** A locked state occurs when a single chain turns on itself, blocking all nearest neighbors of its head (Figure \ref{fig:self_locking}). This can only occur for chain lengths $\geq 8`.

These configurations are trap states; once the chains get into this configuration, they can never change, permanently decreasing mobility for future time steps.

\begin{figure}[htbp]
\centering
\begin{subfigure}{0.3\textwidth}
\includegraphics[width=\linewidth]{images/mutual_locking.png}
\caption{Mutual Locking}
\label{fig:mutual_locking}
\end{subfigure}
\begin{subfigure}{0.3\textwidth}
\includegraphics[width=\linewidth]{images/self_locking.png}
\caption{Self Locking}
\label{fig:self_locking}
\end{subfigure}
\caption{Illustrations of locking phenomena in the flexible chain-like walker model.}
\label{fig:lock}
\end{figure}

The quantity of interest for these simulations is the mobility after a long time $M_{\infty}$ as a function of the density $\rho$, defined as the number of spots occupied by chains over the total number of squares on the grid. $M_{\infty}$ measures how many particles are clustered during an indefinite evolution of the system.

### Analytical Expressions for Mobility

With simple reasoning, we can derive analytical expressions for mobility as a function of density for chain lengths up to 2 and greater than 8:

- **Chain Length 1:** This is a degenerate case, as it's just a self-avoiding random walk. There are no locking phenomena, so mobility is only influenced by density.
  $$M_{\infty} = 1 - \rho^4$$
  The exponent is due to the fact that without locking phenomena, mobility is influenced only if all 4 adjacent spots are occupied.

- **Chain Length 2:** Similar to chain length 1, but one of the possible neighbors is always occupied.
  $$M_{\infty} = 1 - \rho^3$$

- **Chain Lengths 3 to 7:** Mutual locking can occur, but not self-locking. The exact expression for $M_{\infty}$ is not determined, but we expect a monotonically decreasing function of density.

- **Chain Lengths ≥ 8:** Self-locking can occur, so the system will eventually reach mobility 0 as all chains go into the trap state, forming clusters that stand still.

Overall, for statistical simulations, we expect the mobility to be a monotonically decreasing function of density.
