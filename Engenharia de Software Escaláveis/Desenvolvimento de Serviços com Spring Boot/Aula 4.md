---
data: 2026-02-05
disciplina: Desenvolvimento de Serviços com Spring Boot
professor: Leonardo Silva da Gloria
topicos:
  - "[Bean Validation, @Valid, @RequestHeader, Status Code, Headers]"
tags:
  - SpringBoot
  - Validation
  - RestAPI
  - CleanCode
---
# 🎓 Aula: Validação Automática e Manipulação de Headers

> [!abstract] Visão Geral
> O professor Leonardo avançou na profissionalização da API. O foco saiu do "retornar dados" para o "receber dados com segurança". A aula abordou como substituir verificações manuais (`if (nome == null)`) pelo framework de validação do Spring (**Bean Validation**) e como ler metadados da requisição através de **Headers** HTTP.

---

## 💡 Conceitos e Exemplos Práticos

### 1. Validação Declarativa (Bean Validation)
O professor foi enfático: **"Não é para fazer regra de validação básica com IFs no Controller"**.
Em vez de sujar o código verificando se um ID é negativo ou se um nome está vazio, usamos anotações.

* **Dependência:** `spring-boot-starter-validation`.
* **Como funciona:** Anota-se o DTO (Record ou Class) com as restrições e ativa-se a validação no Controller com `@Valid` ou `@Validated`.

**Exemplo Prático (Java):**
```java
// 1. No DTO (Regras de validação)
public record UsuarioDTO(
    @NotBlank(message = "Nome é obrigatório") 
    String nome,
    
    @Email(message = "Email inválido") 
    String email,
    
    @Positive(message = "Idade deve ser maior que zero") 
    Integer idade
) {}

// 2. No Controller (Ativação)
@PostMapping
// O @Valid diz ao Spring: "Verifique as regras do DTO antes de entrar no método"
public ResponseEntity<UsuarioDTO> criar(@RequestBody @Valid UsuarioDTO dto) {
    return ResponseEntity.ok(dto);
}
````

### 2. Manipulação de Headers (`@RequestHeader`)

Além do corpo (`@RequestBody`) e da URL (`@PathVariable`), muitas vezes precisamos passar metadados via cabeçalho (ex: Tokens, Paginação, Idioma).

- **Uso:** Anotação `@RequestHeader` nos parâmetros do método.
    
- **Exemplo da aula:** O professor demonstrou como pegar página e tamanho para paginação via Header (embora Query Params sejam mais comuns, ele usou para exemplificar o poder dos Headers).
    

**Exemplo Prático (Java):**

```java
@GetMapping("/listar")
public ResponseEntity<List<Usuario>> listar(
    // Pegando valor do Header "X-Page-Number". Se não vier, assume 0.
    @RequestHeader(value = "X-Page-Number", defaultValue = "0") int pagina,
    @RequestHeader(value = "Accept-Language", required = false) String idioma
) {
    System.out.println("Página solicitada: " + pagina);
    System.out.println("Idioma do cliente: " + idioma);
    
    return ResponseEntity.ok(service.buscarTodos(pagina));
}
```

### 3. A Importância dos Status Codes para o Frontend

O professor explicou como o **Frontend (React/Angular)** consome a API.

- **O Erro:** O código cliente (JavaScript) não lê a mensagem de texto "Erro ao salvar".
    
- **A Correção:** O cliente lê o **Status Code** (400, 401, 500).
    
- **Regra:** Se o usuário mandou dados errados (ex: idade negativa), retorne **400 Bad Request**. Se o servidor falhou, **500 Internal Server Error**.
    

---

## 🚨 Ênfases do Professor

1. **Framework de Validação:** "Usem o framework. Se o ID tem que ser maior que zero, use `@Positive`. Não faça if."
    
2. **API é para Máquinas:** "Você não escreve API para humano ler a mensagem de erro, você escreve para o computador entender o Status Code."
    
3. **Headers Customizados:** O uso de headers permite limpar a URL e passar configurações de infraestrutura (como tokens e preferências de localização) de forma transparente.
    

---

## 📌 Próximos Passos

- [ ] Adicionar a dependência `validation` no `pom.xml`.
    
- [ ] Refatorar os DTOs adicionando `@NotBlank`, `@Size`, etc.
    
- [ ] Testar no Insomnia/Postman enviando dados inválidos para ver o status 400.