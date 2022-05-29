---
jupytext:
  cell_metadata_filter: -all
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Démonstration de Jupyter Books
## Bases

Installation :
```bash
pip3 install -U jupyter-book
```

Création :
```bash
jb create moncours/
```

ou pour créer à partir d'une TDM : 


```bash
jb toc to-project path/to/_toc.yml 
```


Compiler le cours :


```bash
jb build moncours/
```

Trois types de contenus sont acceptés en entrée : md, ipynb, MyST md




Nettoyage des fichiers sans .jupyter_cache :

```bash
jupyter-book clean mybookname/
```

et de tout le dossier build :

```bash
jupyter-book clean mybookname/ --all
```



[Badges](https://shields.io/)

[![Jupyter Book Badge](badge.svg)](<YOUR URL HERE>)


## Format MyST
Conversion MD ->myST (ajout de metadonnées au début) :

```bash
jupyter-book myst init path/to/markdownfile.md
```

Conversion IPYNB ->myST :

```bash
jupytext mynotebook.ipynb --to myst
```

[Liste des commandes en plus de MD](https://myst-parser.readthedocs.io/en/latest/syntax/syntax.html#syntax-directives)



## Images et figures

```{image} logo.png

:alt: fishy
:class: bg-primary mb-1
:width: 200px
:align: center
```

+++

```{figure} logo.png
---
height: 150px
name: directive-fig
---
Logo !
```


puis pour faire un lien :
{ref}`directive-fig`

+++

Pour déplacer la légende en marge :

```{figure} logo.png
---
figclass: margin-caption
---
Here is my figure caption!
```


+++

Pour déplacer la figure complète :


```{figure} logo.png
---
figclass: margin
---
Here is my figure caption!
```

+++

Pour aligner à gauche :
```{figure} logo.png
---
scale: 50%
align: left
---
Here is my figure caption!
```




## Cacher
### Dans un fichier MD
```{dropdown} Cliquez ici 
Contenu caché !
```
(marche sans Javascript contrairement au suivant)


```{admonition} Cliquez ici
:class: dropdown
Contenu caché !
```

```{toggle}
Contenu caché !
```

```{toggle} Cliquez ici 
:show:
Contenu caché !
```




### Dans un fichier MyST



### Dans un notebook



https://jupyterbook.org/en/stable/interactive/hiding.html#hiding-remove-content

```
{
    "tags": [
        "hide-output"
    ]
}
```

ou hide-cell	ou hide-input	ou remove-cell etc.

## Boîtes
### Admonition : boite avec un titre perso
```{admonition} Ma boîte
:class: tip
Coucou
```

+++


Inclusions :
::::{important}
:::{note}
This text is **standard** _Markdown_
:::
::::

### Directives
```{note}
Here is a note!
```
autres : warning, 
liste ici : https://sphinx-book-theme.readthedocs.io/en/latest/reference/kitchen-sink/paragraph-markup.html#admonitions

+++

Autre syntaxe plus compatible avec d'autres outils :
:::{note}
This text is **standard** _Markdown_
:::



## Dispositions
### Cartes côte à côte
````{panels}
Panel header 1
^^^
Panel body 1
+++
Panel footer 1
---

Panel header 2
^^^
Panel body 2
+++
Panel footer 2
````
voir : https://sphinx-panels.readthedocs.io/en/latest/#card-layout


````{panels}
:column: col-4
:card: border-2
Header A
^^^
Body A
---
Header B
^^^
Body B
---
Header C
^^^
Body C
````
voir : https://sphinx-panels.readthedocs.io/en/latest/#card-styling


### Tabbed contents
```{tabbed} Tab 1 title
My first tab
```

```{tabbed} Tab 2 title
My second tab with `some code`!
```

un exemple avec intégration de sortie :
````{tabbed} A histogram
```{glue:figure} boot_fig
:figwidth: 300px
:name: "fig-boot-tab"

This is a **caption**, with an embedded `{glue:text}` element: {glue:text}`boot_mean:.2f`!
```
````

````{tabbed} A table
```{glue:figure} df_tbl
:figwidth: 300px
:name: "tbl:df-tab"

A caption for a pandas table.
```
````

````{tabbed} Code to generate this
`{ code block here }`
````

voir : https://sphinx-panels.readthedocs.io/en/sphinx-book-theme/index.html#components-tabbed


### Utilisation de la marge
#### Contenu placé à droite
```{sidebar} My sidebar title
My sidebar content
```

#### Marge
```{margin} An optional title
My margin content
```

```{code-cell} <language>
:tags: [margin,remove-input]
print('Cc !')
```
voir : https://jupyterbook.org/en/stable/reference/cheatsheet.html#myst-cheatsheet

[Mettre la sortie d'une cellule (exemple : graphique) en marge droite avec un notebook](https://jupyterbook.org/en/stable/content/layout.html#layout-sidebar)




### Occuper tout l'espace
````{div} full-width
```{note}
Voilà une grande remarque
```
````

ou :

```{note}
:class: full-width
Voilà une grande remarque
```







## Code Python exécuté lors du build
### Config lors du build
https://jupyterbook.org/en/stable/content/execute.html



```{code-cell}
print(2 + 2)
```


```{code-cell}
:tags: [output_scroll]
for i in range(40):
    print(f"this is output line {i}")
```


```{code-cell} ipython3
---
render:
  image:
    width: 200px
    alt: logo
    classes: shadow bg-primary
  figure:
    caption: |
      Image chargée par IPython
    name: logo
---
from IPython.display import Image
Image("logo.png")
```






## Des maths
$e=mc^2$ ou 
$$e=mc^2$$ 

## Note bas de page
[^label] : Ma note de pdp.



## Autres
* faire interpréter du MD : https://jupyterbook.org/en/stable/content/code-outputs.html
* liens vers images, équations, etc : https://jupyterbook.org/en/stable/content/references.html
* [stocker des résultats de sortie Python pour les intégrer au livre](https://jupyterbook.org/en/stable/content/executable/output-insert.html)
* [ipywidgets et figure interactive](https://jupyterbook.org/en/stable/interactive/interactive.html)
* [construction du livre (pdf, html, etc.)](https://jupyterbook.org/en/stable/basics/build.html)
* [conversion en PDF](https://jupyterbook.org/en/stable/advanced/pdf.html)


```{seealso} Voir aussi
Jupyter Book uses [Jupytext](https://jupytext.readthedocs.io/en/latest/) to convert text-based files to notebooks, and can support [many other text-based notebook files](https://jupyterbook.org/file-types/jupytext.html).
```