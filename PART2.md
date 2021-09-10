# Créer un ide complet en Python - Partie 2
## Pour commencer cette dexuième partie nous allons repartir de zéro. Bien sûr les connaisances acquises dans la partie 1 nous sevira dans cette partie.

## Chapitres<br>
1 - [](#application-de-base)<br>
2 - [](#système-de-fichiers)<br>
3 - [](#lancement-du-code)<br>
4 - [](#ajout-de-langages)<br>
5 - [](#importation-des-packages)<br>
6 - [](#contrôles)<br>
7 - [](https://github.com/liam-gen/idepython/blob/main/SUITE.md#finitions)<br>
8 - [](https://github.com/liam-gen/idepython/blob/main/SUITE.md#conversion-exe)<br>

### Application de base

**Pour commencer nous allons devoir importer quelques modules**<br>
\* signifie qu'il n'y a **pas besoin d'importer** le module car il est **déjà présent** sur votre ide
- Tkinter \* 
- Subprocess \*
- Sys \*
- Os \*
- Time \*
- Markdown `pip install markdown`
- TkHtmlView `pip install tkhtmlview`

> Bien voici notre code pour importer les modules

```python
# Importation des modules
from tkinter import *
from tkinter.ttk import Notebook
import subprocess
import os
import sys
from tkinter import filedialog
from tkinter.filedialog import asksaveasfilename, askopenfilename
import time
from tkhtmlview import HTMLLabel
from markdown import markdown
```

> Maintenant que tout ça est fait nous allons pouvoir commencer a créer l'application
- En dessous du précédent code ajoutez ceci
```python
compiler = Tk()
tabcontrol = Notebook(compiler) # Nouveauté (côntrole des onglets)
compiler.title("Mon éditeur de code") # Titre de votre app
compiler.geometry("900x700+500+150") # Taille de votre app
# La fonction os.path.abspath est requise pour convertir en EXE. Elle nous retourne le chemin entier du fichier (ex: os.path.abspath('main.py') retournera C:Users/User/Desktop/Votre Projet/main.py)
compiler.iconbitmap(os.path.abspath('votreimage.ico'))

# Ces ligne doit toujours être a la fin
compiler.mainloop()
```
La suite arrive prochainement ...
