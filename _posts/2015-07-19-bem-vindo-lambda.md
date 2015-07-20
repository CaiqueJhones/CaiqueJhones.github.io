---
layout: post
title:  "Java 8, Parte 1"
date:   19-07-2015 20:30:21  
description: Série de tutoriais sobre as novas funcionalidades da linguagem de programação Java, nesta primeira parte iremos entender como funcionam as expressões Lambdas.
banner_image: java-8.png
categories:
- java
- tutoriais
permalink: bem-vindo-lambda
meta_description: Série de tutoriais sobre as novas funcionalidades da linguagem de programação Java, nesta primeira parte iremos entender como funcionam as expressões Lambdas.
browser_title: Bem vindo Lambda!
comments: true
---
Sejam bem vindos a esta série de tutoriais sobre o Java 8. Aqui abordaremos as principais funcionalidades acrescentadas na nova versão da linguagem e suas vantagens. Estaremos construindo diversos exemplos práticos que nos auxiliarão no aprendizado destes novos conceitos que o Java implementou.

Sumário:

1. Seja bem vindo Lambda
2. [Iterfaces funcionais](http://caiquejhones.github.io/)

## Seja bem vindo Lambda

Uma das principais ferramentas implementada na linguagem com certeza foram as expressões lambdas, com elas agora temos uma nova forma de fazer iteração sobre coleções, vamos a um exemplo:

{% highlight java %}
package com.cjdeveloper.lambda;

import java.util.Arrays;
import java.util.List;

public class TesteLambda {

	public static void main(String[] args) {
		exemplo1();
	}
	
	public static void exemplo1() {
		String nome = "Fabrício";
		String sobrenome = "Santos";
		String trabalho = "Agricultor";
		
		List<String> attr = Arrays.asList(nome, sobrenome, trabalho);
		
		System.out.println("---------Forma tradicional----------");
		for(String string : attr) {
			System.out.println(string);
		}
		System.out.println("---------Com expressão lambda-------");
		attr.forEach(string -> System.out.println(string));
	}

}
{% endhighlight %}

A saída deste programa será:

{% highlight %}
---------Forma tradicional----------
Fabrício
Santos
Agricultor
---------Com expressão lambda-------
Fabrício
Santos
Agricultor
{% endhighlight %}

Apesar desse código parecer estranho a princípio, iremos ver que não é nada complicado e com o tempo estaremos abtuados com ele. Mas da onde vem o método `forEach` e qual argumento deve ser passado? O método `forEach` está dentro da interface `java.lang.Iterable` na qual `List` é herdada e seu argumento é `java.util.function.Consumer` uma interface que contem um **único método abstrato** o `accept(T t)`.

Basicamente uma expressão Lambda dentro do Java é uma maneira menos verbosa de implementar uma interface que contem um único método abstrato(*Interfaces funcionais*), no caso do `forEach` é a interface `Consumer` que como o próprio nome diz, consome os dados dentro da coleção executando as instruções contida dentro do método `accept`. Podemos ainda estender este conceito para outros casos, como estes por exemplo:

{% highlight java %}
JButton button = new JButton("Click");
//forma tradicional
button.addActionListener(new ActionListener() {
	
	@Override
	public void actionPerformed(ActionEvent e) {
		System.out.println("Forma verbosa");
	}
});
//Com Lambda
button.addActionListener(e -> System.out.println("Com Lambda"));
//forma tradicional
Runnable run = new Runnable() {
	
	@Override
	public void run() {
		System.out.println("Forma verbosa");
		outros comandos...
	}
};
new Thread(run).start();

//Com Lambda
new Thread(() -> {
	System.out.println("Com Lambda");
	outros comandos...
}).start();
{% endhighlight %} 

Com estes exemplos fica evidente o quanto o código fica mais enxuto e muito menos verboso, na verdade por debaixo dos panos o compilador infere todo o código por nós dentro do método da interface, tornando a expressão Lambda no Java um forte recurso na hora da codificação.

Nos próximos tutoriais veremos de uma forma mais prática o uso das expressões Lambdas e como elas são importantes para todas as novidades do Java 8.