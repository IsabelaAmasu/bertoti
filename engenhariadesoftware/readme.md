**✨Texto I:**

O primeiro texto explica que a programação e a ciência da computação estão mais relacionadas à criação de códigos e ao estudo teórico dos sistemas. Já a engenharia de software se preocupa em aplicar métodos organizados e bem planejados para desenvolver sistemas confiáveis que funcionem no dia a dia. Além disso, o texto ressalta que, como o software se tornou essencial em muitas áreas da nossa vida, é necessário usar práticas mais profissionais e estruturadas, parecidas com as utilizadas em outras áreas da engenharia.

**✨Texto II:**

O segundo texto afirma que engenharia de software vai além de simplesmente escrever código; ela envolve acompanhar todo o ciclo de vida do software, garantindo que ele continue útil, funcional e sustentável. O texto também aponta três ideias principais:

* **Tempo e mudança:** o software deve ser capaz de evoluir e se adaptar com o tempo;
* **Escala e crescimento:** a organização do projeto precisa permitir expansão;
* **Custos e escolhas:** é necessário tomar decisões equilibradas entre benefícios e gastos.

---

**🧠Trade-offs:**

1. **Rapidez no desenvolvimento vs. Qualidade do código:**
   Quando a prioridade é entregar rápido, o time pode acabar escrevendo um código menos organizado e com pouca verificação. Isso pode facilitar no início, mas causa problemas e aumenta o custo de manutenção depois.

2. **Desempenho vs. Facilidade de entender o código:**
   Melhorar ao máximo o desempenho de um software pode exigir soluções mais complexas. Essas soluções deixam o sistema mais rápido, porém dificultam que outras pessoas entendam e modifiquem o código no futuro.

3. **Flexibilidade vs. Padronização:**
   Permitir que cada cliente personalize o sistema aumenta a satisfação do usuário, mas também faz o software ficar mais complicado de atualizar e manter, porque cada versão pode se comportar de forma diferente.

---

**Diagramas**

![Atividade 4 - Eng de Software](https://github.com/user-attachments/assets/8087213c-c4d8-4097-a6c1-26393cd0e61c)

<img width="982" height="308" alt="diagramaUML" src="https://github.com/user-attachments/assets/8e652292-69ed-447c-aeff-7bf606e0309d" />

---

**Códigos em Java**

**Livros**

```bash
package LivrariaCentral;

public class Livro {

    private String titulo;
    private float preco;

    public Livro(String titulo, float preco){
        this.preco = preco;
        this.titulo = titulo;
    }

    public String getTitulo(){
        return this.titulo;
    }

    public float getPreco(){
        return this.preco;
    }

    public void setTitulo(String titulo){
        this.titulo = titulo;
    }

    public void setPreco(float preco){
        this.preco = preco;
    }

}
```
**Pedido**

```bash
package LivrariaCentral;

import java.util.List;
import java.util.LinkedList;

public class Pedido {
    private List<Livro> livros = new LinkedList<Livro>();

    public void addLivro(List<Livro> livros){
        for(Livro livro : livros){
            this.livros.add(livro);
        }
    }

    public List<Livro> getLivros(){
        return this.livros;
    }

    public List<Livro> getLivroPeloTitulo(String titulo){
        List<Livro> resultado = new LinkedList<Livro>();
        for(Livro livro : this.livros){
            if (livro.getTitulo().equals(titulo)){
                resultado.add(livro);
            }
        }
        return resultado;
    }
}
```

**Lanches**

```bash
package FatecLanches;

public class Lanche {

    private String nome;
    private float valor;

    public Lanche(String nome, float valor){
        this.valor = valor;
        this.nome = nome;
    }

    public String getNome(){
        return this.nome;
    }

    public float getValor(){
        return this.valor;
    }

    public void setNome(String nome){
        this.nome = nome;
    }

    public void setValor(float valor){
        this.valor = valor;
    }

}
```

**Pedido**

```bash
package FatecLanches;

import java.util.List;
import java.util.LinkedList;

public class Pedido {
    private List<Lanche> produtos = new LinkedList<Lanche>();

    public void addProduto(List<Lanche> produtos){
        for(Lanche produto : produtos){
            this.produtos.add(produto);
        }
    }

    public List<Lanche> getProdutos(){
        return this.produtos;
    }

    public List<Lanche> getProdutoPeloNome(String nome){
        List<Lanche> resultado = new LinkedList<Lanche>();
        for(Lanche produto : this.produtos){
            if (produto.getNome().equals(nome)){
                resultado.add(produto);
            }
        }
        return resultado;
    }
}
```

---

**Testes Automatizados**

```bash
package LivrariaCentral;

import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;
import java.util.List;

public class Teste {

    @Test
    void testAdicionarLivro() {
        Pedido pedido = new Pedido();
        Livro livro = new Livro("O Pequeno Príncipe", 25);

        pedido.addLivro(List.of(livro));
        assertEquals(1, pedido.getLivros().size());
    }

    @Test
    void testBuscarLivros(){
        Pedido pedido = new Pedido();
        Livro romance = new Livro("Orgulho e Preconceito", 30);
        Livro ficcao = new Livro("1984", 28);

        pedido.addLivro(List.of(ficcao));
        pedido.addLivro(List.of(romance));

        assertEquals(2, pedido.getLivros().size());

        for (Livro livro : pedido.getLivros()){
            System.out.printf("Livro: %s \nPreço: R$ %.2f\n\n", livro.getTitulo(), livro.getPreco());
        }
    }

    @Test
    void testBuscarLivroPeloTitulo(){
        Pedido pedido = new Pedido();
        Livro romance = new Livro("Orgulho e Preconceito", 30);
        Livro ficcao = new Livro("1984", 28);

        pedido.addLivro(List.of(ficcao));
        pedido.addLivro(List.of(romance));

        assertEquals(2, pedido.getLivros().size());

        for (Livro livro : pedido.getLivroPeloTitulo("1984")){
            System.out.printf("Livro: %s \nPreço: R$ %.2f\n\n", livro.getTitulo(), livro.getPreco());
        }
    }
}
```

```bash
package FatecLanches;

import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;
import java.util.List;

public class Teste {

    @Test
    void testAdicionarProduto() {
        Pedido pedido = new Pedido();
        Lanche produto = new Lanche("Lanche", 10);

        pedido.addProduto(List.of(produto));
        assertEquals(1, pedido.getProdutos().size());
    }

    @Test
    void testBuscarProdutos(){
        Pedido pedido = new Pedido();
        Lanche salada = new Lanche("X-Salada", 11);
        Lanche burguer = new Lanche("X-Burguer", 10);

        pedido.addProduto(List.of(burguer));
        pedido.addProduto(List.of(salada));

        assertEquals(2, pedido.getProdutos().size());

        for (Lanche lanche : pedido.getProdutos()){
            System.out.printf("Lanche: %s \nValor: R$ %.2f\n\n", lanche.getNome(), lanche.getValor());
        }
    }

    @Test
    void testBuscarProdutoPeloNome(){
        Pedido pedido = new Pedido();
        Lanche salada = new Lanche("X-Salada", 11);
        Lanche burguer = new Lanche("X-Burguer", 10);

        pedido.addProduto(List.of(burguer));
        pedido.addProduto(List.of(salada));

        assertEquals(2, pedido.getProdutos().size());

        for (Lanche lanche : pedido.getProdutoPeloNome("X-Salada")){
            System.out.printf("Lanche: %s \nValor: R$ %.2f\n\n", lanche.getNome(), lanche.getValor());
        }
    }
}
```
