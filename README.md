# SAEPVision

Aplicação de compartilhamento de fotografias desenvolvida com HTML, CSS, JavaScript, Node.js, Express e MySQL. A galeria, as contas, as publicações e as curtidas são persistidas no banco; não há armazenamento de demonstração em memória no servidor.

## Requisitos

- Node.js 20 ou superior e npm.
- MySQL 8.0 ou superior.

## Configuração do MySQL

1. Inicie o serviço MySQL.
2. O script `database.sql` cria o banco `saepvision` e as tabelas `usuarios`, `publicacoes`, `curtidas` e `sessions`, com chaves estrangeiras e unicidade por usuário/publicação. Após configurar o `.env`, execute `npm run db:setup`; o servidor também garante a tabela de sessões ao iniciar.

3. No PowerShell, copie `.env.example` para `.env` e ajuste as credenciais:

   ```env
   Copy-Item .env.example .env
   ```

   Depois, abra `.env` e preencha as variáveis exibidas nele. Use uma chave de sessão longa e aleatória; não compartilhe nem versione o `.env`.

4. Instale dependências e crie as tabelas/carregue contas e fotografias de referência:

   ```sh
   npm install
   npm run db:setup
   npm run seed
   ```

   O script lê `database/tb_usuario.csv`, gera hashes bcrypt usando a senha de demonstração e insere no MySQL as seis contas da prova e as nove fotografias fornecidas. A carga pode ser repetida sem duplicar publicações. Defina `DEMO_USER_PASSWORD` antes de executar `npm run seed` para trocar a senha compartilhada das contas.

5. Inicie o servidor:

   ```sh
   npm start
   ```

   Acesse `http://localhost:3000`. Para desenvolvimento com reinício automático, use `npm run dev`.

## Contas de demonstração

Os dados vêm do CSV oficial anexado à prova; todas as contas de referência usam a senha `123456`.

- Fotógrafo: `fotografo1@email.com` / `123456`
- Usuário comum: `usuario1@gmail.com` / `123456`
- Também disponíveis: `fotografo2@gmail.com`, `fotografo3@gmail.com`, `usuario2@gmail.com` e `usuario3@gmail.com`.

Troque as senhas de demonstração antes de usar o sistema fora do ambiente de avaliação.

## Funcionalidades

- Login e logout com sessão no MySQL, cookie `HttpOnly` e senha armazenada com bcrypt.
- Pesquisa por nome ou identificador de fotógrafos sem recarregar a página.
- Galeria com publicações, local, autoria e contagem de curtidas.
- Curtidas persistidas, removíveis pelo mesmo usuário e protegidas por uma restrição `UNIQUE`.
- Cadastro de fotografias somente para fotógrafos, com validação de extensão, assinatura do arquivo e limite de tamanho.
- Perfil de fotógrafo, edição de nome/identificador, lista de publicações e exclusão restrita ao proprietário.
- Imagens de referência em `public/images`; novos arquivos enviados ficam em `public/uploads`.

## Testes

Execute `npm test` para as verificações automatizadas. A API também requer uma instância MySQL disponível para validar login e operações persistidas de ponta a ponta.

# SAEBVISION
