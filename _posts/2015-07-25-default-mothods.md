---
layout: post
title:  "Java 8, Parte 3"
date:   25-07-2015 15:25:29  
description: Série de tutoriais sobre as novas funcionalidades da linguagem de programação Java, nesta terceira parte iremos ver o que são default methods.
categories:
- java
- tutoriais
permalink: default-methods
meta_description: Série de tutoriais sobre as novas funcionalidades da linguagem de programação Java, nesta terceira parte iremos ver o que são default methods.
browser_title: Default Methods
comments: true
---
Seja bem vindo a terceira parte da série de tutorias sobre Java 8 e neste tutorial iremos entender o que é e para que serve os métodos default.

### Sumário

1. [Seja bem vindo Lambda]
2. [Interfaces funcionais](http://caiquejhones.github.io/interfaces-funcionais)
3. Default Methods
4. [Method Reference](http://caiquejhones.github.io/method-reference)

## Default Methods

Vimos no tutorial [Seja bem vindo Lambda] o método `forEach` que está presente na interface `Iterable`, mas como este método funciona e por que códigos anteriores ao Java 8 não quebram com a inclusão deste novo método? Vamos analisá-lo:

{% highlight java %}
default void forEach(Consumer<? super T> action) {
    Objects.requireNonNull(action);
    for (T t : this) {
        action.accept(t);
    }
}
{% endhighlight %}

Isso mesmo, agora podemos utilizar métodos com código dentro de interfaces e todas as classes que implementam estas interfaces terão obrigatoriamente esses novos métodos. Para criar um método default basta utilizar a palavra reservada `default`. Vamos analisar também a interface Consumer:

{% highlight java %}
package java.util.function;

import java.util.Objects;

@FunctionalInterface
public interface Consumer<T> {

    void accept(T t);

    default Consumer<T> andThen(Consumer<? super T> after) {
        Objects.requireNonNull(after);
        return (T t) -> { accept(t); after.accept(t); };
    }
}
{% endhighlight %}

Notamos que existe um default method, vamos ver o que ele faz:

{% highlight java %}
public static void exemplo3() {
	Consumer<String> m1 = t -> System.out.println("Bem vindo:");
	Consumer<String> m2 = t -> System.out.println(t);
	
	List<String> list = Arrays.asList("Lambda", "Interfaces funcionais", "Default methods");
	
	list.forEach(m1.andThen(m2));
}
{% endhighlight %}

A saída será: 

	Bem vindo:
	Lambda
	Bem vindo:
	Interfaces funcionais
	Bem vindo:
	Default methods

Bem útil né? A API Collections ganhou vários métodos default que aumenta consideravelmente as capacidades da API, dentre eles temos o `removeIf` e o `replaceAll`, muito úteis quando estamos trabalhando com listas.

{% highlight java %}
public static void exemplo4() {
	ArrayList<String> list = new ArrayList<>();
	list.add("Lambda");
	list.add("Interfaces funcionais");
	list.add("Default methods");
	
	list.removeIf(s -> s.contains("i"));
	
	list.forEach(s -> System.out.println(s));
}
{% endhighlight %}

A saída será:

	Lambda
	Default methods

Apesar de podermos agora escrever métodos dentro de interfaces isso não representa que o Java passou a aceitar heranças múltiplas, pois ainda tem-se restrições ao utilizar os default methods, um deles é que não é possível utilizar variáveis de instância, já que interfaces não as possui, faz sentido não? 

[Seja bem vindo Lambda]:(http://caiquejhones.github.io/bem-vindo-lambda)