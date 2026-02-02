---
data: 30-01-2026
disciplina: Projeto de bloco Engenharia de Software Escaláveis
professor: Leonardo Silva da Gloria
topicos:
  - Spring Boot
  - ResponseEntity
  - HttpHeaders
  - Status Code
---

# 🎓 Aula: Introdução ao Spring Boot e Controle de Resposta (ResponseEntity)

> [!abstract] Visão Geral
> Nesta aula, o professor Leonardo explicou a filosofia do **Spring Boot** (reduzir atrito de configuração) e focou na manipulação correta de respostas HTTP usando a classe `ResponseEntity`. O objetivo foi mostrar como sair do retorno padrão (JSON 200 OK) e ter controle total sobre o Status Code e Headers da aplicação.

---

## 💡 Conceitos e Exemplos Práticos

### 1. O que é o Spring Boot?
O professor definiu o Spring Boot como um "facilitador" ou um "guarda-chuva" que agrupa diversos frameworks.
- **Objetivo:** Reduzir o atrito de configuração ("Convention over Configuration").
- **Boot:** Cuida da inicialização e configuração automática das dependências (Tomcat embutido, conversão JSON, etc.), permitindo que o dev foque na regra de negócio.

### 2. ResponseEntity (O Coração da Resposta HTTP)
A maior ênfase da aula foi no uso do `ResponseEntity`. Em vez de retornar o objeto puro (que o Spring converte para JSON com status 200 por padrão), devemos usar `ResponseEntity` para customizar a resposta.

**Por que usar?**
Para controlar o **Status Code** (ex: 201, 404, 410) e os **Headers** da requisição.

**Exemplo Prático (Java):**
```java
@RestController
@RequestMapping("/api")
public class ExemploController {

    // ❌ Forma Simples (Menos controle)
    @GetMapping("/simples")
    public String ola() {
        return "Olá Mundo"; // Sempre retorna 200 OK
    }

    // ✅ Forma Recomendada (Com ResponseEntity)
    @GetMapping("/controle-total")
    public ResponseEntity<String> olaComControle() {
        // Exemplo: Retornando um status específico (410 Gone) e Headers customizados
        return ResponseEntity
                .status(HttpStatus.GONE) // Status 410
                .header("X-Custom-Header", "ValorPersonalizado") // Header Customizado
                .body("Este recurso não existe mais.");
    }
    
    // ✅ Exemplo de Sucesso (201 Created)
    @PostMapping("/criar")
    public ResponseEntity<Usuario> criarUsuario(@RequestBody Usuario user) {
        // Lógica de salvar...
        return ResponseEntity
                .status(HttpStatus.CREATED) // 201
                .body(user);
    }
}
````

### 3. Manipulação de Headers e Status

O professor mostrou no inspecionador de rede (Network tab) como o cliente recebe exatamente o que foi configurado no `ResponseEntity`.

- **Status 410 (Gone):** Usado como exemplo de erro ou recurso removido propositalmente.
    
- **Headers:** Podem ser usados para passar metadados, tokens ou informações de controle.
    

---

## 🚨 Ênfase do Professor (Destaques)

1. **Evite Retornos "Crus":** O professor foi enfático: _"Evita dar a resposta sem estar em um ResponseEntity"_. Sempre que precisarmos de granularidade (ex: informar que algo foi criado, ou que houve um erro específico), essa classe é obrigatória.
    
2. **Redução de Atrito:** Entender que o Spring Boot existe para que não precisemos configurar XMLs complexos como antigamente. Ele já traz o servidor (Tomcat) e as bibliotecas prontas.
    
3. **Visualização:** O professor usou o navegador/inspecionador para provar que o status HTTP muda de fato. É importante para quem consome a API (Front-end ou outro serviço) saber se deu 200, 201, 400, etc.
    

---

## 📌 Próximos Passos

- [ ] Praticar o uso de `ResponseEntity.ok()`, `ResponseEntity.created()`, `ResponseEntity.notFound()`.
    
- [ ] Testar endpoints usando Postman ou Insomnia para ver os Headers.