## 🐳 Como Rodar o Projeto com Docker (Individualmente)
Este guia rápido mostrará como construir e executar suas aplicações web e docs usando Docker, criando uma imagem para cada projeto.

Pré-requisitos
Certifique-se de ter o Docker instalado: https://www.docker.com/products/docker-desktop/

Estrutura de Diretórios Esperada
Assumimos que seus Dockerfiles estão dentro dos diretórios de suas respectivas aplicações:

my-turborepo/
├── apps/
│   ├── web/
│   │   └── Dockerfile  <-- Dockerfile para o projeto web
│   └── docs/
│       └── Dockerfile  <-- Dockerfile para o projeto docs
├── package.json
└── ...
1. Construir a Imagem Docker para o Projeto web
Navegue até a raiz do seu monorepo no terminal (my-turborepo/).

## Execute o seguinte comando para construir a imagem do seu projeto web:

```bash
docker build -t meu-app-web -f ./apps/web/Dockerfile .
```

docker build: Comando para construir uma imagem.
-t meu-app-web: Define o nome da imagem como meu-app-web.
-f ./apps/web/Dockerfile: Indica o caminho para o Dockerfile do seu projeto web.
.: O ponto final define o contexto do build como a raiz do seu monorepo. Isso é crucial para que seu Dockerfile possa copiar todo o código do projeto (COPY . .).
2. Construir a Imagem Docker para o Projeto docs
Com o terminal ainda na raiz do seu monorepo, execute o comando para construir a imagem do seu projeto docs:

```Bash
docker build -t meu-app-docs -f ./apps/docs/Dockerfile .
```

-t meu-app-docs: Define o nome da imagem como meu-app-docs.
-f ./apps/docs/Dockerfile: Indica o caminho para o Dockerfile do seu projeto docs.

3. Rodar os Containers Docker
Após construir as imagens, você pode iniciar cada aplicação em seu próprio container.

## Rodar o Projeto web

```Bash
docker run --rm -d -p 8080:3000 meu-app-web
```

docker run: Comando para iniciar um container a partir de uma imagem.
--rm: Remove o container automaticamente quando ele para.
-d: Roda o container em segundo plano (detached mode).
-p 8080:3000: Mapeia a porta 8080 da sua máquina para a porta 3000 do container (web deve estar exposto na porta 3000 no Dockerfile).
meu-app-web: O nome da imagem que você acabou de construir.
Você poderá acessar o projeto web em seu navegador via http://localhost:8080.

Rodar o Projeto docs

```bash
docker run --rm -d -p 8081:3001 meu-app-docs
```

-p 8081:3001: Mapeia a porta 8081 da sua máquina para a porta 3001 do container (docs deve estar exposto na porta 3001 no Dockerfile).
meu-app-docs: O nome da imagem que você acabou de construir.
Você poderá acessar o projeto docs em seu navegador via http://localhost:8081.
