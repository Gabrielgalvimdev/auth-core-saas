# Auth Core para SaaS

> Servico central de autenticacao e autorizacao para produtos SaaS. Login, renovacao e autorizacao ficam previsiveis, com contrato pronto para novos modulos consumirem.

![Go](https://img.shields.io/badge/Go-1.21-007d9c?logo=go)
![gRPC](https://img.shields.io/badge/gRPC-Protocol-6E5BD0?logo=grpc)
![JWT](https://img.shields.io/badge/JWT-Auth-4f46e5)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ed?logo=docker)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-316192?logo=postgresql)

---

## Contexto e Resultado

Produtos SaaS crescem rapido quando login, permissoes e sessoes ficam espalhados em varios modulos sem contrato claro. Auth Core e a solucao da autenticacao mais versatil completa para SaaS, oferecendo usuarios, organizacoes, permissoes e sessoes com maxima seguranca e escalabilidade.

## O que resolve

- Login, renovacao e autorizacao ficam previsiveis
- Contrato pronto para novos modulos consumirem
- Tokens central e renovacao previsivel
- Conversas entre servicos por auditoria

---

## Arquitetura

```text
Web App  ->  Auth Service  ->  Token Store  ->  Servicos Internos
```

---

## Funcionalidades

- Login com usuario e senha
- Refresh token isolado
- Autorizacao baseada em JWT
- Organizacoes e contas
- Permissoes e roles
- Sessoes auditaveis
- Renovacao automatica de token
- Testes de contrato entre servicos

---

## Decisoes Tecnicas

- **JWT de curta duracao**: acess token valida por poucos minutos
- **Refresh token isolado**: token separado, armazenado com seguranca
- **Limites claros entre auth e dominio**: Auth Core nao conhece regras de negocio
- **Token Store centralizado**: redis para revogacao e auditoria
- **gRPC entre servicos**: comunicacao tipada e rapida

---

## Metricas

| Indicador | Meta |
|-----------|------|
| Login no p95 | abaixo de 300ms |
| Endpoints criticos | cobertos por teste de contrato |

---

## Como rodar localmente

### Pre-requisitos

- Go >= 1.21
- Docker e Docker Compose
- PostgreSQL

### Subir com Docker Compose

```bash
# Subir todos os servicos
docker compose up -d

# Ver logs
docker compose logs -f auth
```

### Rodar testes

```bash
go test ./...

# Testes de contrato
go test ./contracts/...
```

### Build

```bash
go build -o auth-core ./cmd/auth
```

---

## Estrutura do projeto

```
auth-core-saas/
├── cmd/              # Binario principal
├── internal/         # Logica interna
│   ├── domain/      # Entidades e regras
│   ├── handlers/    # HTTP handlers
│   ├── usecases/    # Casos de uso
│   └── grpcs/      # Servicos gRPC
├── pkg/              # Pacotes publicos
├── contracts/        # Testes de contrato
├── docker/           # Dockerfiles e config
├── go.mod
├── docker-compose.yml
├── .env.example
├── .gitignore
├── LICENSE
└── README.md
```

---

## Variaveis de ambiente

```env
# Server
PORT=8080
GRPC_PORT=9090
ENV=development

# Database
DATABASE_URL=postgresql://user:pass@localhost:5432/auth_core?sslmode=disable

# JWT
JWT_SECRET=sua-chave-secreta
JWT_EXPIRY=15m
REFRESH_TOKEN_EXPIRY=7d

# Redis (Token Store)
REDIS_URL=redis://localhost:6379/0

# Logging
LOG_LEVEL=info
```

---

## Evidencia pratica

- Diagrama de fluxo de login e refresh
- Testes de contrato planejados
- Roteiro visual de login e tokens
- Exemplo com Docker Compose

---

## Autor

Desenvolvido por **Gabriel Galvim**

[GitHub](https://github.com/Gabrielgalvimdev) | [LinkedIn](https://linkedin.com/in/gabriel-galvim)

---

*Autenticacao SaaS centralizada, segura e escalavel.*
