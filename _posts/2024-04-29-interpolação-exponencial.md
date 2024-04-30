---
layout: post
title: "Interpolação exponencial (eerp)"
categories: matemática
---

<p>$\newcommand{\R}{\mathbb{R}}$A interpolação exponencial (<i>eerp</i> — [cunhado por Freya Holmér](https://twitter.com/FreyaHolmer/status/1068280365108920320)) é uma técnica de interpolação paramétrica que, assim como a interpolação linear, pode ser fixa ou não-fixa:</p>

$$eerp(a,\,b,\,t)=a^{(1-t)}b^t\text{, com }a,\,b\in\R^*_+\text{ e }t\in\R$$

<p>Para a versão fixa, o teste da primeira derivada evidencia que se trata, de fato, de uma interpolação entre $a$ e $b$. Considere:</p>

$$eerp'(a,\,b,\,t)=eerp(a,\,b,\,t)[\ln(b)-\ln(a)]$$

- <p>Quando $a>b$, então $\inf_{x\in[0,1]} eerp(a,\,b,\,t)=b$ e $\sup_{x\in[0,1]} eerp(a,\,b,\,t)=a$:</p>

<p>Como $eerp(a,\,b,\,t)>0$ e $\ln(a)>\ln(b)$, tem-se $eerp'$ negativa. Portanto, $eerp(a,\,b,\,t)$ é <b>estritamente decrescente</b>. Assim, tem-se:</p>

$$\inf_{x\in[0,1]}eerp(a,\,b,\,t)=eerp(a,\,b,\,0)=b\quad\text{ e }\quad\sup_{x\in[0,1]}eerp(a,\,b,\,t)=eerp(a,\,b,\,1)=a$$

- Quando $a<b$, então $\inf_{x\in[0,1]} eerp(a,\,b,\,t)=a$ e $\sup_{x\in[0,1]} eerp(a,\,b,\,t)=b$:

<p>Como $eerp(a,\,b,\,t)>0$ e $\ln(a)<\ln(b)$, tem-se $eerp'$ positiva. Portanto, $eerp(a,b,t)$ é <b>estritamente crescente</b>. Assim,</p>

$$\inf_{x\in[0,1]}eerp(a,\,b,\,t)=eerp(a,\,b,\,0)=a\quad\text{ e }\quad\sup_{x\in[0,1]}eerp(a,\,b,\,t)=eerp(a,\,b,\,1)=b$$

- <p>Quando $a=b$, tem-se $eerp(a,\,b,\,t)$ <b>constante</b>, pois:</p>
    
$$eerp(a,\,b,\,t)=a^{(1-t)}b^t=a^{(1-t)}a^t=a$$

<p>Os dois primeiros casos estão exemplificados a seguir. Quando $a<b$, tem-se:</p>

<img src="/blog/assets/img/2024-04-29/interpolação_exponencial_a.jpg" alt="Interpolação exponencial - caso em que 'a' é menor que 'b'" style="width: 100%; max-width: 300px; margin-left: auto; margin-right: auto; display: block;">

<p>Agora, para $b<a$:</p>

<p>Ela pode aparecer de outras formas. Por exemplo, a partir da reescrita $y=c^{\log_c y}$, com $c\in\R^*_+$ e $c\neq1$:</p>

$$
\begin{align*}
    eerp(a,\,b,\,t)
    &=a^{(1-t)}b^t\\
    &=c^{\log_c a^{(1-t)}}\cdot c^{\log_c b^t}\\
    &=c^{(1-t)\log_c a+t\log_c b}\\
    &=c^{lerp(\log_c a,\;\log_c b,\;t)}
\end{align*}
$$

<p>Ainda, há outra forma mais interessante computacionalmente pela remoção de um cálculo de potência:</p>

$$
\begin{align*}
    eerp(a,\,b,\,t)
    &=a^{(1-t)}b^t\\
    &=\frac{a}{a^t}b^t\\
    &=a\left(\frac{b}{a}\right)^t
\end{align*}
$$

<p>Isso significa que a interpolação exponencial é uma função exponencial de base positiva. Como toda função exponencial é infinitamente diferenciável, então $eerp(a,\,b,\,t)$ é infinitamente diferenciável. Assim, a $n$-ésima derivada em relação a $t$, com $n\geqslant1$, é:</p>

$$eerp^{(n)}(a,\,b,\,t)=eerp(a,\,b,\,t)\cdot\ln\left(\frac{b}{a}\right)^n$$

<p>Portanto, tem-se $eerp(a,\,b,\,t)\in C^\infty$.</p>