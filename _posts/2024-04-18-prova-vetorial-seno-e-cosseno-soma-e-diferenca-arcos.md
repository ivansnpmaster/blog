---
layout: post
title: "Prova vetorial de $\\sin(a+b)$ e $\\cos(a+b)$"
author: Ivan Ribeiro
categories: matemática demonstração
usemathjax: true
---

<p>Um vetor \(\vec{\textbf{u}}=(a,\,b)\in \mathbb{R}^2\) pode ser representado através da combinação linear da base cartesiana:</p>

$$\vec{\textbf{u}}=a\hat{\textbf{x}}+b\hat{\textbf{y}}$$

<p>Uma rotação de $\theta$ unidades da base cartesiana na circunferência unitária é dada por:</p>

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

Isso significa que rotacionar um vetor $\vec{\textbf{u}}$ é o mesmo que rotacionar a base cartesiana e escaloná-la pelas componentes de $\vec{\textbf{u}}$:

$$\text{Rot}_\theta(\vec{\textbf{u}})=a\text{Rot}_\theta(\hat{\textbf{x}})+b\text{Rot}_\theta(\hat{\textbf{y}})$$

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

Tem-se, ainda:

$$
\begin{equation}\tag{2}
    \label{equacao-rotacao-dupla}
    \text{Rot}_\beta(\text{Rot}_\alpha(\hat{\textbf{x}}))
    =
    \text{Rot}_\beta\left(
        \begin{bmatrix}
            \cos(\alpha)\\
            \sin(\alpha)
        \end{bmatrix}
    \right)
\end{equation}
$$

Lembrando a equação (\ref{equacao-rocatao-vetor}):

$$
  \text{Rot}_\theta(\vec{\textbf{u}})
  =
  \begin{bmatrix}
      \color{red}a\color{black}\cos(\theta)-\color{blue}b\color{black}\sin(\theta)\\
      \color{red}a\color{black}\sin(\theta)+\color{blue}b\color{black}\cos(\theta)
  \end{bmatrix}
$$

Tomando $\color{red}{a=\cos(\alpha)}$ e $\color{blue}{b=\sin(\alpha)}$ nas equações (\ref{equacao-rocatao-vetor}) e (\ref{equacao-rotacao-dupla}), e considerando a rotação por $\beta$ da equação (\ref{equacao-rotacao-dupla}), tem-se:

$$
  \text{Rot}_{\alpha+\beta}(\hat{\textbf{x}})
  =
  \begin{bmatrix}
      \cos(\alpha+\beta)\\
      \sin(\alpha+\beta)
  \end{bmatrix}
  =
  \begin{bmatrix}
      \color{red}{\cos(\alpha)}\cos(\beta)-\color{blue}{\sin(\alpha)}\sin(\beta)\\
      \color{red}{\cos(\alpha)}\sin(\beta)+\color{blue}{\sin(\alpha)}\cos(\beta)
  \end{bmatrix}
$$
