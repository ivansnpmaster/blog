---
layout: post
title: "Interpolação exponencial"
categories: matemática
---

<p>$\newcommand{\R}{\mathbb{R}}$A interpolação exponencial ($eerp$ — <a href="https://twitter.com/FreyaHolmer/status/1068280365108920320" target="_blank">cunhado por Freya Holmér</a>) é uma técnica de interpolação paramétrica que, assim como a interpolação linear, pode ser fixa ou não-fixa:</p>

$$eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})=\color{red}{a}^{(1-\color{magenta}{t})}\color{blue}{b}^\color{magenta}{t}\text{, com }\color{red}{a},\,\color{blue}{b}\in\R^*_+\text{ e }\color{magenta}{t}\in\R$$

<p>Para a versão fixa, o teste da primeira derivada evidencia que se trata, de fato, de uma interpolação entre $\color{red}{a}$ e $\color{blue}{b}$. Considere:</p>

$$eerp'(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})=eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})[\ln(\color{blue}{b})-\ln(\color{red}{a})]$$

- <p>Quando $\color{red}{a}>\color{blue}{b}$, então $\inf_{\color{magenta}{t}\in[0,1]} eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})=\color{blue}{b}$ e $\sup_{\color{magenta}{t}\in[0,1]} eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})=\color{red}{a}$:</p>

<p>Como $eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})>0$ e $\ln(\color{red}{a})>\ln(\color{blue}{b})$, tem-se $eerp'$ negativa. Portanto, $eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})$ é <b>estritamente decrescente</b>. Assim, tem-se:</p>

$$\inf_{\color{magenta}{t}\in[0,1]}eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})=eerp(\color{red}{a},\,\color{blue}{b},\,0)=\color{blue}{b}$$

E,

$$\sup_{\color{magenta}{t}\in[0,1]}eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})=eerp(\color{red}{a},\,\color{blue}{b},\,1)=\color{red}{a}$$

- Quando $\color{red}{a}<\color{blue}{b}$, então $\inf_{\color{magenta}{t}\in[0,1]} eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})=\color{red}{a}$ e $\sup_{\color{magenta}{t}\in[0,1]} eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})=b$:

<p>Como $eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})>0$ e $\ln(\color{red}{a})<\ln(\color{blue}{b})$, tem-se $eerp'$ positiva. Portanto, $eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})$ é <b>estritamente crescente</b>. Assim,</p>

$$\inf_{\color{magenta}{t}\in[0,1]}eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})=eerp(\color{red}{a},\,\color{blue}{b},\,0)=\color{red}{a}$$

E,

$$\sup_{\color{magenta}{t}\in[0,1]}eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})=eerp(\color{red}{a},\,\color{blue}{b},\,1)=\color{blue}{b}$$

- <p>Quando $\color{red}{a}=\color{blue}{b}$, tem-se $eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})$ <b>constante</b>, pois:</p>
    
$$eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})=\color{red}{a}^{(1-\color{magenta}{t})}\color{blue}{b}^\color{magenta}{t}=\color{red}{a}^{(1-\color{magenta}{t})}\color{red}{a}^\color{magenta}{t}=\color{red}{a}$$

<p>Os dois primeiros casos estão exemplificados a seguir. Quando $\color{red}{a}<\color{blue}{b}$, tem-se:</p>

<img src="/blog/assets/img/2024/04/29/interpolação_exponencial_a.png" alt="Interpolação exponencial - caso em que 'a' é menor que 'b'" style="width: 100%; max-width: 300px; margin-left: auto; margin-right: auto; display: block;">

<p>Agora, para $\color{blue}{b}<\color{red}{a}$:</p>

<img src="/blog/assets/img/2024/04/29/interpolação_exponencial_b.png" alt="Interpolação exponencial - caso em que 'b' é menor que 'a'" style="width: 100%; max-width: 300px; margin-left: auto; margin-right: auto; display: block;">

<p>Ela pode aparecer de outras formas. Por exemplo, a partir da reescrita $y=c^{\log_c y}$, com $c\in\R^*_+$ e $c\neq1$:</p>

$$
\begin{align*}
    eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})
    &=\color{red}{a}^{(1-\color{magenta}{t})}\color{blue}{b}^\color{magenta}{t}\\
    &=c^{\log_c \color{red}{a}^{(1-\color{magenta}{t})}}\cdot c^{\log_c \color{blue}{b}^\color{magenta}{t}}\\
    &=c^{(1-\color{magenta}{t})\log_c \color{red}{a}\,+\,\color{magenta}{t}\log_c \color{blue}{b}}\\
    &=c^{lerp(\log_c \color{red}{a},\;\log_c \color{blue}{b},\;\color{magenta}{t})}
\end{align*}
$$

<p>Ainda, há outra forma mais interessante computacionalmente pela remoção de um cálculo de potência:</p>

$$
\begin{align*}
    eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})
    &=\color{red}{a}^{(1-\color{magenta}{t})}\color{blue}{b}^\color{magenta}{t}\\
    &=\frac{\color{red}{a}}{\color{red}{a}^\color{magenta}{t}}\color{blue}{b}^\color{magenta}{t}\\
    &=\color{red}{a}\left(\frac{\color{blue}{b}}{\color{red}{a}}\right)^\color{magenta}{t}
\end{align*}
$$

<p>Isso significa que a interpolação exponencial é uma função exponencial de base positiva. Como toda função exponencial é infinitamente diferenciável, então $eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})$ é infinitamente diferenciável. Assim, a $n$-ésima derivada em relação a $\color{magenta}{t}$, com $n\geqslant1$, é:</p>

$$eerp^{(n)}(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})=eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})\cdot\ln\left(\frac{\color{blue}{b}}{\color{red}{a}}\right)^n$$

<p>Portanto, tem-se $eerp(\color{red}{a},\,\color{blue}{b},\,\color{magenta}{t})\in C^\infty$ (uma função suave).</p>