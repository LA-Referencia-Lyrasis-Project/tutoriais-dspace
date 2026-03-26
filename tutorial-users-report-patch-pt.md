
# Tutorial - Relatório de Atividades de Usuários no DSpace

Este patch implementa um relatório estatístico que permite ao administrador visualizar um resumo geral das métricas do repositório, incluindo a quantidade total de usuários, envios, revisões, aprovações, rejeições e retiradas.

----------

## 1. Aplicando o Patch no Backend

Faça o download do arquivo `users-report-backend.diff` (localizado na pasta `scripts/`) para o diretório raiz da sua instalação do DSpace (código-fonte do backend). Abra um terminal na raiz do projeto e execute o seguinte comando:



```
git apply --reject --whitespace=fix users-report-backend.diff

```

## 2. Realizando o Build

Após aplicar o patch com sucesso, rode o comando do Maven para compilar o projeto:



```
mvn clean package

```

Assim que a compilação finalizar, navegue até a pasta do instalador gerado e execute a atualização via Ant:



```
cd dspace/target/dspace-installer
ant update

```

Por fim, **reinicie o seu servidor** (por exemplo, o Tomcat).

----------

## 3. Aplicando o Patch no Frontend (DSpace Angular)

Agora, faça o download do arquivo correspondente ao frontend (`users-report-frontend.diff`) para o diretório raiz da sua instalação do DSpace Angular. Abra um terminal na raiz do projeto Angular e execute o seguinte comando:



```
git apply --reject --whitespace=fix users-report-frontend.diff

```

Após aplicar o patch, instale as novas dependências executando:



```
npm install

```

Caso a instalação não funcione ou apresente algum problema, instale a biblioteca de gráficos especificamente rodando:



```
npm install apexcharts

```

----------

## ⚠️ Observações Importantes para o Frontend

-   **Incompatibilidade de Imports (DSpace 8 e 9):** Em versões anteriores ao DSpace 10 (como a 8 e a 9), o alias `@dspace` nos imports não é compatível. Após aplicar o patch, será necessário abrir os arquivos afetados e corrigir os caminhos dos imports manualmente.
    
-   **Conflitos em Arquivos de Tradução (i18n):** É provável que os arquivos de tradução gerem erros ou rejeições durante a aplicação do patch. Se o `git apply` falhar nesses arquivos e acabar criando um arquivo de tradução novo ou um arquivo `.rej`, você precisará corrigir isso manualmente. Basta abrir o arquivo gerado pelo patch, copiar as novas chaves de tradução e colá-las diretamente nos seus arquivos de tradução originais (como o `en.json5` ou `pt-BR.json5`).
