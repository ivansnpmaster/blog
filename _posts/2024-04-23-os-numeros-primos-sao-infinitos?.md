---
layout: post
title: "Os números primos são infinitos?"
author: Ivan Ribeiro
categories: matemática demonstração
---

<p>$\textbf{Definição}$: Um número $\textit{primo}$ é um número natural diferente de zero e de $1$ que só é divisível por $1$ e por ele mesmo. Um inteiro positivo maior que $1$ que não é primo é chamado de $\textit{composto}$.</p>

<p>Uma coisa é certa: os números compostos são infinitos. Por exemplo, os números pares. Já os números primos são também? Euclides propôs uma prova por absurdo:</p>

<p>$\textbf{Hipótese}$: Os números primos são finitos.</p>

Vamos criar um número $A$ que é o produto de todos os finitos primos, sendo:

$$A=p_1\cdot p_2 \cdot\ldots\cdot p_r$$

<p>O número $A$ possui um sucessor, que é $A+1$. Ele não é primo, pois não está dentro da multiplicação acima e é maior que cada primo individualmente e também maior que o próprio $A$. Logo,  $A+1$ é $\textit{composto}$. Como $A+1$ é composto, ele é múltiplo de algum primo que é fator de $A$:</p>

$$A+1=k\cdot p_i$$

<p>Porém, como $p_i$ está na multiplicação que resultou em $A$, ele também é um fator de $A$.</p>

$$A=r\cdot p_i$$

<p>Agora, podemos relacionar $A=r\cdot p_i$ com $A+1$:</p>

$$
  \begin{align*}
    (r\cdot p_i)+1&=k\cdot p_i\\
    1&=k\cdot p_i-r\cdot p_i\\
    1&=p_i(k-r)
  \end{align*}
$$

<p>Chegamos a um absurdo: que $1$ é divisível pelo primo $p_i$. Logo, nossa hipótese inicial é falsa. Isso significa que seu complemento é verdadeiro: os números primos são infinitos.</p>
