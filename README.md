# CAST Store — Documentação (GitHub Pages)

Portal de documentação da CAST Store, no mesmo modelo do `sacc-docs`:
`docs/index.html` (home com cards) + `docs/pagina.html?doc=<arquivo>.md` (visualizador
com sidebar que renderiza o markdown no navegador com marked + DOMPurify + Mermaid).

## Publicar

1. Crie o repositório (ex.: `cast-infra-interna/cast-store-docs`) e envie esta pasta:
   ```bash
   git init && git add . && git commit -m "docs: portal CAST Store"
   git branch -M main
   git remote add origin https://github.com/cast-infra-interna/cast-store-docs.git
   git push -u origin main
   ```
2. No GitHub: **Settings → Pages → Build and deployment → Deploy from a branch →
   `main` / `/ (root)`**.
3. Acesse `https://cast-infra-interna.github.io/cast-store-docs/docs/index.html`.

## Editar

- O conteúdo fica nos `.md` dentro de `docs/` (fonte única).
- Página nova: crie o `.md` e registre em `ARVORE_DOCS` em `docs/assets/js/main.js`.
- Cores: variáveis em `:root` de `docs/assets/css/style.css` (paleta oficial CAST).

## Testar localmente

```bash
cd docs && python -m http.server 8000
# abrir http://localhost:8000/index.html
```
