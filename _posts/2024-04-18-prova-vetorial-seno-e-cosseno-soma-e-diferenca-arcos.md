---
layout: post
title: "Prova vetorial de $\\sin(a+b)$ e $\\cos(a+b)$"
categories: matemática demonstração
---

<p>Um vetor $\vec{\textbf{u}}\in \mathbb{R}^2$ pode ser representado através da combinação linear da base cartesiana:</p>

$$\vec{\textbf{u}}=a\hat{\textbf{x}}+b\hat{\textbf{y}}$$

<p>Uma rotação de $\theta$ unidades da base cartesiana no círculo trigonométrico unitário é dada por:</p>

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

<p>A rotação no plano preserva algumas propriedades úteis. Com $k$ e $\theta\in\mathbb{R}$, um vetor $\vec{\textbf{u}}$ rotacionado por $\theta$ e depois escalonado por $k$ é o mesmo que um vetor $\vec{\textbf{u}}$ escalonado por $k$ e depois rotacionado por $\theta$.</p>

$$k\text{Rot}_\theta(\vec{\textbf{u}})=\text{Rot}_\theta(k\vec{\textbf{u}})$$

Isso significa que rotacionar um vetor $\vec{\textbf{u}}$ é o mesmo que rotacionar a base cartesiana e escaloná-la pelas componentes de $\vec{\textbf{u}}$.

$$\text{Rot}_\theta(\vec{\textbf{u}})=a\cdot\text{Rot}_\theta(\hat{\textbf{x}})+b\cdot\text{Rot}_\theta(\hat{\textbf{y}})$$

$$
\text{Rot}_\theta(\vec{\textbf{u}})=
  a
  \begin{bmatrix}
      \cos(\theta)\\
      \sin(\theta)
  \end{bmatrix}
  +
  b
  \begin{bmatrix}
      -\sin(\theta)\\
      \cos(\theta)
  \end{bmatrix}
$$

$$
\begin{equation}\tag{1}\label{equacao-rocatao-vetor}
        \text{Rot}_\theta(\vec{\textbf{u}})=
        \begin{bmatrix}
            a\cos(\theta)-b\sin(\theta)\\
            a\sin(\theta)+b\cos(\theta)
        \end{bmatrix}
    \end{equation}
$$

Ao rotacionarmos, por exemplo, $\hat{\textbf{x}}$ primeiramente por $\alpha$ e depois por $\beta$, teremos o mesmo resultado se tivéssemos rotacionado por $\alpha+\beta$, comutativamente.

$$\text{Rot}_{\alpha+\beta}(\hat{\textbf{x}})=\text{Rot}_\alpha(\text{Rot}_\beta(\hat{\textbf{x}}))=\text{Rot}_\beta(\text{Rot}_\alpha(\hat{\textbf{x}}))$$
