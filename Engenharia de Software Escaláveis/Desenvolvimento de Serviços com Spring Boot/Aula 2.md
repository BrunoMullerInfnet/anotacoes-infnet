---
data: 2026-01-29
disciplina: Desenvolvimento de Serviços com Spring Boot
professor: Leonardo Silva da Gloria
topicos: [Java Moderno, Records, Optionals, Streams API, Lambdas]
---
# 🎓 Resumo da Aula: Java Moderno no Spring Boot

> [!abstract] Visão Geral
> A aula foi uma revisão técnica das funcionalidades introduzidas no **Java 14, 16 e 17** que são essenciais para o desenvolvimento com **Spring Boot 3**. O professor codificou ao vivo para demonstrar como substituir padrões antigos ("velho testamento") por abordagens modernas e funcionais.

---

## 🔝 Tópicos Mais Comentados e Exemplos Práticos

### 1. Records (Java 14+)
O tópico mais enfatizado para a criação de **DTOs** (Data Transfer Objects). O professor explicou que criar classes apenas para transportar dados (com getters, setters, equals, hashcode) é verboso e desnecessário no Java moderno.

**Conceito:** `Records` são classes imutáveis por padrão que geram todo o código repetitivo automaticamente.

**Exemplo Prático (Java):**
```java
// ❌ Como fazíamos antes (Verboso)
public class ClienteDTO {
    private String nome;
    private String email;
    // + Getters, Setters, Construtores, toString, equals, hashCode...
}

// ✅ Como o professor quer (Record)
public record ClienteDTO(String nome, String email) {}

// Uso:
public class Main {
    public static void main(String[] args) {
        var cliente = new ClienteDTO("Ana", "ana@email.com");
        System.out.println(cliente.nome()); // Acesso direto (sem getNome())
    }
}
````

---

### 2. Optional (Tratamento de Nulidade)

O professor criticou o uso excessivo de verificações `if (objeto != null)` e apresentou o `Optional` como a solução semântica para representar a ausência de valor.

**Conceito:** Um contêiner que pode ou não conter um valor não nulo. Evita o `NullPointerException`.

**Exemplo Prático (Java):**

```java
public Optional<ClienteDTO> buscarCliente(Long id) {
    // Simulação de busca no banco
    return Optional.ofNullable(database.find(id));
}

// Uso recomendado na aula (ifPresentOrElse):
public void processar(Long id) {
    buscarCliente(id).ifPresentOrElse(
        cliente -> System.out.println("Processando: " + cliente.nome()),
        () -> System.out.println("Cliente não encontrado!") // Runnable caso vazio
    );
}
```

---

### 3. Streams API e Programação Funcional

Foi mostrado como manipular coleções de dados de forma declarativa (dizendo _o que_ fazer, e não _como_ fazer).

**Conceito:** Pipelines de processamento que suportam operações de filtro, mapeamento e redução. O professor destacou a capacidade de **paralelismo** automático do Java em grandes volumes de dados.

**Exemplo Prático (Java):**

Java

```java
List<String> linguagens = List.of("Java", "Python", "JavaScript", "C#");

// Pipeline: Filtrar nomes com 'J', transformar em Maiúsculas e Imprimir
linguagens.stream()
    .filter(nome -> nome.startsWith("J"))   // Predicate (Filtro)
    .map(String::toUpperCase)               // Function (Transformação)
    .forEach(System.out::println);          // Consumer (Ação Final)
```

---

## 🚨 Ênfase do Professor (O que cai na prova/projeto)

O professor Leonardo destacou explicitamente os pontos críticos para a disciplina:

1. **Semântica é Mandatória:** Não basta o código funcionar. Você precisa saber explicar _por que_ usou um `Record` ou um `Stream`. A intenção do código deve estar clara.
    
2. **Uso Obrigatório:** A frase chave foi: _"Vou querer que vocês usem bastante Stream, Optional e Records. Vamos usar isso o período inteiro."_
    
3. **Adeus ao Boilerplate:** Ele desencorajou fortemente o uso de classes POJO tradicionais para DTOs quando se pode usar Records.
    
4. **Modernização:** O foco é alinhar a turma com o mercado atual que utiliza Spring Boot 3, onde essas práticas de Java 17+ são o padrão.