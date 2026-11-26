# Meu Banco

App pessoal de gestão financeira: receitas, despesas, investimentos, dívidas, Imposto de Renda e relatórios em PDF.
Funciona no navegador e pode ser instalado na tela inicial do celular, como um app. Não precisa de servidor nem de instalação de nada.

## ⚠️ Leia antes de publicar (privacidade)

- **Este código não contém seus dados.** Ele abre vazio. Seus lançamentos ficam salvos **só no navegador do seu aparelho**.
- **Nunca suba para o GitHub o arquivo `MEUS-DADOS-NAO-SUBIR-NO-GITHUB.json`.** Ele tem seus dados reais (salário, dívidas). Esse arquivo você importa **dentro do app**, depois de publicado.
- O GitHub Pages **gratuito exige repositório público**. Isso é seguro aqui (o código não tem dados pessoais), mas qualquer pessoa que souber o endereço consegue abrir o app, vazio. Se quiser o código privado, publique o mesmo repositório na Vercel (aceita repositório privado, grátis).

## Publicar no GitHub Pages (pelo navegador, sem programar)

1. Entre em **github.com** e toque em **+ ▸ New repository**.
2. Nome: `meu-banco`. Deixe **Public**. Toque em **Create repository**.
3. Toque em **uploading an existing file** (ou **Add file ▸ Upload files**).
4. Envie **todos** estes arquivos: `index.html`, `manifest.webmanifest`, `sw.js`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png`, `README.md`.
5. Toque em **Commit changes**.
6. Vá em **Settings ▸ Pages**. Em **Branch**, escolha `main` e a pasta `/ (root)`. Toque em **Save**.
7. Espere 1 a 2 minutos. Seu app fica em: `https://SEU-USUARIO.github.io/meu-banco/`

## Primeiro uso

1. Abra o endereço no celular.
2. Toque em **Importar backup (.json)** e escolha `MEUS-DADOS-NAO-SUBIR-NO-GITHUB.json` (guardado no seu aparelho). Ou toque em **Começar do zero**.
3. **iPhone:** Safari ▸ Compartilhar ▸ **Adicionar à Tela de Início**. **Android:** Chrome ▸ ⋮ ▸ **Instalar app**.

## Dia a dia

- **+** (botão laranja): lança gasto, despesa, receita ou investimento em 3 toques.
- **Mês**: tudo do mês, limites por categoria, contas e investimento do mês.
- **Investir / Dívidas / Mais ▸ Imposto de Renda / Relatórios**: equivalem às abas da planilha.
- **Mais ▸ Novo ano**: cria os 12 meses do ano seguinte, já ligados ao saldo de dezembro.
- **Mais ▸ Backup**: exporte um arquivo de vez em quando. **É a sua única cópia de segurança.**

## Atualizar o app depois

Troque o `index.html` no repositório (Add file ▸ Upload files, mesmo nome). Para o celular pegar a versão nova, edite `sw.js` e mude o número (por exemplo, de `meubanco-v2` para `meubanco-v3`).

## Limites (leia)

- **Os dados ficam só neste aparelho e navegador.** Limpar os dados do navegador apaga tudo. Não há sincronização entre celular e computador: exporte o backup num e importe no outro.
- **O PIN é uma trava de conveniência**, não criptografia forte. Não substitui a senha do celular.
- **O Imposto de Renda é estimativa** (Lei 15.270/2025, tabelas conferidas em nov/2026). Não substitui o programa da Receita nem um contador.
- A fonte (Inter) vem do Google Fonts na primeira abertura; sem internet, o app usa fontes do sistema.
