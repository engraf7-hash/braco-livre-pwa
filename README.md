# Braço Livre — App de Guitarra (PWA)

App para ensinar guitarra (cordas, escalas, harmonia, palhetada), com afinador cromático, identificador de notas por microfone e exercícios visuais. Funciona offline e é instalável no celular.

## Estrutura

```
├── index.html          # App inteiro (HTML + CSS + JS)
├── manifest.json        # Metadados do PWA (nome, cores, ícones)
├── sw.js                # Service worker (cache offline)
├── icons/
│   ├── icon-192.png
│   ├── icon-512.png
│   └── apple-touch-icon.png
└── README.md
```

## Publicar no GitHub Pages (passo a passo)

1. Crie um repositório novo no GitHub (ex: `braco-livre`).
2. Faça upload de **todos** estes arquivos mantendo a mesma estrutura de pastas (o `icons/` precisa continuar como subpasta).
3. No repositório, vá em **Settings → Pages**.
4. Em **Source**, selecione a branch `main` (ou `master`) e a pasta `/ (root)`.
5. Salve. Em alguns minutos o GitHub mostrará a URL pública, algo como:
   `https://seu-usuario.github.io/braco-livre/`
6. Abra essa URL no celular (Chrome/Safari) → menu do navegador → **"Adicionar à tela de início"** / **"Instalar app"**.

## Rodar localmente antes de subir (opcional)

Service workers exigem HTTPS ou `localhost` — não funcionam abrindo o `index.html` direto no navegador (`file://`). Para testar localmente:

```bash
cd braco-livre-pwa
python3 -m http.server 8000
```

Depois acesse `http://localhost:8000` no navegador.

## Observações técnicas

- O **afinador** e o **identificador de notas** usam a Web Audio API (`getUserMedia`) — o navegador vai pedir permissão de microfone. Isso só funciona em contexto seguro (HTTPS ou localhost), o que o GitHub Pages já garante.
- O `sw.js` guarda os arquivos principais em cache na primeira visita, então o app abre offline depois disso (exceto o afinador, que sempre precisa do microfone ativo).
- Os ícones em `icons/` são placeholders simples gerados programaticamente — sinta-se à vontade para substituí-los por uma arte própria, mantendo os mesmos nomes de arquivo e tamanhos (192×192, 512×512, 180×180).
- Para trocar o nome, cores ou ícone do app na tela inicial, edite `manifest.json`.
