# Dev Container - .NET 8.0 Template

Objetivo principal – Oferecer um ponto de partida **pronto‑para‑usar** que cria, de forma automática, um ambiente de desenvolvimento consistente e reproduzível dentro de um dev container (VS Code Remote Containers). Tudo que você precisa está descrito neste README.

## Configuração - [devcontainer.json](./.devcontainer/devcontainer.json)

### Exemplo

```json
{
  "name": "C# (.NET)",
  "image": "mcr.microsoft.com/devcontainers/dotnet:1-8.0-bookworm",
  "features": {
    "ghcr.io/devcontainers/features/docker-outside-of-docker:1": {},
    "ghcr.io/devcontainers/features/node:latest": {},
    "ghcr.io/devcontainers/features/dotnet:2": {
      "version": "8.0"
    }
  }
}
```

### Descrição

| **Item**                     | **Descrição**                                                                                                                                         | **Utilidade**                                                                                                                   |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| **name**                     | Nome amigável que aparece na barra inferior do VS Code quando o container está ativo.                                                                 | Identifica rapidamente o tipo de ambiente.                                                                                      |
| **image**                    | Imagem base oficial da Microsoft para .NET 8 (bookworm = Debian 12).                                                                                  | Garante que todas as ferramentas do SDK 8.0 estejam disponíveis sem precisar instalar nada localmente.                          |
| **docker-outside-of-docker** | Habilita o Docker‑in‑Docker (DinD) de modo “outside‑of‑docker”. Permite que você execute comandos docker dentro do container usando o daemon do host. | Ideal para compilar imagens, rodar testes que dependem de containers ou usar ferramentas como docker compose.                   |
| **node**                     | Instala a última versão LTS do Node.js e npm.                                                                                                         | Suporta builds front‑end, scripts de automação, ferramentas como webpack, eslint, ou testes unitários em JavaScript/TypeScript. |
| **dotnet (versão 8.0)**      | Garante que o SDK/.NET Runtime 8.0 esteja instalado (mesmo que já venha na imagem base).                                                              | Evita incompatibilidades caso a imagem base seja atualizada para outra versão no futuro.                                        |

Nota: *As features são mantidas pelo projeto devcontainers e recebem atualizações de segurança automaticamente e demais features podem ser obtidas [aqui](https://containers.dev/features).*

## Como usar este repositório?

### Clonar com SSH

```bash
git clone git@github.com:juninolv/devcontainer-dotnet-template.git
cd devcontainer-dotnet-template
```

### Clonar com HTTP

```bash
git clone https://github.com/juninolv/devcontainer-dotnet-template.git
cd devcontainer-dotnet-template
```

*Se estiver criando um novo projeto, basta clicar em “Use this template” no GitHub e escolher o nome do seu repositório.*

### Abra no VS Code com Remote Containers

1. Instale a extensão "Remote - Containers" (ou Dev Containers) se ainda não o fez.
2. No VS Code, abra a pasta raiz do projeto.
3. Quando a barra inferior indicar “Reopen in Container”.
4. O VS Code vai:
    - Baixar a imagem configurada (se ainda não existir).
    - Aplicar as features.
    - Montar o código-fonte dentro do container.

### Teste o ambiente

```bash
dotnet --info
node --version
docker version
```

## Dicas

| Tema                  | Como fazer                                                                                                                                         |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| Persistir volumes     | Monte diretórios externos no devcontainer.json usando a propriedade mounts.                                                                        |
| Customizar a imagem   | Crie um Dockerfile dentro de .devcontainer/ e referencie‑o com "dockerFile": "Dockerfile" ao invés de "image".                                     |
| Variáveis de ambiente | Defina "runArgs": ["-e", "MY_VAR=valor"] ou use "containerEnv" no JSON.                                                                            |
| Debugging             | Pressione F5 no VS Code; o debugger já está configurado para .NET 8 dentro do container.                                                           |
| CI/CD                 | Reuse o mesmo devcontainer.json nas pipelines (GitHub Actions, GitLab CI) para garantir que os testes rodem no mesmo ambiente que o desenvolvedor. |

## Contribuindo

Sempre siga as boas práticas de contribuição do repositório original.

[Licença](./LICENSE)

Distribuído sob a licença MIT – sinta‑se livre para usar, modificar e distribuir conforme suas necessidades.
