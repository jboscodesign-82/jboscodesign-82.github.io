# CLAUDE.md

Este arquivo orienta o Claude Code ao trabalhar neste repositório.

## Visão geral

Portfólio de produto e design do João Bosco, publicado via GitHub Pages.
Site estático, sem build nem dependências — cada página é autocontida
(HTML + CSS + JS embutidos).

## Estrutura

- `index.html` — home do portfólio (hero, lista de trabalhos, awards, about, contato).
- `project-*.html` — uma página por case, todas no mesmo template visual.
- `assets/` — imagens e vídeos das páginas de projeto.
- `avatar.png`, `favicon-*.png` — identidade, referenciados pela raiz.
- `loaders/` — galeria de 50 loaders em CSS puro (projeto à parte).
- `smart-cifra/` — projeto Next.js à parte, publicado na Netlify (ver `netlify.toml`).
- `.github/workflows/deploy-pages.yml` — publica a raiz do repo no GitHub Pages.
- `.claude/` — configuração do Claude Code (permissões, hooks, settings).

## Convenções

- Idioma de comunicação: português (pt-BR).
- Commits: mensagens claras e descritivas, no imperativo.

### Páginas de projeto

Todas compartilham os mesmos tokens CSS (`--bg`, `--ink`, `--accent`, `--serif`…),
header, animação de reveal no scroll e navegação "Let's keep exploring" encadeando
um projeto ao próximo. Ao criar uma página nova, copie a estrutura de uma existente
em vez de inventar outra.

**Imagem nunca deve ultrapassar o tamanho natural.** Boa parte dos assets tem menos
de 1200px e estica feio em largura total. Cada peça leva um `max-width` igual à sua
largura real, e nas galerias o slide é uma caixa com a imagem centralizada em
`width/height: auto` — `object-fit: contain` sozinho amplia e borra.

**GIF vira MP4.** Converta com ffmpeg (`libx264`, `-crf 25`, `-pix_fmt yuv420p`) e
confira que a duração bate com a do GIF antes de apagar o original. A economia passa
de 90%.

**Galeria** aceita várias instâncias por página: o JS varre `.gallery` e inicializa
cada uma. Não use IDs fixos. Navega por setas, dots e arrasto com o dedo — o
arrasto trava o eixo no primeiro movimento, então gesto vertical dentro da galeria
continua rolando a página. `.gallery-outer` leva `touch-action: pan-y`.

## Comandos úteis

Não há build. Para visualizar localmente:

```sh
python3 -m http.server 8000   # depois acesse http://localhost:8000
```

## Publicação

Push na branch de deploy dispara o workflow e publica a raiz do repo.
A branch está declarada em `.github/workflows/deploy-pages.yml`.
