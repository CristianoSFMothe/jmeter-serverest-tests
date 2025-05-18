# 🧪 Testes de API com Apache JMeter — Serverest

Este repositório contém um plano de teste construído com o **Apache JMeter** para testar a API [Serverest.dev](https://serverest.dev/), cobrindo todo o ciclo de vida de um usuário: criação, consulta, atualização e remoção.

---

## 📁 Estrutura do Teste

```text
Serverest
├── Usuários
│   └── Fluxo - GET > POST > GET(id) > PUT(id) > GET(id) > DELETE(id)
│       ├── GET - Listar usuários
│       ├── POST - Cadastrar usuário
│       ├── GET(id) - Buscar usuário cadastrado
│       ├── PUT(id) - Atualizar usuário
│       ├── GET(id) - Verificar atualização
│       ├── DELETE(id) - Remover usuário
│
├── GET retornar todos usuários (Agregador)
│   └── GET retornar todos usuários
│       ├── GET > https://serverest.dev/usuarios
│       └── Status Code
├── Constant Timer
|
├── POST cadastrar usuário - sucesso (Agregador)
│   └── POST cadastrar usuário - sucesso
│       ├── POST > https://serverest.dev/usuarios
│       │   ├── Status Code
│       │   └── ID do Usuário (JSON Extractor)
│       └── Response Message (opcional)
├── Constant Timer
|
├── GET retornar usuário ID (Agregador)
│   └── GET retornar usuário ID
│       ├── GET > https://serverest.dev/usuarios/${id}
│       └── Status Code
├── Constant Timer
|
├── PUT atualizar usuário (Agregador)
│   └── PUT atualizar usuário
│       ├── PUT > https://serverest.dev/usuarios/${id}
│       └── Status Code
├── Constant Timer
|
├── GET retornar usuário atualizado (Agregador)
│   └── GET retornar usuário atualizado
│       ├── GET > https://serverest.dev/usuarios/${id}
│       └── Status Code
├── Constant Timer
|
├── DELETE usuário cadastrado (Agregador)
│   └── DELETE usuário cadastrado
│       ├── DELETE > https://serverest.dev/usuarios/${id}
│       └── Status Code
│
├── Debug Sampler
├── View Results Tree
├── View Results in Table
├── Aggregate Report
├── Summary Report
└── jp@gp - Active Threads Over Time
```

---

## ⚙️ Pré-requisitos

- [Java 8+](https://www.oracle.com/java/technologies/javase-downloads.html)
- [Apache JMeter 5.6.3](https://jmeter.apache.org/download_jmeter.cgi)

---

## 🚀 Como executar

1. Clone o repositório:

   ```bash
   git clone https://github.com/CristianoSFMothe/jmeter-serverest-tests.git
   cd jmeter-serverest-tests
   ```

2. Abra o Apache JMeter.

3. Vá em **File > Open** e selecione o arquivo:

   ```
   POST - Cadastrado.jmx
   ```

4. Clique no botão **Iniciar (▶️)** para executar os testes.

---

## 🔁 Configuração de carga

O grupo de threads (Thread Group) está configurado para simular múltiplos usuários com os seguintes parâmetros:

- **Number of Threads (users):** 5
- **Ramp-up Period (seconds):** 10
- **Loop Count:** 3
- **Duration (seconds):** 30

---

## 🧠 Estratégias utilizadas

- **JSON Extractor** para capturar dinamicamente o `_id` do usuário após o `POST`
- **Variáveis dinâmicas** reutilizadas em `GET`, `PUT` e `DELETE` com `${id}`
- **Constant Timer** entre requisições para evitar colisões
- **Agregadores** para organizar os resultados por operação
- **Debug Sampler** para auxiliar em inspeções manuais

---

## ✅ Melhorias possíveis

- Gerar e-mails únicos automaticamente para evitar duplicações
- Adicionar lógica condicional para cenários de falha
- Exportar os resultados em `.jtl` para geração de relatórios

---

## 🧑‍💻 Autor

**Cristiano Mothe**
🔗 [GitHub](https://github.com/CristianoSFMothe)

---

## 📄 Licença

Este projeto está licenciado sob a [MIT License](LICENSE).
