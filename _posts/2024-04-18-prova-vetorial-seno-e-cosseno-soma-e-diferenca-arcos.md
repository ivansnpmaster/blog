---
layout: post
title: "Prova vetorial de $\\sin(a+b)$ e $\\cos(a+b)$"
categories: matemática demonstração
---

Um vetor $\vec{\textbf{u}}\in \mathbb{R}^2$ pode ser representado através da combinação linear da base cartesiana:

$$\vec{\textbf{u}}=a\hat{\textbf{x}}+b\hat{\textbf{y}}$$

Uma rotação de $\theta$ unidades da base cartesiana no círculo trigonométrico unitário é dada por:

$$
\text{Rot}_\theta(\hat{\textbf{x}})=
\begin{bmatrix}
\cos(\theta)\\
\sin(\theta)
\end{bmatrix}
\quad\text{ e }\quad
\text{Rot}_\theta(\hat{\textbf{y}})=
\begin{bmatrix}
-\sin(\theta)\\
\cos(\theta)
\end{bmatrix}
$$

A rotação no plano preserva algumas propriedades úteis. Com $k$ e $\theta\in\mathbb{R}$, um vetor $\vec{\textbf{u}}$ rotacionado por $\theta$ e depois escalonado por $k$ é o mesmo que um vetor $\vec{\textbf{u}}$ escalonado por $k$ e depois rotacionado por $\theta$.

$$\text{Rot}_\theta(\vt{u})=\text{Rot}_\theta(k\vt{u})$$
