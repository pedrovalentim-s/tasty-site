# Site institucional — Tasty Media

Site de `tastymedia.com.br`. Página única, HTML autocontido (CSS e JS inline),
sem build e sem dependências.

## Estrutura

```
public/index.html    o site inteiro — é o único arquivo de conteúdo
.claude/launch.json  config do servidor local
```

## Rodar localmente

```bash
python3 -m http.server 4321 -d public
```

Abre em http://localhost:4321

## Publicar

O projeto no Cloudflare Pages chama-se **`tasty-site-1fn`**.

```bash
npx wrangler pages deploy public --project-name tasty-site-1fn
```

Requer acesso à conta Cloudflare da Tasty (`npx wrangler login` na primeira vez).
Enquanto o projeto for do tipo *Direct Upload*, o deploy é sempre manual por este
comando — um `git push` aqui **não publica nada** sozinho.

## Domínios — leia antes de mexer em DNS

| Host | Aponta para | Conteúdo |
|---|---|---|
| `tastymedia.com.br` | Cloudflare Pages (`tasty-site-1fn`) | este site |
| `www.tastymedia.com.br` | Great Pages | landing pages em `/lp3` e `/lp4` |

A raiz do `www` faz 302 para o apex, configurado **dentro do painel do Great Pages**.

⚠️ DNS aponta o hostname inteiro, nunca caminhos individuais. Apontar `www` para o
Cloudflare Pages derruba as landing pages do Great Pages. O apex é o único host
livre para este site.
