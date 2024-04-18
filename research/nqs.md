---
layout: page
title: Neural quantum states (NQS)
permalink: /research/nqs
use_math: true
---

### Table of contents

- [Introduction](#introduction)
- [Sign problem](#nqs-and-the-sign-problem)
- [Symmetries](#symmetries-in-nqs)
- [NQS for interacting fermions](#nqs-for-interacting-fermions)
- [Open-source software: NetKet](#open-source-software-netket)

## Introduction

Naïvely, many-body quantum wave functions contain an exponential amount of information: for example, the quantum state of *N* spin-1/2 particles can be fully described using $2^N$ complex numbers.
Given the memory constraints of real computers, such a complete description is only possible for small systems.
However, quantum states of physical interest, such as the ground states of condensed-matter systems, are highly structured and can be compressed using an appropriate representation.
The parameters of these *variational ansätze* can be optimised to represent ground states using *variational Monte Carlo*, or to track the time evolution of a state using the *time-dependent variational principle*.

Building on the success of deep neural networks at representing images, language, and other types of information motivates using them as a variational ansatz.
In such a *neural quantum state*, the network takes a computational basis state as its input and outputs its amplitude in the wave function $|\psi\rangle$.
For example, a many-body spin-1/2 quantum state can be written in the $\sigma^z$ basis as
<div>
$$ |\psi\rangle = \sum_{\sigma_1,\dots = \pm1} \psi(\sigma_1,\dots) |\sigma_1,\dots\rangle; $$
</div>
the neural network is used to encode the function $\psi(\sigma_1,\dots)$.

Neural quantum states have been used successfully for a variety of challenging problems in many-body quantum physics.
Nevertheless, it is a new method, with many open and challenging tasks to solve in order to bring out its full potential.
I am interested in solving these problems, as well as exploiting these improvements to solve open problems in condensed-matter physics.

## NQS and the sign problem

Quantum Monte Carlo methods allow us to solve quantum many-body problems numerically exactly.
However, they are limited by the *Monte Carlo sign problem:* the probability distribution used in the Monte Carlo sampling is only fully positive (i.e., a valid probability distribution) for <dfn title="A Hamiltonian is stoquastic if its off-diagonal matrix elements are negative or zero.">stoquastic</dfn> Hamiltonians. These include interacting bosons and non-frustrated magnets; by contrast, fermion systems and frustrated magnets are not amenable to quantum Monte Carlo.

[I discovered that NQS may show a similar "sign problem".](https://arxiv.org/abs/2002.04613)
Ground state wave functions of stoquastic Hamiltonians have all-positive amplitudes: they are equivalent to probability distributions, which are well represented by neural networks.
By contrast, learning the ground state of a non-stoquastic Hamiltonian involve destructive interference.
NQS architectures that split amplitudes and complex phases of the wave function struggle to follow these interferences, since the phase has to suddenly jump by $\pi$ whenever $\psi=0$.
This is a serious issue for such important architectures as [*recurrent neural networks*](https://en.wikipedia.org/wiki/Recurrent_neural_network), which need an explicit representation of the Born probability distribution.

![Ansätze with separate wave function amplitudes and phases (left) cannot track destructive interferences. Writing the wave function as a sum of terms (right) improves the issue.](/assets/2022/11/zero.png)

I found later that writing the wave function as a sum of terms allows tracking destructive interference in many cases: $\psi=0$ is no longer special, as it can be crossed by changing the relative magnitude of positive and negative terms.
This allowed us to obtain [excellent wave functions for such highly frustrated magnets](https://arxiv.org/abs/2211.07749) as the $J_1-J_2$ Heisenberg model on the square and triangular lattices.
Nevertheless, the sign structures of [fermion wave functions](#nqs-for-interacting-fermions) is considerably more complex, requiring more sophisticated approaches.

## Symmetries in NQS

## NQS for interacting fermions

## Open-source software: NetKet