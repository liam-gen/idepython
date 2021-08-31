# Créer un ide complet en Python

##Chapitres:<br>
1 - [Application de base](#application-de-base)<br>
2 - Système de fichiers<br>
3 - Lancement du code<br>
4 - Ajout d'autres langages<br>
5 - Importation de packages<br>
6 - Contrôles<br>
7 - Ponctuation<br>
8 - Convertion ex EXE<br>

## Prérequis
- Python 3.9.0<br>
- Un ide _commique quand on sait qu'on va en créer un :)_<br>

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
import tkinter
from tkinter import *
from tkinter.filedialog import asksaveasfilename, askopenfilename
import subprocess
import time
import sys
import os
from tkhtmlview import HTMLLabel
from markdown import markdown
```

> Maintenant que tout ça est fait nous allons pouvoir commencer a créer l'application
- En dessous du précédent code ajoutez ceci
```python
compiler = Tk()
compiler.title("Mon éditeur de code") # Titre de votre app
compiler.geometry("900x700+500+150") # Taille de votre app
compiler.iconbitmap(os.path.abspath('votreimage.ico')) # Utilisez bien la fonction os.path.abspath pour avoir le tout le path. Ce sera utile quand nous convertirons l'app en EXE

# Cette ligne doit toujours être a la fin
compiler.mainloop()
```

Ce qui vous donne : 
![Application basique](https://images.liamgen.repl.co/1.png)

Ajoutons un menu

```python
```

### Système de fichiers

Ajoutons ceci 
```python
def 
```
