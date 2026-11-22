# SAMTECH · Gestão de OS (GitHub Pages + Google Drive)

Arquivos: `index.html` (app) e `config.js` (suas chaves). Os dados das OS/clientes e os PDFs ficam no **seu Google Drive**.

## 1. Google Cloud (uma vez, ~10 min)
1. Acesse console.cloud.google.com → crie o projeto "SAMTECH OS".
2. **APIs e serviços › Biblioteca** → ative a **Google Drive API**.
3. **Tela de consentimento OAuth** → tipo Externo → preencha nome e e-mail → em **Usuários de teste** adicione os e-mails de quem vai usar (até 100). Pode deixar em modo "Teste".
4. **Credenciais › Criar credenciais › ID do cliente OAuth › Aplicativo da Web**.
   - Origens JavaScript autorizadas: `https://SEU-USUARIO.github.io`
5. Copie o **ID do cliente** para `clientId` em `config.js`.

## 2. Pasta compartilhada no Drive
1. No Drive crie a pasta **SAMTECH OS** e compartilhe com a equipe como **Editor**.
2. Abra a pasta e copie o ID da URL (`drive.google.com/drive/folders/ID`) para `rootFolderId` em `config.js`.
   (Sem isso, cada pessoa criaria a sua própria pasta.)

## 3. GitHub Pages
1. Crie um repositório (ex.: `samtech-os`) e envie `index.html` e `config.js`.
2. **Settings › Pages › Deploy from a branch › main / (root)**.
3. Acesse `https://SEU-USUARIO.github.io/samtech-os/`.

## Como funciona
- Dados em `SAMTECH OS/_dados` (um arquivo por OS/cliente); o app atualiza a cada ~8 s para todos.
- Botão **☁ Drive** gera o PDF e salva em `Contratos|Pontuais › Cliente › Ano › Mês`.
- Escopo `drive` completo é necessário para ler a pasta compartilhada; por isso só use com contas da equipe.
- Fotos ficam reduzidas dentro do arquivo da OS (use poucas fotos por OS; o ideal é até ~12).
- O `clientId` não é segredo, mas o repositório público expõe o `rootFolderId`; o acesso real é controlado pelo compartilhamento do Drive.

## Venda para outras empresas (marca própria)
- Cada cliente recebe **sua própria cópia**: repositório GitHub próprio, projeto Google Cloud próprio (ou o seu, com os e-mails dele em "Usuários de teste") e pasta própria no Drive. Assim os dados de uma empresa nunca se misturam com os de outra.
- No `config.js` do cliente: coloque o `clientId` e o `rootFolderId` dele e use `seed: false`.
- Dentro do app, aba **⚙ Marca**: logotipo, nome, contatos e cores. A identidade fica salva no Drive do cliente e vale para a tela e para os PDFs.
- Atenção: o acesso total ao Drive (`drive`) é um escopo restrito do Google. Para uso interno da equipe de cada cliente (modo teste, até 100 e-mails) funciona; para um aplicativo público seria preciso a verificação do Google ou outro tipo de armazenamento.
