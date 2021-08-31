# Créer un ide complet en Python

## Chapitres:<br>
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
# La fonction os.path.abspath est requise pour convertir en EXE
compiler.iconbitmap(os.path.abspath('votreimage.ico'))

# Ajoutons l'éditeur
editor = Text(height=55, width=250, bg='#545955', foreground='white', selectbackground='#5865F2', insertbackground='white') #  A modifier a votre guise

# Ces ligne doit toujours être a la fin
editor.pack()
compiler.mainloop()
```

Ce qui vous donne : 
![Application basique](https://images.liamgen.repl.co/1.png)

Ajoutons un menu

```python
# Menu
menu_bar = Menu(compiler)

file_menu = Menu(menu_bar, tearoff=0)
file_menu.add_command(label="New file", command=new_file)
file_menu.add_command(label='Open Ctrl+O', command=open_file)
file_menu.add_command(label='Save Ctrl+S', command=save_as)
file_menu.add_command(label='Exit', command=exit)
menu_bar.add_cascade(label='File', menu=file_menu)
```

**Au dessus** de ce menu nous viendrons ajouter les fonctions new, open, save et exit et une variable contenant le path

```python
file_path = ""

def set_file_path(path):
    global file_path
    file_path = path

def new_file(*args):
    set_file_path("")
    editor.delete(1.0, END)
    editor.insert(1.0, '=> Nouveau Fichier <=')
    compiler.title(f'Mon éditeur de code - Untitled')
    
def open_file(*args):
    path = askopenfilename()
    set_current_file(path)
    with open(path, 'r') as file:
        code = file.read()
        editor.delete('1.0', END)
        editor.insert('1.0', code)
        set_file_path(path)
        compiler.title(f'FiveCode - {path}')
  
def save_as(*args):
    global file_path
    if file_path == '':
        path = asksaveasfilename()
        compiler.title(f'FiveCode - {path}')
        set_current_file(path)
    else:
        path = file_path
    with open(path, 'w') as file:
        code = editor.get('1.0', END)
        file.write(code)
        set_file_path(path)
    
def exit(*args):
    sys.exit()
        
```

### Système de fichiers

Ajoutons ceci 
```python
def 
```
