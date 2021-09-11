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

> Ensuite, ajoutons les importations des modules tout en haut du code

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
folder_path = ""
output = Text(height=10, width=250, bg='#212422', foreground='white', selectbackground='#5865F2') # La sortie sera la même dans tous les onglets


# Ces ligne doit toujours être a la fin
compiler.mainloop()
```

### Onglets

Pour utiliser les onglets nous alons nous baser sur l'ouverture d'un dossier.
Pour commencer vous allez devoir créer cette classe:

```python
class Tab:
    def __init__(self, file):
        self.file = file
        tab = Frame(tabcontrol)
        if os.path.isfile(folder_path+"/"+file) and (file.endswith('.py') or file.endswith('.js') or file.endswith('.html') or file.endswith('.md') or file.endswith('.txt')):
            f = open(folder_path+"/"+file, 'r')
            code = f.read()
            f.close()
            run_btn = Button(tab, text="Run", command=(lambda: self.run())).pack()
            save_btn = Button(tab, text="Save", command=(lambda: self.save())).pack()
            text = Text(tab, height=50, width=250, bg='#545955', foreground='white', selectbackground='#5865F2', insertbackground='white')
            self.text = text
            text.insert(1.0, code)
            text.pack()
            tabcontrol.add(tab, text=file)
```

La suite arrive bientôt ...
