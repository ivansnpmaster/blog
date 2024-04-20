---
layout: post
title: "Prova vetorial do seno e cosseno da soma de arcos"
author: Ivan Ribeiro
categories: matemática demonstração
---

<p>Um vetor $\newcommand{\R}{\mathbb{R}} \vec{\textbf{u}}=(a,\,b)\in\R^2$ pode ser representado através da combinação linear da base cartesiana:</p>

$$
    \newcommand{\vt}[1]{\vec{\textbf{#1}}}
    \newcommand{\vtu}[1]{\hat{\textbf{#1}}}

    \vt{u}=a\vtu{x}+b\vtu{y}
$$

<p>Uma rotação de $\theta$ unidades da base cartesiana na circunferência unitária é dada por:</p>
<img src="/blog/assets/img/2024-04-18/rotacao_base_cartesiana_r2.png" alt="Esquematização de uma rotação da base cartesiana R^2" style="width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; display: block;">

$$
    \newcommand{\rot}{\text{Rot}}
    
    \rot_\theta(\hat{\textbf{x}})=
    \begin{bmatrix}
        \cos(\theta)\\
        \sin(\theta)
    \end{bmatrix}
    \quad\text{ e }\quad
    \rot_\theta(\hat{\textbf{y}})=
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

Considerando $\vt{u}$ como $\text{Rot}_\alpha(\hat{\textbf{x}})$, pode-se tomar $\color{red}a=\cos(\alpha)$ e $\color{blue}b=\sin(\alpha)$ na equação (\ref{equacao-rocatao-vetor}) e rotacionar $\vt{u}$ em $\beta$ unidades da equação (\ref{equacao-rotacao-dupla}):

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
