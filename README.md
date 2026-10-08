# Ha fatto anche cose buone

Verifica, una per una, le presunte "cose buone" del fascismo. Sito statico generato con Hugo.

## Sviluppo locale

```bash
hugo server -D
```

Serve Hugo (versione estesa non necessaria). Anteprima su http://localhost:1313

## Nuova scheda

```bash
hugo new bufale/nome-scheda.md
```

## Deploy

Build: `hugo --minify` — output in `public/`

Pubblicato su GitHub Pages tramite `.github/workflows/hugo.yaml` a ogni push su `main`.

## Contribuire

Vedi [CONTRIBUTING.md](CONTRIBUTING.md). Le regole editoriali complete sono in [AGENTS.md](AGENTS.md).

## Licenza

Contenuti: CC BY-SA 4.0. Codice: MIT.
