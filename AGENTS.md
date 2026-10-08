# Contesto del progetto

Sito statico Hugo che verifica, una per una, le presunte "cose buone" del fascismo.
Dominio previsto: hafattoanchecosebuone.it

## Regole editoriali — non negoziabili

1. **Nessuna affermazione verificabile senza fonte.** Ogni claim puntuale è agganciato a una nota a piè di pagina (`[^nome]`) che rimanda al testo e al link esatti, elencate in fondo alla scheda sotto `## Fonti`. Se una fonte non è verificabile, l'affermazione si toglie.
2. **Il merito, dove c'è, si riconosce.** Verdetto `parzialmente vero` quando esiste un nucleo reale. Non gonfiare le smentite.
3. **Tono asciutto, mai insultante.** Il lettore ideale è chi arriva diffidente. Un dato preciso convince, un aggettivo no. Ironia ammessa solo se sostenuta da un fatto.
4. **Mai citazioni lunghe dalle fonti.** Riformulare sempre con parole proprie e linkare l'originale.

## Struttura

- `content/bufale/*.md` — una scheda per mito
- `content/metodo.md` — spiegazione del metodo e dei verdetti
- `layouts/` — template, nessun tema esterno
- `static/css/style.css` — unico foglio di stile, token CSS in `:root`; contiene anche le `@font-face`
- `static/fonts/` — font ospitati in locale (niente Google Fonts: privacy e prestazioni)
- `archetypes/bufale.md` — scheletro per `hugo new`

## Front matter di una scheda

```yaml
mito: "la frase come si sente dire davvero, senza virgolette caporali"
fatto: "una riga di smentita, compare nell'elenco in home"
categoria: "una delle categorie esistenti, controlla prima di inventarne"
verdetto: "falso" | "parzialmente vero" | "propaganda" | "omissione"
```

Il campo `mito` viene reso nel template già con le virgolette caporali: non metterle nel front matter.

## Citare le fonti

Le fonti sono note a piè di pagina in stile Wikipedia, non un array nel front matter. Nel corpo, agganciate al claim specifico:

```markdown
Circa cinquantamila morti[^rochat] secondo lo storico.
```

In fondo alla scheda, sotto un `## Fonti`:

```markdown
## Fonti

[^rochat]: Giorgio Rochat — [Deportazione e campi di concentramento](https://...)
```

Hugo/Goldmark genera da solo numerazione, link e freccia di ritorno: non serve altro markup. Una fonte senza url resta comunque una nota valida (citazione bibliografica senza link).

- Si cita solo ciò che si è letto. Se un dato viene da un autore che lo riprende da altri (es. Filippi che cita Novello), la nota indica anche la fonte originale e la pagina.
- Per i libri, indicare pagina o capitolo.
- Link a Normattiva solo nella forma non codificata: `https://www.normattiva.it/uri-res/N2Ls?urn:nir:stato:regio.decreto.legge:1933-03-27;371`. La forma `urn%3A...=` apre una pagina di errore pur rispondendo 200. Usare il tipo d'atto giusto (`legge`, `regio.decreto`, `regio.decreto.legge`, `decreto.legislativo.luogotenenziale`…).

## Sistema visivo

L'idea è **la correzione**: la frase falsa porta il segno rosso della penna, sotto c'è il fatto.
- Display: Bodoni Moda (corsivo per i miti). Testo: Archivo. Riferimenti e etichette: IBM Plex Mono.
- Rosso `--rosso` solo per il segno di correzione e i verdetti falsi. Blu `--blu-archivio` per link, note, focus e verdetto parziale. I verdetti `propaganda` e `omissione` usano `--inchiostro` (modificatori `voce__verdetto--neutro` e `timbro--neutro`).
- Contrasto minimo WCAG AA (4,5:1) per il testo: `--inchiostro-lieve` è tarato su questo.
- Una sola animazione in tutto il sito: il tratto rosso in apertura. Rispetta `prefers-reduced-motion`. Non aggiungerne altre, nemmeno transizioni al passaggio del mouse.

La data «Ultima revisione» di ogni scheda viene da git (`enableGitInfo`): per questo il workflow fa il checkout con `fetch-depth: 0`.

## Comandi

```bash
hugo server -D      # anteprima locale con le bozze
hugo new bufale/nome-scheda.md
hugo --minify       # build di produzione in public/
```

## Nota operativa

Questo repository è pubblicato da un account GitHub separato dall'identità personale dell'autore. Non inserire nome, email personale o riferimenti biografici in commit, contenuti o configurazioni.
