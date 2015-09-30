---
layout: post
title:  "Introdução à linguagem C, Operadores"
date:   29-09-2015 18:00:00
description: Sejam bem vindos ao curso de introdução à linguagem de programação C, nesta aula iremos aprender sobre operadores.
categories:
- cursos
- c
meta_description: Curso de introdução à linguagem de programação C, nesta aula aprenderemos sobre operadores.
browser_title: Operadores
permalink: cursos/c/aula3
comments: true
banner_video: '<iframe width="560" height="315" src="//www.youtube.com/embed/pPRM96Xkrcw" frameborder="0" allowfullscreen></iframe>'
---
Sejam bem vindos ao curso de introdução à linguagem de programação C, nesta aula iremos aprender sobre operadores.

## Operadores

Operadores são instruções para que o computador faça manipulações matemáticas ou lógicas, nesta aula iremos ver os operadores aritméticos, que fazem manipulaões matemáticas.

### Operadores Aritméticos

A tabela abaixo demonstra os operadores e seus respectivos exemplos:

Operador | Finalidade | Exemplo | Resultado
---------|------------|---------|----------
+ | Adição | 2 + 1 | 3
- | Subtração | 5 - 2 | 3
* | Multiplicação | 3 * 3 | 9
/ | Divisão | 8 / 2 | 4
% | Divisão euclidiana (Resto) | 5 % 2 | 1

Exemplo de programa:

{% highlight c %}
int soma = 10 + 20 + 30;
int sub = 90 - 45;
double div = 30 / 10;
double mult = 10 * 4;
int resto = 10 % 3;

printf("Soma: %d \n", soma);
printf("Subtracao: %d \n", (90 - 45));
printf("divisao: %lf \n", div);
printf("multiplicacao: %lf \n", mult);
printf("Resto: %d \n", resto);
{% endhighlight %}

### Operadores de incremento e decremento

O operador de incremento (++) soma 1 ao seu operando enquanto que o de decremento (\--) subtrai 1. A tabela abaixo mostra os dois tipos de uso:

Operador |Intrução | Pré-fixado | Pós-fixado
---------|---------|------------|-----------
++ | var = var + 1 | ++var | var++
\-- | var = var - 1 | \--var | var\--

A diferança entre o pós-fixado e o pré-fixado é que o primeiro executa o incremento e depois a instrução, enquanto o segundo executa a instrução e depois o incremento, o programa a seguir exemplifica:

{% highlight c %}
#include <stdio.h>

int main() {
  int inc1, inc2;
  inc1 = 10;
  inc2 = ++inc1;
  printf("Exemplo de incremento inc1: %d\n", inc1);
  printf("Exemplo de incremento inc2: %d\n", inc2);
}
{% endhighlight %}

Saída:

    Exemplo de incremento inc1: 11
    Exemplo de incremento inc2: 11

{% highlight c %}
#include <stdio.h>

int main() {
  int inc1, inc2;
  inc1 = 10;
  inc2 = inc1++;
  printf("Exemplo de incremento inc1: %d\n", inc1);
  printf("Exemplo de incremento inc2: %d\n", inc2);
}
{% endhighlight %}

Saída:

    Exemplo de incremento inc1: 11
    Exemplo de incremento inc2: 10

 A mudança é sensível e o leitor precisa tomar cuidado para não confundilos.

### Casting

Este recurso força um determinado valor assumir um determinado tipo, exemplo:

{% highlight c %}
#include <stdio.h>

int main() {
  int var1 = (int) 10/3;
  printf("Exemplo de casting: %d\n", var1);
}
{% endhighlight %}

Saída:

    Exemplo de casting: 3;

### Precedência

É a prioridade com que os operadores são executados pelo compilador. Caso os operadores tenham o mesmo nível de precedência eles são analisados da esquerda para direita:

Precedência | Operador
------------|----------
Alta | Incremento, decremento, multiplicação, divisão e módulo.
Baixa | Soma, subtração.

O uso de parenteses faz com que a precedência de operadores mude, mudando também o resultado final, exemplo:

    10/2+3+1 = 9;
    10/(2+3)+1 = 6;

Existem ainda os operadores relacionais, lógicos e bit a bit que serão vistos na próxima aula.

## Função **scanf**

Esta função fica dentro da biblioteca *stdio* e é responsável por ler a entrada padrão, que no nosso caso é o teclado. Ela recebe como primeiro parâmetro uma string contendo a sequência do tipo a ser lido, os demais parâmetros são as variáveis que receberão os valores lidos.
Obs: É necessário utilizar o '&' na frente do nome da variável, esta instrução será explicada mais a frente.

Exemplo:

{% highlight c %}
#include <stdio.h>

int main() {
  int n1, n2;
  printf("Entre com dois numeros inteiro:\n");
  scanf("%d%d", &n1, &n2);
  printf("Voce digitou: %d e %d \n", n1, n2);
}
{% endhighlight %}

Saída:

    Voce digitou: 3 e 7;

## Comentários

Comentários são partes do código que serão ignoradas pelo compilador, é bastante útil para organização do programa. Existem dois tipos de comentários: o de linha e de várias linhas, como se pode ver abaixo:

{% highlight c %}
#include <stdio.h>

int main() {
  int n1, n2; //comentário que será ignorado.
  printf("Entre com dois numeros inteiro:\n");
  scanf("%d%d", &n1, &n2);
  printf("Voce digitou: %d e %d \n", n1, n2);
  /*
  Comentário
  de varias
  linhas
  */
}
{% endhighlight %}

Saída:

    Voce digitou: 3 e 7;
