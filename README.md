# Meu Banco

App pessoal de finanças: receitas, despesas, investimentos, dívidas, Imposto de Renda e relatórios em PDF.
Funciona no navegador e instala na tela inicial do celular. Com **login e senha**, seus dados ficam na nuvem (Supabase) e você acessa de qualquer aparelho.

## ⚠️ Privacidade

- O código **não contém seus dados**. Nunca suba `MEUS-DADOS-NAO-SUBIR-NO-GITHUB.json` para o GitHub. Importe esse arquivo dentro do app, depois de logar.
- O GitHub Pages grátis exige repositório público. É seguro porque o código não tem dados pessoais. A chave `anon` do Supabase é pública por natureza; quem protege seus dados é o login + a regra de segurança (RLS) do passo 3.
- **Nunca** coloque a chave `service_role` em nenhum arquivo.

## 1. Criar o projeto no Supabase (grátis)

1. Entre em **supabase.com** ▸ **Start your project** ▸ entre com o GitHub ou e-mail.
2. **New project**. Nome: `meu-banco`. Crie uma senha forte para o banco (guarde). Região: **South America (São Paulo)**. Plano **Free**. Aguarde 1–2 minutos.

## 2. Pegar a URL e a chave

1. No projeto: **Project Settings** (engrenagem) ▸ **API Keys** (ou **API**).
2. Copie o **Project URL** (`https://xxxx.supabase.co`) e a chave **anon / public** (ou *Publishable key*).

https://okgkybcvchnnpdhirxdw.supabase.co
sb_publishable_TjneNe6B8fFB2dY6B35wHg_0lL3guBY

## 3. Criar a tabela segura

1. Menu **SQL Editor** ▸ **New query**. Cole tudo abaixo e toque em **Run**:

```sql
create table if not exists public.dados (
  user_id uuid primary key references auth.users(id) on delete cascade,
  conteudo jsonb not null,
  atualizado bigint not null default 0
);
alter table public.dados enable row level security;
create policy "dono_le" on public.dados for select using (auth.uid() = user_id);
create policy "dono_insere" on public.dados for insert with check (auth.uid() = user_id);
create policy "dono_atualiza" on public.dados for update using (auth.uid() = user_id) with check (auth.uid() = user_id);
grant select, insert, update on public.dados to authenticated;
```

Deve aparecer "Success". Isso garante que cada login só enxerga os próprios dados.

## 4. Login por e-mail e senha

1. **Authentication ▸ Sign In / Providers ▸ Email**: deixe ligado. Desligue **Confirm email** (assim você entra logo após criar a conta). Salve.
2. Abra o app, toque em **Criar conta** e crie seu e-mail e senha (mínimo 8 caracteres).
3. **Depois de criar a sua conta**, volte em Authentication ▸ Sign In / Providers e desligue **Allow new users to sign up**. Assim ninguém mais consegue criar conta no seu app.

## 5. Ligar o app ao Supabase

No GitHub, abra o arquivo `config.js` ▸ lápis (editar) ▸ cole a URL e a chave entre as aspas ▸ **Commit changes**. Só isso.

## Publicar no GitHub Pages

1. github.com ▸ **+ ▸ New repository** ▸ nome `meu-banco` ▸ **Public** ▸ Create.
2. **uploading an existing file** e envie: `index.html`, `config.js`, `manifest.webmanifest`, `sw.js`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png`, `README.md`.
3. **Commit changes** ▸ **Settings ▸ Pages** ▸ Branch `main` / `(root)` ▸ Save.
4. Em 1–2 min: `https://SEU-USUARIO.github.io/meu-banco/`

(Ao atualizar o app depois, troque o número em `sw.js`: `meubanco-v3` → `v4`.)

## Primeiro uso

1. Abra o endereço, toque em **Criar conta** (ou Entrar).
2. Toque em **Importar backup (.json)** e escolha `MEUS-DADOS-NAO-SUBIR-NO-GITHUB.json`. Ele sobe para a sua conta.
3. Em outro aparelho: abra o mesmo endereço e entre com o mesmo e-mail e senha.
4. iPhone: Safari ▸ Compartilhar ▸ Adicionar à Tela de Início. Android: Chrome ▸ ⋮ ▸ Instalar app.

## Como a sincronização funciona (leia)

- Cada alteração é salva no aparelho na hora e enviada à nuvem em segundos. Sem internet, o app funciona e envia quando voltar.
- Ao abrir o app ou voltar para ele, ele busca alterações feitas em outro aparelho.
- **Vale a alteração mais recente (última a salvar vence).** Não existe mistura automática. Se você editar em dois aparelhos ao mesmo tempo, sem sincronizar entre eles, uma das edições é perdida. Na prática: espere o "☁ Sincronizado" antes de trocar de aparelho.
- **Plano grátis do Supabase pausa o projeto após ~7 dias sem uso.** Se acontecer, o login falha: entre em supabase.com e toque em **Restore project**. Seus dados não são apagados. Usar o app toda semana evita isso.
- Esqueceu a senha? Em Supabase ▸ Authentication ▸ Users ▸ seu usuário ▸ definir nova senha.
- Continue exportando um **backup (.json)** de vez em quando (Mais ▸ Backup). O PIN, se ativado, também sincroniza.

## Novidades desta versão

- Login/senha e nuvem; Sair da conta limpa o aparelho.
- Toda receita/despesa tem **data** (e recorrentes têm **dia do mês**). Sem data aparece "sem data".
- Cartão **📍 Onde você parou**; gráficos que destacam o mês escolhido, gráfico de gastos por dia, rosca com o mês/ano.
- **PDF** gerado pelo próprio app: no celular abre o menu Compartilhar (Arquivos, WhatsApp…).

## Limites

- IR é estimativa (Lei 15.270/2025), não substitui a Receita nem contador.
- A fonte Inter vem do Google Fonts; sem internet usa a do sistema.
