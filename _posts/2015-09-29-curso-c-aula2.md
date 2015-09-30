---
layout: post
title:  "Introdução à linguagem C, Variáveis"
date:   29-09-2015 17:00:00
description: Curso de introdução à linguagem de programação C.
categories:
- cursos
- c
meta_description: Curso de introdução à linguagem de programação C, nesta aula aprenderemos sobre as variáveis.
browser_title: Variáveis
permalink: cursos/c/aula2
comments: true
banner_video: '<iframe width="560" height="315" src="//www.youtube.com/embed/iDNIZsik8wQ" frameborder="0" allowfullscreen></iframe>'
---
Sejam bem vindos ao curso de introdução à linguagem de programação C, nesta aula iremos aprender o que é variáveis.

## Variáveis

Variáveis são uns espaços reservados na memória para alocação de determinados valores, em C existem diferentes tipos de variáveis que aloca valores e tamanhos distintos. O tamanho deste espaço varia de acordo com a arquitetura do computador.

Para declarar uma variável basta digitar o tipo e logo em seguida o nome. Para que o nome da variável seja válido é necessário começar por um _ (undescore) ou uma letra, contudo podem-se haver números no meio e no fim. É necessário também que a variável não possua o mesmo nome de palavras reservadas, normalmente o editor colore as palavras reservadas.

A tabela abaixo mostra os diferentes tipos de variáveis:

Nome | Descrição
-----|----------
char | Guarda um caracter.
int | Guarda um número inteiro.
float | Guarda um número real com certa precisão.
double | Guarda um número real com maior precisão do que o float.
unsigned char | Guarda um caracter sem sinal.
long int | Guarda um número inteiro com domínio estendido.
unsigned int | Guarda um número inteiro sem sinal.
unsigned long int | Guarda um número inteiro com domínio estendido sem sinal.
short int | Guarda um número inteiro com domínio reduzido.
unsigned short int | Guarda um número inteiro com domínio reduzido sem sinal.

Abaixo temos exemplos de declaração de variáveis:

{% highlight c %}
char varChar1;
varChar1 = 'c';
char varChar2 = 90;

int varInt = 10;
long int varLongInt = 1000000;
short int varShortInt = 1;
unsigned int varUnsignedInt = 3;
unsigned short int varUnsignedShortInt = 90;

float varFloat = 100.45;
double varDouble = 500.78;
{% endhighlight %}

## Constantes

Constantes são valores imutáveis dentro do seu programa, para criar um constante no C, existem duas formas, a primeira usando o comando:

{% highlight c %}
#define PI 3.14159
{% endhighlight %}

ou utilizando a palavra reservada **const**:

{% highlight c %}
const float E = 2.718;
{% endhighlight %}

Por conversão toda constante deve ser escrita em caixa alta, facilitando assim a sua distinção para variáveis comuns.

## Função **printf**

Esta função está dentro da biblioteca *stdio* e é responsável por exibir um determinado texto na saída padrão, que nesta aula é o console. Para isso ela formata os vários tipos de variáveis em *string* de acordo com a tabela ASCII. O primeiro argumento de printf é um string de controle, uma sequência de caracteres entre aspas. Esta string, que sempre deve estar presente, pode especificar através de caracteres especiais (as seqüências de conversão) quantos outros argumentos estarão presentes nesta invocação da função. Estes outros argumentos serão variáveis cujos valores serão formatados e apresentados na tela.

Algumas sequencias de controles são:

Sequencia | Saída
------------ | -------------
%c | Imprime um caracter.
%d | Imprime um número inteiro.
%f | Imprime um número real.
%u | Imprime um número inteiro sem sinal.
%e | Imprime um número com notação cintífica.
\n | Quebra a linha.
\t | Insere uma tabulação.
\r | Identifica início de linha.
\\\ | Insere uma \

Exemplos:

{% highlight c %}
printf("Variaveis do tipo char %c e %c \n", varChar1, varChar2);
printf("Variaveis do tipo inteiro %d, %li, %hi, %u e %hu \n", varInt, varLongInt, varUnsignedInt, varUnsignedShortInt);
printf("Variavel do tipo real %f e %lf \n", varFloat, varDouble);
{% endhighlight %}

## Referências

http://www.ic.unicamp.br/~ducatte/mc102/aula03.pdf,  acessado no dia 23 de setembro de 2015.
