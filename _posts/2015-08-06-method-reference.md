---
layout: post
title:  "Java 8, Parte 4"
date:   06-08-2015 18:21:37
description: Série de tutoriais sobre as novas funcionalidades da linguagem de programação Java, nesta quarta parte iremos entender como funciona o method reference.
categories:
- java
- tutoriais
permalink: method-reference
meta_description: Série de tutoriais sobre as novas funcionalidades da linguagem de programação Java, nesta quarta parte iremos entender como funciona o method reference.
browser_title: Method Reference
comments: true
---
Seja bem-vindo a quarta parte da série de tutorias sobre Java 8 e neste tutorial iremos entender o que é e para que serve os *method references*.

### Sumário

1. [Seja bem vindo Lambda]({{ '/bem-vindo-lambda' | prepend: site.baseurl | prepend: site.url }})
2. [Interfaces funcionais]({{ '/interfaces-funcionais' | prepend: site.baseurl | prepend: site.url }})
3. [Default Methods]({{ '/default-methods' | prepend: site.baseurl | prepend: site.url }})
4. Method Reference

## Method References

O *method reference* é um recurso bastante parecido com as expressões lambdas e também são inferidos em tempo de compilação, sua sintaxe é bastante simples, vamos a um exemplo:

{% highlight java %}
public class Author {
	private String name;
	
	// construtor, gets e sets

	public void imprime() {
		System.out.println(name);
	}
}

Author caique = new Author("Caique Jhones");
Author junior = new Author("Junior dos Santos");
Author flavio = new Author("Flávio José");

List<Author> autores = Arrays.asList(caique, junior, flavio);

Consumer<Author> comLambda = a -> a.imprime();
Consumer<Author> comReference = Author::imprime;

autores.forEach(comLambda);
System.out.println("-------------");
autores.forEach(comReference);
{% endhighlight %}

A saída:

	Caique Jhones
	Junior dos Santos
	Flávio José
	-------------
	Caique Jhones
	Junior dos Santos
	Flávio José

Perceba que foi utilizado o nome da classe juntamente com o delimitador `::` concatenado com o nome do método **sem os parênteses**, isso equivale a expressão lambda só que com um código mais enxuto, esse novo conceito da linguagem será útil na utilização das novas API's (como RxJava por exemplo) e deixará o código mais funcional. Não existe reflexão em *method reference* tudo é feito em tempo de compilação.

### Referenciando métodos de instância

Um *method reference* do tipo `Author::imprime` só pode ser atribuído a uma interface funcional que receba como argumento uma instância da classe `Author`, que é o caso da interface `Consumer`:

{% highlight java %}
public interface Consumer<T> {
    void accept(T t);
}
{% endhighlight %}

a partir daí o compilador pode executar o método `imprime` da instância recebida no método `acept`. Entretanto podemos utilizar uma instância de `Author`, o *method reference* fica desta forma: `caique::imprime`, e a partir daí utilizá-lo em uma interface funcional que não recebe nenhum parâmetro. Exemplo:

{% highlight java %}
Runnable r = caique::imprime;
new Thread(r).start();
{% endhighlight %}

Não confunda a chamada `Author::imprime` com `caique::imprime`, pois o primeiro executará o método de qualquer `Author` que será passado por parâmetro dentro da interface funcional, já o segundo executará o método da instância que o chamou.

### Com construtores

Podemos ainda referenciar os construtores para criarmos novas instâncias, como se fosse um *factory*, assim:

{% highlight java %}
//Com construtor padrão
Supplier<Author> factory = Author::new;
Author semNome = factory.get();

//Com contrutor que recebe um argumento
Function<String, Author> fac = Author::new;
Author caique = fac.apply("Caique Jhones");
{% endhighlight %}

Para criarmos uma instância, passamos o *method reference* `Author::new` para uma interface funcional que será responsável por devolver a nova instância, no caso de um construtor padrão utilizamos a interface `java.util.function.Supplier`, para um construtor com um argumento podemos utilizar a interface `java.util.function.Function` e usamos o método `apply` passando o nosso parâmetro. Podemos ainda utilizar a interface `java.util.function.BiFunction`, para casos onde temos dois parâmetros, evidentemente a API não supre todos os casos possíveis, mas nada impede que nós mesmos criarmos as interfaces. Os arrays também não ficaram de fora, para usarmos o *method reference* utilizamos a sintaxe `array[]::new`, a novidade aqui é que ganha-se os colchetes, exemplo: `float[]::new`.

Além disso podemos ainda referenciar um métodos da classe mãe, com um `super::nomeDoMetodo` e métodos estáticos como `Integer::parseInt`. Vale salientar que para cada operação desta, deve-se ter uma interface funcional que será a referência, aqui vimos algumas, mas existem diversas outras como: `java.util.function.ToIntFunction`, `java.util.function.ToIntBiFunction` e outras variações dos tipos primitivos, que evitam o *autoboxing* para este tipos. Contudo na maioria dos casos não nos preocuparemos com isso, já que o *method reference* será passado como argumento em vários métodos.

Neste tutorial vimos uma parte importante do Java 8, a partir daqui poderemos compreender como funciona a nova API de Stream e todas as novas funcionalidades e vantagens que a API Collection implementou.