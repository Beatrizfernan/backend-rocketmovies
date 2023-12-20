# **RocketMovies API - Backend**

Bem-vindo à RocketMovies API, uma plataforma para gerenciamento de notas e informações sobre filmes! Esta API permite que usuários armazenem títulos, notas e observações associadas a filmes que assistiram.

## **Configurações**

### **Autenticação**

O arquivo **`auth.js`** em **`backend-rocketmovies/src/configs`** define as configurações para autenticação JWT. Certifique-se de configurar a variável de ambiente **`AUTH_SECRET`** para garantir a segurança da autenticação.

```jsx

module.exports = {
  jwt: {
    secret: process.env.AUTH_SECRET || "default",
    expiresIn: "1d",
  },
};

```

### **Upload de Arquivos**

O arquivo **`upload.js`** em **`backend-rocketmovies/src/configs`** contém as configurações para o upload de arquivos usando o **`multer`**. Os arquivos são temporariamente armazenados em uma pasta temporária (**`TMP_FOLDER`**) antes de serem movidos para a pasta de upload (**`UPLOAD_FOLDER`**). Certifique-se de configurar esses caminhos de acordo.

```jsx

const path = require("path");
const multer = require("multer");
const crypto = require("crypto");

const TMP_FOLDER = path.resolve(__dirname, "..", "..", "temp");
const UPLOAD_FOLDER = path.resolve(TMP_FOLDER, "uploads");

const MULTER = {
  storage: multer.diskStorage({
    destination: TMP_FOLDER,
    filename(request, file, callback) {
      const fileHash = crypto.randomBytes(10).toString("hex");
      const fileName = `${fileHash}-${file.originalname}`;

      return callback(null, fileName);
    },
  }),
};

module.exports = {
  TMP_FOLDER,
  UPLOAD_FOLDER,
  MULTER,
};

```

## **Controllers**

A pasta **`backend-rocketmovies/src/controllers`** contém os controladores responsáveis pela lógica de negócios da aplicação.

- **NotesControllers.js**: Controlador para operações relacionadas a notas (filmes). Permite criar, atualizar, excluir e obter informações sobre notas, incluindo tags associadas.
- **SessionsControllers.js**: Controlador responsável pela autenticação do usuário.
- **UsersAvatarController.js**: Controlador para atualização do avatar do usuário.
- **UsersControllers.js**: Controlador para operações relacionadas a usuários. Permite criar e atualizar informações do usuário.

## **Rotas**

A configuração de rotas está definida nos arquivos em **`backend-rocketmovies/src/routes`**.

- **index.js**: Agrupa todas as rotas da aplicação.
- **notes.routes.js**: Define rotas relacionadas a notas, utilizando o **`NotesControllers`**. As operações incluem criar, atualizar, excluir, mostrar e listar notas.
- **sessions.routes.js**: Define a rota para autenticação do usuário, utilizando o **`SessionsControllers`**.
- **users.routes.js**: Define rotas relacionadas a usuários, utilizando **`UsersControllers`** e **`UsersAvatarController`**. Inclui operações de criação, atualização e atualização de avatar.

## **Middlewares**

- **ensureAuthenticated.js**: Middleware para garantir que as rotas protegidas só sejam acessadas por usuários autenticados.

## **Utils**

- **AppError.js**: Classe para lidar com erros personalizados na aplicação.
- **DataChecker.js**: Classe com métodos para validar e verificar dados, como a existência de usuários, notas, tags, etc.

## **Configuração do Banco de Dados**

A pasta **`backend-rocketmovies/src/database/knex`** contém arquivos relacionados à configuração do banco de dados usando o Knex. Certifique-se de configurar as migrações para criar as tabelas necessárias.

## **Servidor**

O arquivo **`backend-rocketmovies/src/server.js`** inicializa o servidor Express e configura a lógica de tratamento de erros.

## **Executando a Aplicação**

Certifique-se de ter as dependências instaladas usando:

```bash

npm install

```

Em seguida, inicie o servidor usando:

```bash

npm start

```

A API estará acessível em **`http://localhost:3333`**. Certifique-se de ajustar a porta conforme necessário.



https://statuesque-croquembouche-626d47.netlify.app/
https://rocketmoviess.onrender.com
