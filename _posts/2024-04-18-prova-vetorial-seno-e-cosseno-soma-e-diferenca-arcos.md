---
layout: post
title: "Prova vetorial do seno e cosseno da soma de arcos"
author: Ivan Ribeiro
categories: matemática demonstração
---
$
    \DeclareMathOperator{\sen}{sen}
    \newcommand{\R}{\mathbb{R}}
    \newcommand{\vt}[1]{\vec{\textbf{#1}}}
    \newcommand{\vtu}[1]{\hat{\textbf{#1}}}
    \newcommand{\rot}{\text{Rot}}
$
O objetivo deste post é demonstrar as seguintes igualdades:

$$\sen(\alpha+\beta)=\sen(\alpha)\cos(\beta)+\sen(\beta)\cos(\alpha)$$

$$\cos(\alpha+\beta)=\cos(\alpha)\cos(\beta)-\sen(\alpha)\sen(\beta)$$

<p>Um vetor $\vt{u}=(a,\,b)\in\R^2$ pode ser representado através da combinação linear da base cartesiana:</p>

$$\vt{u}=a\vtu{x}+b\vtu{y}$$

<p>Uma rotação de $\theta$ unidades da base cartesiana na circunferência unitária é dada por:</p>
<img src="/blog/assets/img/2024-04-18/rotacao_base_cartesiana_r2.png" alt="Esquematização de uma rotação da base cartesiana R^2" style="width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; display: block;">

$$
    \rot_\theta(\vtu{x})=
    \begin{bmatrix}
        \cos(\theta)\\
        \sin(\theta)
    \end{bmatrix}
    \quad\text{ e }\quad
    \rot_\theta(\vtu{y})=
    \begin{bmatrix}
        -\sin(\theta)\\
        \cos(\theta)
    \end{bmatrix}
$$

<p>A rotação no plano preserva algumas propriedades úteis. Com $k$ e $\theta\in\R$, um vetor $\vt{u}$ rotacionado por $\theta$ e depois escalonado por $k$ é o mesmo que um vetor $\vt{u}$ escalonado por $k$ e depois rotacionado por $\theta$.</p>

$$k\rot_\theta(\vt{u})=\rot_\theta(k\vt{u})$$

Isso significa um vetor $\vt{u}$ pode ser pensado como a base cartesiana rotacionada e escalonada pelas componentes de $\vt{u}$:

$$\rot_\theta(\vt{u})=a\rot_\theta(\vtu{x})+b\rot_\theta(\vtu{y})$$

$$
\rot_\theta(\vt{u})=
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
        \rot_\theta(\vt{u})=
        \begin{bmatrix}
            a\cos(\theta)-b\sin(\theta)\\
            a\sin(\theta)+b\cos(\theta)
        \end{bmatrix}
    \end{equation}
$$

Ao rotacionarmos, por exemplo, $\vtu{x}$ primeiramente por $\alpha$ e depois por $\beta$, teremos o mesmo resultado se tivéssemos rotacionado por $\alpha+\beta$, comutativamente.

$$\rot_{\alpha+\beta}(\vtu{x})=\rot_\alpha(\rot_\beta(\vtu{x}))=\rot_\beta(\rot_\alpha(\vtu{x}))$$

Tem-se, ainda:

$$
\begin{equation}\tag{2}
    \label{equacao-rotacao-dupla}
    \rot_\beta(\rot_\alpha(\vtu{x}))
    =
    \rot_\beta\left(
        \begin{bmatrix}
            \cos(\alpha)\\
            \sin(\alpha)
        \end{bmatrix}
    \right)
\end{equation}
$$

Considerando $\vt{u}$ como $\rot_\alpha(\vtu{x})$, pode-se tomar $\color{red}a=\cos(\alpha)$ e $\color{blue}b=\sin(\alpha)$ na equação (\ref{equacao-rocatao-vetor}) e rotacionar $\vt{u}$ em $\beta$ unidades da equação (\ref{equacao-rotacao-dupla}):

$$
  \rot_{\alpha+\beta}(\vtu{x})
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
