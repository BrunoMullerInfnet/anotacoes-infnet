---
data: 2026-02-03
disciplina: Desenvolvimento de Serviços com Spring Boot
professor: Leonardo Silva da Gloria
topicos:
  - "[Arquitetura em Camadas, Service Pattern, Injeção de Dependência, Controller vs Service]"
tags:
  - "#spring-boot"
  - clearArchitecture
  - backend
  - java
---
# 🎓 Aula Prática: Arquitetura de Camadas e Injeção de Dependência

> [!abstract] Visão Geral
> Nesta aula prática, o foco saiu de "apenas fazer funcionar" para "organizar a casa". O professor estruturou o projeto separando as responsabilidades em **Controller**, **Service** e **Repository**, e demonstrou a forma correta de conectar essas camadas usando **Injeção de Dependência via Construtor** (abandonando o `@Autowired` em atributos).

---

## 🏛️ O Conceito: Arquitetura em Camadas (Separation of Concerns)

O professor enfatizou que **o Controller não deve ter regra de negócio**. Ele deve ser "burro" (thin controller), servindo apenas como um guarda de trânsito HTTP.

### 1. A Estrutura Ideal
* **Controller (`@RestController`):**
    * **Responsabilidade:** Receber a requisição HTTP, validar o DTO de entrada e devolver a resposta (`ResponseEntity`).
    * **O que NÃO faz:** Não acessa banco de dados, não calcula impostos, não valida regras complexas.
* **Service (`@Service`):**
    * **Responsabilidade:** O coração da aplicação. Contém toda a lógica de negócio ("Se o usuário for VIP, dá desconto").
    * **O que NÃO faz:** Não sabe o que é HTTP (não recebe `HttpServletRequest` nem retorna `ResponseEntity`). Retorna objetos de domínio ou DTOs.
* **Repository (`@Repository`):**
    * **Responsabilidade:** Falar com o banco de dados (SQL/JPA).
    * **O que NÃO faz:** Regra de negócio.

---

## 💉 Aprofundando: Injeção de Dependência (A Maneira Correta)

Um dos pontos de maior ênfase nas aulas práticas modernas de Spring.

### O Problema do `@Autowired` em Atributos (Field Injection)
Muitos tutoriais antigos ensinam assim:
```java
// ❌ MÁ PRÁTICA (Field Injection)
@Service
public class UsuarioService {
    @Autowired // O professor deve ter criticado isso
    private UsuarioRepository repository;
}
````

- **Por que é ruim?**
    
    1. Esconde dependências (você não vê o que a classe precisa para funcionar).
        
    2. Dificulta testes unitários (você é obrigado a usar Reflection ou frameworks pesados para mocar o repository).
        
    3. Permite mutabilidade (o atributo não pode ser `final`).
        

### A Solução: Injeção via Construtor (Constructor Injection)

Esta é a forma que o professor prioriza para um código profissional:

Java

```java
// ✅ BOA PRÁTICA (Recomendada na aula)
@Service
public class UsuarioService {

    // 1. Atributo 'final' garante imutabilidade (ninguém troca o repository no meio da execução)
    private final UsuarioRepository repository;

    // 2. O Spring entende que precisa injetar aqui, mesmo sem @Autowired
    public UsuarioService(UsuarioRepository repository) {
        this.repository = repository;
    }
}
```

---

## 💻 Exemplo Prático Completo (Conectando as Pontas)

Destrinchando o fluxo que foi codificado na aula: **Controller chama Service, que chama Repository**.

### 1. O Service (Regra de Negócio)

Note que ele não sabe que existe HTTP/Web. Ele só processa dados.

Java

```java
@Service
public class UsuarioService {
    
    private final UsuarioRepository repository;

    public UsuarioService(UsuarioRepository repository) {
        this.repository = repository;
    }

    public UsuarioDTO criarUsuario(UsuarioDTO dados) {
        // Regra de negócio: Verificar se email já existe
        if (repository.existsByEmail(dados.email())) {
            throw new IllegalArgumentException("Email já cadastrado");
        }
        
        // Converte DTO -> Entity (Omitido para brevidade)
        Usuario entidade = new Usuario(dados);
        
        // Salva no banco
        Usuario salvo = repository.save(entidade);
        
        return new UsuarioDTO(salvo);
    }
}
```

### 2. O Controller (Orquestrador)

Ele injeta o Service (não o Repository!) e usa o `ResponseEntity` visto na aula anterior.

Java

```java
@RestController
@RequestMapping("/usuarios")
public class UsuarioController {

    private final UsuarioService service; // Injeção do Service

    public UsuarioController(UsuarioService service) {
        this.service = service;
    }

    @PostMapping
    public ResponseEntity<UsuarioDTO> criar(@RequestBody UsuarioDTO dto) {
        // Delega a lógica para o service
        UsuarioDTO novoUsuario = service.criarUsuario(dto);
        
        // Retorna o status correto (201 Created)
        return ResponseEntity.status(HttpStatus.CREATED).body(novoUsuario);
    }
}
```

---

## 🚨 Ênfases do Professor (Pontos de Atenção)

1. **Testabilidade:** O código foi escrito dessa forma (com construtores) para facilitar os testes. _"Se eu quiser testar o Service, eu posso dar um 'new UsuarioService(mockRepository)' sem precisar subir o Spring inteiro."_
    
2. **Semântica:** Cada classe tem um sufixo que diz o que ela faz (`Controller`, `Service`, `Repository`). Isso ajuda na manutenção.
    
3. **Segurança e DTOs:** Reforçou-se o uso de DTOs (`Records`) para trafegar dados entre o Controller e o Service, nunca expondo a Entidade JPA diretamente no JSON de resposta.
    

---

## 📌 Próximos Passos

- [ ] Refatorar os códigos antigos trocando `@Autowired` por Construtores.
    
- [ ] Garantir que nenhum Controller esteja chamando Repository diretamente.
    
- [ ] Estudar tratamento de exceções globais (`@ExceptionHandler`) para capturar os erros lançados pelo Service.