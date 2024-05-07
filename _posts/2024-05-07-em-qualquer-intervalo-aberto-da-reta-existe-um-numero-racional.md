---
layout: post
title: "Em qualquer intervalo aberto da reta existe um número racional"
categories: matemática demonstração
---

<p>$\newcommand{\R}{\mathbb{R}}\newcommand{\N}{\mathbb{N}}\newcommand{\Q}{\mathbb{Q}}$Para demonstrar que em qualquer intervalo aberto da reta existe um número racional, precisamos da propriedade arquimediana dos números reais:</p>

> Se $r\in\R$, com $r>0$, então existe um número $n\in\N$ tal que $0<\frac{1}{n}<r$.

<p>Agora, considere um intervalo aberto $I=(a,\,b)$, com $a$ e $b$ em $\R$ e $a<b$.</p>

Temos três casos:

- $a<0<b$
- $0<a<b$
- $a<b<0$

<p>O <b>primeiro caso</b> é trivial, pois zero é racional por definição.</p>

<p>Para o <b>segundo caso</b>, $0<a<b$, seja $r=b-a$. Implica que $r>0$, pois $b>a$. Pela propriedade arquimediana, existe $n\in\N$ tal que $\frac{1}{n}<r$.</p>

<p>Como $\frac{1}{n}<r=b-a$, então existe um $m\in\N$ tal que $a< \frac{m}{n}< b$. Esse $m$ pode ser pensado como um múltiplo do racional $\frac{1}{n}$, de modo que esse múltiplo $\frac{m}{n}$ em algum momento caia no intervalo $(a,\,b)$, exemplificado na figura a seguir:</p>

<img src="/blog/assets/img/2024/05/07/propriedade_arquimediana_reais_em_intervalo.jpg" alt="Esquematização da propriedade arquimediana dos números reais em um intervalo aberto" style="width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; display: block;">

<p>Logo, $\frac{m}{n}\in\Q\cap(a,\,b)$ para o segundo caso.</p>

<p>Para o <b>terceiro caso</b>, $a<b<0$, pode-se pensar no caso anterior refletido na origem:</p>

<img src="/blog/assets/img/2024/05/07/intervalo-refletido-origem.jpg" alt="Esquematização de um intervalo refletido na origem" style="width: 100%; max-width: 450px; margin-left: auto; margin-right: auto; display: block;">

<p>Como $a<b<0$, então $0<-b<-a$. Pelo caso anterior, existe $s\in\Q$ tal que $s\in(-b,\,-a)$. Logo, $-s\in\Q\cap(a,\,b)$.</p>