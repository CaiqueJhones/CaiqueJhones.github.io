---
layout: post
title:  "Java 8, Parte 2"
date:   25-07-2015 03:21:04
description: Série de tutoriais sobre as novas funcionalidades da linguagem de programação Java, nesta segunda parte iremos ver o que é interfaces funcionais.
categories:
- java
- tutoriais
permalink: interfaces-funcionais
meta_description: Série de tutoriais sobre as novas funcionalidades da linguagem de programação Java, nesta segunda parte iremos ver o que é interfaces funcionais.
browser_title: Interfaces funcionais
comments: true
---
Seja bem vindo a segunda parte da série de tutorias sobre Java 8 e neste tutorial iremos entender o que é e para que serve as interfaces funcionais.

### Sumário

1. [Seja bem vindo Lambda]({{ '/bem-vindo-lambda' | prepend: site.baseurl | prepend: site.url }})
2. Interfaces funcionais
3. [Default Methods]({{ '/default-methods' | prepend: site.baseurl | prepend: site.url }})
4. [Method Reference]({{ '/method-reference' | prepend: site.baseurl | prepend: site.url }})

## Interfaces funcionais

O Java 8 trás um novo pacote chamado de `java.util.function` que contém uma série de interfaces que podem e devem ser reaproveitadas para a utilização de [expressões lambdas](http://caiquejhones.github.io/bem-vindo-lambda), essas interfaces possuem apenas **um método abstrato** e esta característica faz com que elas sejam definidas como **interfaces funcionais**. Algumas interfaces antigas como `Runnable` e `ActionListerner` apesar de não sofrerem nenhum tipo de alteração na versão 8 da linguagem, também passaram a ser definidas como tal.

### Criando interfaces funcionais

Para criar uma interface funcional é muito simples, basta criar um interface comum que contenha um único método abstrato que sua interface já poderá ser usada com uma expressão lambda, vamos a um exemplo:

{% highlight java %}
package com.cjdeveloper.lambda.functions;

public interface Print {

	void draw(String txt);

}
{% endhighlight %}

{% highlight java %}
public static void exemplo2() {
	//Usando uma classe anônima
	Print p1 = new Print() {

		@Override
		public void draw(String txt) {
			System.out.println(txt);
		}
	};

	p1.draw("Aula sobre interfaces funcionais");

	//usando lambda
	Print p2 = txt -> System.out.println(txt);
	p2.draw("Aula sobre interfaces funcionais");
}
{% endhighlight %}

Dentro do método `exemplo2()` criamos primeiro uma classe anônima e executamos o método `draw` e logo abaixo criamos uma expressão lambda que executa a mesma tarefa, mas de uma forma muito mais enxuta, perceba que a variável `txt` dentro da expressão lambda é o argumento do método `draw`.


> Quando executamos apenas uma instrução dentro da expressão lambda, podemos suprimir as chaves.

Temos ainda a opção de anotar a nossa interface para que ela seja explicitamente uma interface funcional, desta forma:

{% highlight java %}
package com.cjdeveloper.lambda.functions;

@FunctionalInterface
public interface Print {

	void draw(String txt);

}
{% endhighlight %}

Isto garante que caso a interface ganhe um novo método abstrato acidentalmente, este erro ocorra:

	Exception in thread "main" java.lang.Error: Unresolved compilation problem:
	The target type of this expression must be a functional interface

E fará com que o Eclipse informe que o nosso programa contém erros. Esta anotação é opcional por um motivo muito importante: garantir que as interfaces existentes antes do Java 8 não quebrem.

Outro detalhe interessante sobre as expressões lambdas é que podemos utilizar varáveis locais do método em que a expressão está contida, assim como ocorre com as classe anônimas, com a única exigência que a variável seja `final`.


> A partir do Java 8 você não precisa mais explicitar que a variável local é final para utilizar dentro de classes anônimas ou expressões lambdas, basta apenas não alterá-la que o compilador irá traduzir como final, entretanto se houver qualquer alteração do valor da variável, um erro de compilação irá ocorrer.


{% highlight java %}

{% endhighlight %}
