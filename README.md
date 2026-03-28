# webhook-inspect

README simplificado com instruções básicas para instalar e rodar o projeto.

## Visão geral

Monorepo com duas workspaces:
- `api` — backend em TypeScript (Fastify, Drizzle ORM, Postgres)
- `web` — frontend em React + Vite

O propósito do projeto é receber e inspecionar webhooks, persistir/mostrar entradas e fornecer uma UI para visualização.

## Tecnologias principais

- Node.js (pnpm workspaces)
- TypeScript
- Fastify (servidor HTTP)
- Drizzle ORM (migrations / acesso a Postgres)
- Postgres (`pg`)
- Zod (validação de schemas)
- React + Vite (frontend)

## Pré-requisitos

- Node.js (versão compatível com dependências)
- pnpm (o `package.json` da raiz indica uma versão recomendada)
- Postgres (quando utilizar persistência)
- Git (opcional)

## Instalação

Na raiz do projeto (usa workspaces):

pnpm install

(ou instale separadamente em `api` e `web` se preferir)

## Variáveis de ambiente

Crie um arquivo `.env` em `api/` com as variáveis necessárias (exemplo):

- `DATABASE_URL` — string de conexão com Postgres
- Outras variáveis configuradas no código da API

A localização e nomes exatos dependem da implementação no diretório `api`.

## Rodando em desenvolvimento

Rodar ambos os workspaces em terminais separados:

1) Backend (API)
cd api
pnpm install
pnpm dev

2) Frontend (Web)
cd web
pnpm install
pnpm dev

Também é possível instalar tudo pela raiz com `pnpm install` e então executar os comandos de cada workspace.

## Build / Produção (resumo)

Frontend:
cd web
pnpm build
Sirva os arquivos estáticos gerados conforme seu ambiente (Nginx, Vercel, etc).

Backend:
Garanta que a API esteja compilada/empacotada para produção (conforme sua pipeline).
O `package.json` do `api` tem um `start` que aponta para `dist/server.js` — execute `node dist/server.js` ou use o processo que sua infra exigir.

## Migrations e banco de dados

O workspace `api` utiliza `drizzle-kit`. Exemplos de comandos (rodar dentro de `api`):

- pnpm db:generate  # gerar migrations
- pnpm db:migrate   # aplicar migrations
- pnpm db:studio    # abrir studio do drizzle

Verifique a configuração de `drizzle-kit` e os scripts no `api/package.json` para detalhes.

## Estrutura geral

- `api/` — código do servidor, rotas, acesso a banco, migrations
- `web/` — aplicação React (Vite)
- `package.json` (raiz) — workspaces e gerenciador de pacotes

## Uso

- Envie webhooks para o endpoint exposto pela API (ver rotas em `api/src`).
- Abra a UI em `web` para visualizar/inspecionar entradas (dependendo da implementação).

## Contribuição

1. Crie uma branch a partir de `main`.
2. Abra um Pull Request com descrição clara das mudanças.
3. Adicione testes/descrição quando aplicável.

## Licença

Sem licença definida. Adicione um arquivo `LICENSE` conforme a política do projeto.

## Observações finais

Se quiser, posso:
- Adicionar exemplos de `.env`
- Documentar endpoints existentes (preciso dos arquivos da `api`)
- Criar instruções de deploy mais detalhadas
