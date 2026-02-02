---
tags:
  - faculdade
  - engenharia-de-software
  - java
  - design-patterns
  - ddd
  - oop
data: 28-01-2026
professor: Luiz Maia
assunto: Revisão de Orientação a Objetos
---
# Revisão de Orientação a Objetos (OOP)

## 📝 Visão Geral
Nesta aula, o professor Luiz Maia fez uma revisão aprofundada dos conceitos fundamentais de Orientação a Objetos, preparando a turma para os tópicos de SOLID, Design Patterns e DDD. A aula focou nos 4 pilares da POO, com comparações entre Java e C# e exemplos práticos.

## 🏛️ Os 4 Pilares da Orientação a Objetos

### 1. Encapsulamento
* **Conceito**: Proteger atributos e propriedades de acessos indevidos externos à classe.
* **Implementação**:
    * Uso de modificadores de acesso (`private`, `protected`).
    * Atributos devem ser privados e acessados/modificados apenas por métodos da própria classe (Getters/Setters ou métodos de negócio como `move()` e `stop()`).
* **Comparação**: Java/C# possuem encapsulamento forte, enquanto Python não implementa nativamente (apenas convenções).
* **Métodos Privados**: O professor ressaltou que métodos também podem ser privados se forem auxiliares internos e não precisarem ser expostos.



### 2. Herança
* **Conceito**: Criação de subclasses que herdam atributos e métodos de uma superclasse, promovendo reutilização de código.
* **Modificador `protected`**: Permite que subclasses acessem diretamente atributos da superclasse sem passar por métodos públicos.
* **Exemplo Clássico**: Classe `Pessoa` (superclasse) com subclasses `Aluno` (adiciona nota) e `Funcionario` (adiciona cargo).
* **Alerta**: Herança nem sempre é a solução ideal e pode ter problemas se mal utilizada.



### 3. Polimorfismo
O professor dividiu em dois tipos principais:
1.  **Estático (Tempo de Compilação)**:
    * **Sobrecarga (Overloading)**: Métodos com o mesmo nome mas assinaturas diferentes (parâmetros distintos). Ex: Calculadora com múltiplos métodos `somar`.
    * **Sobrecarga de Construtor**: Ter múltiplos construtores na classe.
2.  **Dinâmico (Tempo de Execução)**:
    * **Sobrescrita (Overriding)**: Uso da anotação `@Override`. A subclasse altera o comportamento de um método da superclasse (ex: `toString()`).
    * **Métodos Virtuais**: Métodos implementados na classe abstrata que não obrigam a implementação na subclasse (funcionam como implementação padrão).



### 4. Abstração
* **Conceito**: Identificar quais elementos do mundo real devem virar classes, atributos e métodos no sistema.
* **Dificuldade**: Considerado o pilar mais difícil de dominar, pois depende de experiência e não apenas regras rígidas.
* **Ferramentas**: O uso de UML (Diagrama de Casos de Uso e Diagrama de Classes) ajuda a materializar a abstração antes do código.


## ☕ Java vs C# (.NET)
Durante a aula, houve uma comparação entre os ecossistemas:
* **Java**: Muitas vezes requer integração de vários frameworks separados (Spring, Hibernate, JPA).
* **.NET (C#)**: Ecossistema mais integrado e "pronto para uso", facilitando conexões com nuvem (Azure).
* **Mercado**: Java tem mais vagas (mais concorrido), mas C# tende a ter salários melhores pela menor oferta de profissionais.

## 💻 Exemplos de Código Mencionados
* **Veículo**: Exemplo de encapsulamento com atributo `private boolean moving`.
* **Calculadora**: Exemplo de polimorfismo estático (sobrecarga).
* **Pessoa/Aluno/Funcionário**: Exemplo clássico de herança.
* **Arquivo de Apoio**: `PO.zip` (disponível na pasta da Aula 02) contém os códigos fontes usados.

## 📌 Próximos Passos
* Continuar o estudo para entrar em **SOLID** e **Design Patterns** na sequência.