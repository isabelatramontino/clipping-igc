# Setup — Publicar no GitHub Pages

Passo a passo. Use o Terminal do seu Mac.

## Pré-requisitos (1 vez só)

1. **Conta no GitHub:** https://github.com/signup (se ainda não tiver)
2. **Git instalado:** já vem no macOS. Para verificar: `git --version`
3. **GitHub CLI (opcional mas facilita muito):** https://cli.github.com
   ```bash
   brew install gh
   gh auth login
   ```

## Passo 1 — Criar o repositório no GitHub

**Opção A — via GitHub CLI (mais rápido):**
```bash
cd ~/Documents/clipping-ma-github   # ou onde você salvou a pasta
gh repo create clipping-ma --public --source=. --remote=origin
```

**Opção B — via site:**
1. Vá em https://github.com/new
2. Nome do repositório: `clipping-ma`
3. Público (para usar GitHub Pages grátis)
4. NÃO marque "Initialize with README" (já temos um)
5. Clique "Create repository"

## Passo 2 — Fazer o primeiro push

No terminal, dentro da pasta `clipping-ma-github`:

```bash
cd ~/Documents/clipping-ma-github
git init
git add .
git commit -m "Primeiro clipping M&A"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/clipping-ma.git
git push -u origin main
```

Troque `SEU-USUARIO` pelo seu username do GitHub.

## Passo 3 — Ativar GitHub Pages

1. Vá em `https://github.com/SEU-USUARIO/clipping-ma/settings/pages`
2. Em **Source**, selecione: `Deploy from a branch`
3. **Branch:** `main` · **Folder:** `/ (root)` · clique **Save**
4. Aguarde 1-2 minutos. Sua URL pública vai aparecer no topo da página — algo como:
   ```
   https://SEU-USUARIO.github.io/clipping-ma/
   ```
5. Abra a URL para confirmar que está no ar.

## Passo 4 (opcional) — Domínio próprio

Se quiser usar algo como `clipping.igcp.com.br`:

1. Fale com o time de TI da IGC para apontar um CNAME:
   ```
   clipping.igcp.com.br  →  SEU-USUARIO.github.io
   ```
2. Em `Settings → Pages` do repo, coloque o domínio no campo "Custom domain"
3. Marque "Enforce HTTPS"

## Passo 5 (opcional) — Atualização automática

Para que o clipping das 9h e 18h publique sozinho no GitHub, me avise depois que fez o push inicial. Eu vou atualizar a tarefa agendada para, ao fim de cada atualização, rodar `git add . && git commit -m "Update DD/MM HH:MM" && git push`. Para isso funcionar sem pedir senha, precisa configurar credenciais Git (SSH key ou personal access token) — eu te passo o passo a passo quando chegarmos lá.

---

**Dúvidas comuns**

- *Preciso pagar?* Não — GitHub Pages é grátis para repositórios públicos.
- *Qualquer um pode ver o site?* Sim, é público. Se quiser controle de acesso, precisamos trocar para Cloudflare Pages com Access ou Vercel com autenticação.
- *Posso editar o arquivo direto no GitHub?* Pode — abra `index.html` no GitHub, clique no lápis e edite. As mudanças aparecem no site em ~1 minuto.
