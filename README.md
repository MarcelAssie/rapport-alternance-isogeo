# Rapport d'alternance Isogeo

Depot LaTeX du rapport d'alternance de Marcel Assie chez Isogeo, realise dans
le cadre du cycle ingenieur en geomatique a Geodata Paris.

Le document principal est `main.tex`. Il assemble la page de garde, les pages
preliminaires, le glossaire, les listes automatiques et, progressivement, les
chapitres du rapport.

## Structure

```text
.
|-- main.tex                 # Fichier racine du rapport
|-- frontmatter/             # Couverture, informations, resume, glossaire, listes
|-- parts/                   # Chapitres du corps du rapport
|-- annexes/                 # Annexes
|-- bibliography/            # Bibliographie
|-- figures/                 # Images et logos utilises dans le rapport
|-- config/                  # Configuration et metadonnees du rapport
|-- auxil/                   # Fichiers temporaires de compilation
`-- out/                     # PDF genere
```

Les images de la page de garde sont attendues dans `figures/frontmatter/` :

- `geodataparis.png` pour l'ecole ;
- `isogeo_logo.png` pour l'entreprise ;
- `illustration_couverture.png` pour l'illustration principale.

## Prerequis

- Une distribution LaTeX, par exemple MiKTeX.
- `latexmk`.
- LuaLaTeX. Le projet n'est pas prevu pour etre compile avec pdfLaTeX.

## Compilation

Depuis la racine du depot :

```powershell
latexmk -pdf -lualatex -file-line-error -interaction=nonstopmode `
  -output-directory=out `
  -aux-directory=auxil `
  main.tex
```

Le PDF final est genere ici :

```text
out/main.pdf
```

Dans PyCharm, il faut configurer la compilation avec LuaLaTeX et pointer le
fichier principal sur `main.tex`. Si le PDF affiche encore une ancienne version,
fermer puis rouvrir l'onglet PDF permet souvent de vider le cache du visualiseur.

## Modifier le rapport

- Les informations generales du rapport sont centralisees dans `main.tex` et
  dans `config/metadata.tex`.
- La page de garde est dans `frontmatter/couverture.tex`.
- Les informations administratives sont dans
  `frontmatter/informations_rapport.tex`.
- Le glossaire et la liste des sigles sont dans
  `frontmatter/glossaire_sigles.tex`.
- La table des matieres, la liste des figures et la liste des tableaux sont
  dans `frontmatter/tables_et_listes.tex`.
- Les chapitres du corps du rapport pourront etre ajoutes dans `parts/`, puis
  charges depuis `main.tex` avec `\LoadReportFile{parts/nom_du_fichier}`.

## Nettoyage

Pour supprimer les fichiers temporaires generes par `latexmk` :

```powershell
latexmk -C
```

Les dossiers `auxil/` et `out/` peuvent etre regeneres par une nouvelle
compilation.
