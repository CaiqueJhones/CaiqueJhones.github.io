---
layout: post
title:  "Java 8, Parte 1"
date:   19-07-2015 20:30:21  
description: Série de tutoriais sobre as novas funcionalidades da linguagem de programação Java, nesta primeira parte iremos entender como funcionam as expressões Lambdas.
categories:
- java
- tutoriais
permalink: bem-vindo-lambda
meta_description: Série de tutoriais sobre as novas funcionalidades da linguagem de programação Java, nesta primeira parte iremos entender como funcionam as expressões Lambdas.
browser_title: Bem vindo Lambda!
comments: true
---
Sejam bem-vindos a esta série de tutoriais sobre o Java 8. Aqui abordaremos as principais funcionalidades acrescentadas nesta nova versão da linguagem e suas vantagens. Estaremos construindo diversos exemplos práticos que nos auxiliarão no aprendizado destes novos conceitos que o Java implementou.

### Sumário:

1. Seja bem-vindo Lambda
2. [Interfaces funcionais]({{ '/interfaces-funcionais' | prepend: site.baseurl | prepend: site.url }})
3. [Default Methods]({{ '/default-methods' | prepend: site.baseurl | prepend: site.url }})
4. [Method Reference]({{ '/method-reference' | prepend: site.baseurl | prepend: site.url }})

## Seja bem-vindo Lambda

Uma das principais características implementada na linguagem foi a expressão lambda, com ela podemos instanciar classes anônimas que possuem apenas um único método abstrato. Vamos analisar uma nova forma de fazer iteração em coleções:

{% highlight java %}
String nome = "Fabrício";
String sobrenome = "Santos";
String trabalho = "Agricultor";

List<String> attr = Arrays.asList(nome, sobrenome, trabalho);

System.out.println("---------Forma tradicional----------");
for(String s : attr) {
	System.out.println(s);
}

System.out.println("---------Com expressão lambda-------");
attr.forEach(s -> System.out.println(s));
{% endhighlight %}

A saída deste programa será:


	---------Forma tradicional----------
	Fabrício
	Santos
	Agricultor
	---------Com expressão lambda-------
	Fabrício
	Santos
	Agricultor


No exemplo acima temos uma lista de strings e em seguida exibimos seu conteúdo de duas formas distintas: a primeira com um `for each` tradicional e a segunda utilizando um método chamado `forEach`, que encontra-se na interface `java.lang.Iterable` na qual `List` é herdada, seu argumento é do tipo `java.util.function.Consumer` uma interface que contem um **único método abstrato**, o `accept(T t)`. Nos próximos artigos iremos entender como foi possível a interface `Iterable` ganhar esse novo método sem que tenha quebrado a compatibilidade com versões anteriores da linguagem. 

No método `forEach` passamos como parâmetro a expressão lambda `s -> System.out.println(s)`, que é uma maneira mais concisa de escrever:

{% highlight java %}
attr.forEach(new Consumer<String>{
	public void accept(String s) {
		System.out.println(s);
	}
});
{% endhighlight %}

O `s` antes do símbolo `->` é equivalente ao parâmetro do método `accept`, já o que vem depois do símbolo é equivalente ao corpo do método. Temos ainda outras formas de escrever as expressões lambdas, como apresentadas nos exemplos abaixo:

{% highlight java %}
Runnable r = () -> {
	int val = 10;
	System.out.println(val);
};
Thread th = new Thread(r);
th.start();
{% endhighlight %}

{% highlight java %}
Test t = (a, b) -> {
	int s = a + b;
	return s;
};
System.out.println("A soma de 1 + 2 = " + t.sum(1 + 2));

interface Test {
	int sum(int a, int b);
}
{% endhighlight %}

{% highlight java %}
JButton button = new JButton("Click");
button.addActionListener(event -> System.out.println("Fui clicado!"));
{% endhighlight %}

Podemos notar que: 

* Quando o método não possui argumentos como é o caso do `run` da interace `Runnable`, temos que usar `()` antes do símbolo de flecha. 
* Para um corpo que possui mais de uma instrução, devemos coloca-lo entre chaves. 
* Para casos que o método possui dois ou mais argumentos, temos a sintaxe `(a, b) ->`, os parenteses só podem ser omitidos quando temos um único argumento. 

Outro detalhe sobre as expressões lambdas é que podemos utilizar varáveis locais do bloco em que a expressão está contida, assim como ocorre com as classe anônimas (lembre que existe uma exigência para que a variável seja `final`).

> A partir do Java 8 você não precisa mais explicitar que a variável local é `final` para utilizar dentro de classes anônimas ou expressões lambdas, basta apenas não alterá-la que o compilador irá traduzir como final.

### Conclusão

As expressões lambdas são alternativas mais concisas para instanciar classes anônimas, tornando o código mais enxuto e menos verboso. Quando aliadas aos novos recursos da linguagem teremos mecanimos para tornar o nosso código mais simples e fáceis de serem lidos. No próximo artigo entederemos o que são interaces funcionais e como elas são importantes para as novas APIs da linguagem.
