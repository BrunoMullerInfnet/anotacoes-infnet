---
data: 2026-02-02
disciplina: Design Patterns e Domain-Driven Design (DDD) com Java
professor: Luiz Maia
assunto: "[SOLID, Interfaces, Acoplamento, Coesão, Boas Práticas]"
tags:
  - solid
  - interfaces
  - acomplamento
---
---
# 🎓 Aula 03: Qualidade de Software e SOLID Completo

> [!abstract] Resumo da Aula
> Nesta aula, o professor Luiz Maia aprofundou os conceitos que distinguem um "programador amador" de um profissional. O foco foi a transição do "apenas funcional" para o "arquiteturalmente correto", detalhando métricas de qualidade (Acoplamento/Coesão) e percorrendo todos os cinco princípios do **SOLID**.

---

## 💡 Conceitos de Qualidade de Código

### 1. Acoplamento e Coesão
O professor destacou que um bom design busca o equilíbrio entre esses dois pilares:

* **Acoplamento (Coupling):** Nível de dependência entre classes.
    * **Objetivo:** **Baixo Acoplamento**.
    * **Explicação:** Classes muito dependentes geram um "efeito dominó": você mexe em uma e quebra cinco.
* **Coesão (Cohesion):** Responsabilidade única de cada classe.
    * **Objetivo:** **Alta Coesão**.
    * **Explicação:** Uma classe deve ter um propósito claro. Classes "faz-tudo" (God Classes) são difíceis de testar e manter.

### 2. Interfaces: A Regra de Ouro
A frase da aula foi: **"Programe para uma interface, não para uma implementação"**.
O uso de interfaces permite o polimorfismo e o desacoplamento. Ao usar `List` em vez de `ArrayList`, você garante que seu código funcione com qualquer tipo de lista sem precisar ser alterado.

---

## 🧩 Os 5 Princípios S.O.L.I.D.

O professor apresentou o acrônimo como a base para os Design Patterns que serão estudados:

### S — Single Responsibility Principle (SRP)
**Princípio da Responsabilidade Única**
* "Uma classe deve ter um, e apenas um, motivo para mudar."
* **Exemplo:** Uma classe de `Usuario` não deve conter a lógica de salvar no banco de dados e nem de enviar e-mails de boas-vindas. Essas são responsabilidades de classes de serviço ou repositórios.

### O — Open-Closed Principle (OCP)
**Princípio Aberto-Fechado**
* "Entidades de software devem estar **abertas para extensão**, mas **fechadas para modificação**."
* **Na prática:** Você deve conseguir adicionar novas funcionalidades (como um novo tipo de pagamento) criando novas classes, sem precisar alterar o código que já está funcionando.

### L — Liskov Substitution Principle (LSP)
**Princípio da Substituição de Liskov**
* "As subclasses devem ser substituíveis pelas suas classes base."
* **Explicação:** Se `B` é filho de `A`, eu devo poder usar `B` em qualquer lugar que aceite `A` sem que o programa quebre ou tenha comportamentos inesperados (como um Pinguim que herda de Ave, mas não voa).

### I — Interface Segregation Principle (ISP)
**Princípio da Segregação de Interface**
* "Uma classe não deve ser forçada a implementar interfaces e métodos que não utiliza."
* **Na prática:** É melhor ter várias interfaces pequenas e específicas do que uma interface "gorda" com métodos que nem todas as classes que a implementam precisam.

### D — Dependency Inversion Principle (DIP)
**Princípio da Inversão de Dependência**
* "Dependa de abstrações (interfaces) e não de implementações concretas."
* **Exemplo:** O seu serviço não deve depender de `MySQLRepository`, mas sim de uma interface `IRepository`. Isso permite trocar o banco de dados sem tocar na lógica de negócio.

---

## ⚠️ Ênfases do Professor

1. **Herança vs. Composição:** O professor alertou que a herança cria um acoplamento muito forte ("classe filha fica refém da pai"). A tendência moderna é **priorizar a composição**.
2. **Código para Humanos:** "O computador entende qualquer coisa; o código limpo é para que seu colega de equipe entenda o que você fez daqui a seis meses".
3. **Padrão de Projeto:** Só fazem sentido se você entender o SOLID primeiro. Eles são "receitas" para aplicar esses princípios em problemas comuns.

---

## 📌 Próximos Passos
- [ ] Implementar um exemplo prático de **OCP** usando interfaces.
- [ ] Revisar o projeto de bloco para identificar classes com baixa coesão.