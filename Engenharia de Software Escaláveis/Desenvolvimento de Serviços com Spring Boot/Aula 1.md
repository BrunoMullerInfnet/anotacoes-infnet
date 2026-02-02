---
tags:
  - java
  - jvm
  - spring-boot
  - hibernate
  - arquitetura
  - clean-code
  - backend
  - historia-da-computacao
data: 27-01-2026
assunto: Evolução do Java e Ecossistema Spring
professor: Leonardo Silva da Gloria
---
# Evolução do Java: Da JVM ao Spring Boot

## ☕ Fundamentos do Java e JVM
O Java foi projetado com a filosofia "Write Once, Run Anywhere".
* **Compilação**: O código Java não vira código de máquina diretamente; ele vira **Byte Code**.
* **Execução**: A **JVM (Java Virtual Machine)** interpreta esse Byte Code e se comunica com o hardware.
* **Vantagem**: A única exigência do hardware é suportar a JVM. Isso permitiu que o Java rodasse em diversos dispositivos e dominasse os servidores corporativos.

![[Pasted image 20260127074939.png]]

---

## 🛠️ Evolução das Ferramentas (Resolvendo Dores Antigas)

### 1. Hibernate (A Ponte ORM)
Resolveu o "abismo" entre a Orientação a Objetos e o Banco de Dados Relacional.
* **O Problema**: Java usa Classes, Herança e Polimorfismo. Bancos usam Tabelas, Linhas e Colunas.
* **A Solução (ORM)**: O Hibernate automatiza o mapeamento, eliminando a necessidade de escrever SQL para operações básicas.

![[Pasted image 20260127075810.png]]

### 2. Struts (Organização MVC Antiga)
Veio para organizar a bagunça dos anos 2000 (arquivos JSP).
* **Antes**: HTML (Design), Java (Lógica) e SQL (Dados) misturados em um único arquivo. Manutenção impossível.
* **Com Struts**: Separou a interface da lógica de navegação.

![[Pasted image 20260127080044.png]]

---

## 🌱 A Era Spring e o Conceito de Beans

Com o tempo, o **Spring Boot** surgiu para simplificar ainda mais a configuração e o desenvolvimento.

![[Pasted image 20260127080911.png]]

### Diferença entre Java Bean vs. Spring Bean

| Característica | **Java Bean (Convenção Clássica)** | **Spring Bean (Conceito Moderno)** |
| :--- | :--- | :--- |
| **Definição** | Uma classe seguindo regras de escrita. | Um objeto gerenciado pelo Framework. |
| **Regras** | 1. Construtor vazio.<br>2. Atributos privados.<br>3. Getters e Setters. | Anotado (ex: `@Bean`, `@Service`). O Spring gerencia o ciclo de vida (IoC). |
| **Objetivo** | Permitir que ferramentas visuais manipulassem o objeto. | Inversão de Controle e Injeção de Dependência. |

> [!INFO] Inversão de Controle (IoC)
> No Spring, você não dá `new Objeto()`. Você avisa ao Spring que a classe é um Bean, ele cria, guarda no container e te entrega pronto.

![[Pasted image 20260127084751.png]]

---

## 🏷️ Principais Annotations do Spring

A partir do Java 5, as anotações substituíram configurações complexas em XML.

### 1. `@Repository` (Camada de Dados)
* Transforma a classe em um Bean.
* **Diferencial**: Traduz exceções técnicas do SQL para exceções amigáveis do Spring (DataAccessException).

### 2. `@Service` (Camada de Negócio)
* Indica onde reside a lógica de negócio e regras do sistema.
* Semanticamente organiza o código (sabe-se que ali não é controller nem repositório).

### 3. `@Autowired` (Injeção de Dependência)
* Conecta os Beans. O Spring procura uma instância compatível no container e injeta automaticamente.

![[Pasted image 20260127085726.png]]

---

## 🧹 Spring e Clean Code
O uso correto das anotações promove práticas de código limpo:

1.  **Separação de Preocupações (SoC)**: Ao ver `@Service`, sabe-se a responsabilidade da classe (Princípio SRP).
2.  **Fim do Boilerplate**: Eliminação de XMLs gigantescos de configuração. O código é autodescritivo.
3.  **Baixo Acoplamento**: Com `@Autowired` (Inversão de Dependência), a classe `A` não precisa saber *como* criar a classe `B`, apenas que precisa dela.
4.  **Foco no Domínio**: O arquivo `.java` foca na regra de negócio, não em abrir/fechar conexões de banco.

![[Pasted image 20260127090337.png]]

### Ciclo de Vida de um Bean
![[Pasted image 20260127091037.png]]