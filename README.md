# Créer un ide complet en Python

_Cela pourrais vous paraître beaucoup si vous regardez tout mais c'est beaucoup de répétions (ex: a chaque fin de chapitre je remontre l'entièreté du code)_<br><br>
**C'est parti!**<br><br>
## Chapitres:<br>
1 - [Application de base](#application-de-base)<br>
2 - [Système de fichiers](#système-de-fichiers)<br>
3 - [Lancement du code](#lancement-du-code)<br>
4 - [Ajout d'autres langages](#ajout-de-langages)<br>
5 - [Importation de packages](#importation-des-packages)<br>
6 - [Contrôles](#controles)<br>
7 - [Finitions](https://github.com/liam-gen/idepython/blob/main/SUITE.md#finitions)<br>
8 - [Convertion EXE](https://github.com/liam-gen/idepython/blob/main/SUITE.md#conversion-exe)<br>

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
![Application basique](https://images.liamgen.repl.co/2.png)

Bien c'est déjà le fin de ce chapitre. Voici le résumé du code
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

compiler = Tk()
compiler.title("Mon éditeur de code") # Titre de votre app
compiler.geometry("900x700+500+150") # Taille de votre app
# La fonction os.path.abspath est requise pour convertir en EXE
compiler.iconbitmap(os.path.abspath('botdiscord.png'))

# Ajoutons l'éditeur
editor = Text(height=55, width=250, bg='#545955', foreground='white', selectbackground='#5865F2', insertbackground='white') #  A modifier a votre guise

# Ces ligne doit toujours être a la fin
editor.pack()
compiler.mainloop()
```

### Système de fichiers

Ajoutons un menu pour les fichiers

```python
# Menu
menu_bar = Menu(compiler)

file_menu = Menu(menu_bar, tearoff=0)
file_menu.add_command(label="New file", command=new_file)
file_menu.add_command(label='Open Ctrl+O', command=open_file)
file_menu.add_command(label='Save Ctrl+S', command=save_as)
file_menu.add_command(label='Exit', command=exit)
menu_bar.add_cascade(label='File', menu=file_menu)

compiler.config(menu=menu_bar)
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
    else:
        path = file_path
    with open(path, 'w') as file:
        code = editor.get('1.0', END)
        file.write(code)
        set_file_path(path)
    
def exit(*args):
    sys.exit()
        
```

Nous avons maintenant ceci:
![Application basique](https://images.liamgen.repl.co/3.png)

Bien! Voici notre code maintenant:

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

compiler = Tk()
compiler.title("Mon éditeur de code") # Titre de votre app
compiler.geometry("900x700+500+150") # Taille de votre app
# La fonction os.path.abspath est requise pour convertir en EXE
compiler.iconbitmap(os.path.abspath('botdiscord.png'))

# Ajoutons l'éditeur
editor = Text(height=55, width=250, bg='#545955', foreground='white', selectbackground='#5865F2', insertbackground='white') #  A modifier a votre guise

# Système de fichiers

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
    else:
        path = file_path
    with open(path, 'w') as file:
        code = editor.get('1.0', END)
        file.write(code)
        set_file_path(path)
    
def exit(*args):
    sys.exit()

#Menu
menu_bar = Menu(compiler)

file_menu = Menu(menu_bar, tearoff=0)
file_menu.add_command(label="New file", command=new_file)
file_menu.add_command(label='Open Ctrl+O', command=open_file)
file_menu.add_command(label='Save Ctrl+S', command=save_as)
file_menu.add_command(label='Exit', command=exit)
menu_bar.add_cascade(label='File', menu=file_menu)

compiler.config(menu=menu_bar)
# Ces ligne doit toujours être a la fin
editor.pack()
compiler.mainloop()
```

### Lancement du code
Tout d'abord ajpouton le code output (*sortie de code*) juste a coté du text editor écrivez ceci:

```python
code_output = Text(height=10, width=250, bg='#212422', foreground='white', selectbackground='#5865F2')
```

Puis ajoutez ceci dans les dernières lignes de code:

```python
code_output.pack()
```

Ajoutons ensuite un menu pour lancer le fichier. Ajoutez le juste après le menu de fichiers

```python
run_bar = Menu(menu_bar, tearoff=0)
run_bar.add_command(label='Run Ctrl+5', command=run)
menu_bar.add_cascade(label='Run', menu=run_bar)
```

Ajoutons en dessous des autres fonctions la fonction permettant de lancer le code

```python
def run(*args):
    # Sauvagarder le fichier si il ne l'est pas
    if file_path == '':
        path = asksaveasfilename()
        compiler.title(f'FiveCode - {path}')
    else:
        path = file_path
    with open(path, 'w') as file:
        code = editor.get('1.0', END)
        file.write(code)
        set_file_path(path)
        
    # Pour l'instant nous lancerons que du code Python mais nous modifirons cela plus tard
    command = f'python {file_path}'
    process = subprocess.Popen(command, stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True)
    output, error = process.communicate()
    code_output.insert('1.0', output)
    code_output.insert('1.0',  error)
```

Voici le rendu:
![Lancer le code](https://images.liamgen.repl.co/4.png)

Voici donc notre code actuellement:
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

compiler = Tk()
compiler.title("Mon éditeur de code") # Titre de votre app
compiler.geometry("900x700+500+150") # Taille de votre app
# La fonction os.path.abspath est requise pour convertir en EXE
compiler.iconbitmap(os.path.abspath('botdiscord.png'))

# Ajoutons l'éditeur
editor = Text(height=55, width=250, bg='#545955', foreground='white', selectbackground='#5865F2', insertbackground='white') #  A modifier a votre guise
code_output = Text(height=10, width=250, bg='#212422', foreground='white', selectbackground='#5865F2')

# Système de fichiers

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

    else:
        path = file_path
    with open(path, 'w') as file:
        code = editor.get('1.0', END)
        file.write(code)
        set_file_path(path)
    
def exit(*args):
    sys.exit()

def run(*args):
    # Sauvagarder le fichier si il ne l'est pas
    if file_path == '':
        path = asksaveasfilename()
        compiler.title(f'FiveCode - {path}')
    else:
        path = file_path
    with open(path, 'w') as file:
        code = editor.get('1.0', END)
        file.write(code)
        set_file_path(path)
        
    # Pour l'instant nous lancerons que du code Python mais nous modifirons cela plus tard
    command = f'python {file_path}'
    process = subprocess.Popen(command, stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True)
    output, error = process.communicate()
    code_output.insert('1.0', output)
    code_output.insert('1.0',  error)



#Menu
menu_bar = Menu(compiler)

file_menu = Menu(menu_bar, tearoff=0)
file_menu.add_command(label="New file", command=new_file)
file_menu.add_command(label='Open Ctrl+O', command=open_file)
file_menu.add_command(label='Save Ctrl+S', command=save_as)
file_menu.add_command(label='Exit', command=exit)
menu_bar.add_cascade(label='File', menu=file_menu)

run_bar = Menu(menu_bar, tearoff=0)
run_bar.add_command(label='Run Ctrl+5', command=run)
menu_bar.add_cascade(label='Run', menu=run_bar)

compiler.config(menu=menu_bar)
# Ces ligne doit toujours être a la fin
editor.pack()
code_output.pack()
compiler.mainloop()
```

### Ajout de langages

Pour ajouter d'autres langages nous allons nous fier a l'extension du fichier (.py, .js, .html, ...)
Rendez vous dans la fonction run

```python
def run(*args):
    if file_path == '':
        path = asksaveasfilename()
        compiler.title(f'FiveCode - {path}')
    else:
        path = file_path
    with open(path, 'w') as file:
        code = editor.get('1.0', END)
        file.write(code)
        set_file_path(path)


    if file_path.endswith('.js'):
        command = f'node {file_path}'
    elif file_path.endswith('.py'):
        command = f'python {file_path}'
    elif file_path.endswith('.html'):
        create_html_window(editor.get(1.0, END))
    elif file_path.endswith('.md'):
        create_markdown_window(editor.get(1.0, END))
    else: return
    process = subprocess.Popen(command, stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True)
    output, error = process.communicate()
    code_output.insert('1.0', output)
    code_output.insert('1.0',  error)
```

Nous allons ajouter les fonctions pour créer des fenêtres html et markdown

Rendez vous **au dessus** de la fonction run puis ajoutez ceci:

```python
# Nous utilisons ici le module tkhtmlview
def create_html_window(html):
    htmlwindow = Toplevel()
    htmlwindow.title("localhost")
    frame = HTMLLabel(htmlwindow, html=html)
    frame.pack(expand=True, fill="both")

def create_markdown_window(md):
    htmlwindow = Toplevel()
    htmlwindow.title("Markdown")
    html = markdown(md)
    frame = HTMLLabel(htmlwindow, html=html)
    frame.pack(expand=True, fill="both")
```

Voici notre bel ide après ces changements:
![Ajout de langages](https://images.liamgen.repl.co/5.png)

Et voici notre code comme a chaque fin de chapitre:<br>

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

compiler = Tk()
compiler.title("Mon éditeur de code") # Titre de votre app
compiler.geometry("900x700+500+150") # Taille de votre app
# La fonction os.path.abspath est requise pour convertir en EXE
compiler.iconbitmap(os.path.abspath('botdiscord.png'))

# Ajoutons l'éditeur
editor = Text(height=55, width=250, bg='#545955', foreground='white', selectbackground='#5865F2', insertbackground='white') #  A modifier a votre guise
code_output = Text(height=10, width=250, bg='#212422', foreground='white', selectbackground='#5865F2')

# Système de fichiers

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

    else:
        path = file_path
    with open(path, 'w') as file:
        code = editor.get('1.0', END)
        file.write(code)
        set_file_path(path)
    
def exit(*args):
    sys.exit()

# Nous utilisons ici le module tkhtmlview
def create_html_window(html):
    htmlwindow = Toplevel()
    htmlwindow.title("localhost")
    frame = HTMLLabel(htmlwindow, html=html)
    frame.pack(expand=True, fill="both")

def create_markdown_window(md):
    htmlwindow = Toplevel()
    htmlwindow.title("Markdown")
    html = markdown(md)
    frame = HTMLLabel(htmlwindow, html=html)
    frame.pack(expand=True, fill="both")

def run(*args):
    if file_path == '':
        path = asksaveasfilename()
        compiler.title(f'FiveCode - {path}')
    else:
        path = file_path
    with open(path, 'w') as file:
        code = editor.get('1.0', END)
        file.write(code)
        set_file_path(path)


    if file_path.endswith('.js'):
        command = f'node {file_path}'
    elif file_path.endswith('.py'):
        command = f'python {file_path}'
    elif file_path.endswith('.html'):
        create_html_window(editor.get(1.0, END))
    elif file_path.endswith('.md'):
        create_markdown_window(editor.get(1.0, END))
    else: return
    process = subprocess.Popen(command, stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True)
    output, error = process.communicate()
    code_output.insert('1.0', output)
    code_output.insert('1.0',  error)

#Menu
menu_bar = Menu(compiler)

file_menu = Menu(menu_bar, tearoff=0)
file_menu.add_command(label="New file", command=new_file)
file_menu.add_command(label='Open Ctrl+O', command=open_file)
file_menu.add_command(label='Save Ctrl+S', command=save_as)
file_menu.add_command(label='Exit', command=exit)
menu_bar.add_cascade(label='File', menu=file_menu)

run_bar = Menu(menu_bar, tearoff=0)
run_bar.add_command(label='Run Ctrl+5', command=run)
menu_bar.add_cascade(label='Run', menu=run_bar)

compiler.config(menu=menu_bar)
# Ces ligne doit toujours être a la fin
editor.pack()
code_output.pack()
compiler.mainloop()
```

### Importation des packages

Déjà nous allons créer un menu avec comme command import_package. Je pense que vous savez le faire, je vais donc vous épargner ce détail. Nous allons ensuite ajouter ces codes en dessous de la fonction run

```python
def import_package(*args):
    global pckg_input
    global install_window
    install_window = Toplevel()
    install_window.title('Insller un package')
    pckg_input = entree = Entry(install_window, width=50, bg='#545955', foreground='white') # Password : show="*"
    installbtn = Button(install_window, text="Installer", command=install).pack()
    pckg_input.pack()

def install(*args):
    global pckg_input
    global install_window
    package = pckg_input.get()
    if file_path == '':
        path = asksaveasfilename()
        compiler.title(f'FiveCode - {path}')
    else:
        path = file_path
    if file_path.endswith('.js'):
        command = f'npm i {package}'
    elif file_path.endswith('.py'):
        command = f'pip install {package}'
    process = subprocess.Popen(command, stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True)
    output, error = process.communicate()
    code_output.insert('1.0', output)
    code_output.insert('1.0',  error)
    install_window.destroy()
```

Bien vous pouvez maintenant importer des packages

Voici notre code pour ceux qui n'auraient pas compris

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

compiler = Tk()
compiler.title("Mon éditeur de code") # Titre de votre app
compiler.geometry("900x700+500+150") # Taille de votre app
# La fonction os.path.abspath est requise pour convertir en EXE
compiler.iconbitmap(os.path.abspath('botdiscord.png'))

# Ajoutons l'éditeur
editor = Text(height=55, width=250, bg='#545955', foreground='white', selectbackground='#5865F2', insertbackground='white') #  A modifier a votre guise
code_output = Text(height=10, width=250, bg='#212422', foreground='white', selectbackground='#5865F2')

# Système de fichiers

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

    else:
        path = file_path
    with open(path, 'w') as file:
        code = editor.get('1.0', END)
        file.write(code)
        set_file_path(path)
    
def exit(*args):
    sys.exit()

# Nous utilisons ici le module tkhtmlview
def create_html_window(html):
    htmlwindow = Toplevel()
    htmlwindow.title("localhost")
    frame = HTMLLabel(htmlwindow, html=html)
    frame.pack(expand=True, fill="both")

def create_markdown_window(md):
    htmlwindow = Toplevel()
    htmlwindow.title("Markdown")
    html = markdown(md)
    frame = HTMLLabel(htmlwindow, html=html)
    frame.pack(expand=True, fill="both")

def run(*args):
    if file_path == '':
        path = asksaveasfilename()
        compiler.title(f'FiveCode - {path}')
    else:
        path = file_path
    with open(path, 'w') as file:
        code = editor.get('1.0', END)
        file.write(code)
        set_file_path(path)


    if file_path.endswith('.js'):
        command = f'node {file_path}'
    elif file_path.endswith('.py'):
        command = f'python {file_path}'
    elif file_path.endswith('.html'):
        create_html_window(editor.get(1.0, END))
    elif file_path.endswith('.md'):
        create_markdown_window(editor.get(1.0, END))
    else: return
    process = subprocess.Popen(command, stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True)
    output, error = process.communicate()
    code_output.insert('1.0', output)
    code_output.insert('1.0',  error)

def import_package(*args):
    global pckg_input
    global install_window
    install_window = Toplevel()
    install_window.title('Insller un package')
    pckg_input = entree = Entry(install_window, width=50, bg='#545955', foreground='white') # Password : show="*"
    installbtn = Button(install_window, text="Installer", command=install).pack()
    pckg_input.pack()

def install(*args):
    global pckg_input
    global install_window
    package = pckg_input.get()
    if file_path == '':
        path = asksaveasfilename()
        compiler.title(f'FiveCode - {path}')
    else:
        path = file_path
    if file_path.endswith('.js'):
        command = f'npm i {package}'
    elif file_path.endswith('.py'):
        command = f'pip install {package}'
    process = subprocess.Popen(command, stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True)
    output, error = process.communicate()
    code_output.insert('1.0', output)
    code_output.insert('1.0',  error)
    install_window.destroy()

#Menu
menu_bar = Menu(compiler)

file_menu = Menu(menu_bar, tearoff=0)
file_menu.add_command(label="New file", command=new_file)
file_menu.add_command(label='Open Ctrl+O', command=open_file)
file_menu.add_command(label='Save Ctrl+S', command=save_as)
file_menu.add_command(label='Exit', command=exit)
menu_bar.add_cascade(label='File', menu=file_menu)

run_bar = Menu(menu_bar, tearoff=0)
run_bar.add_command(label='Run Ctrl+5', command=run)
menu_bar.add_cascade(label='Run', menu=run_bar)

pckg_bar = Menu(menu_bar, tearoff=0)
pckg_bar.add_command(label="Import Package", command=import_package)
menu_bar.add_cascade(label="Packages", menu=pckg_bar)

compiler.config(menu=menu_bar)
# Ces ligne doit toujours être a la fin
editor.pack()
code_output.pack()
compiler.mainloop()
```

### Contrôles

Pour ajouter des raccourcis vous devez définir des contrôles

Vous devez placer ces lignes entre le menu et les fonctions d'importation des modules

```python
# Vous pouvez les changer a votre guise
compiler.bind("<Control-o>", open_file)
compiler.bind("<Control-s>", save_as)
compiler.bind("<Control-a>", save_as)
compiler.bind("<Control-Key-5>", run)
```

Puis pour ajouter la ponctuation (*ex: le fait que quand on mette un guillemet, un autre se place après et la curseur se replace au milieu, ...*)
Ajoutez `compiler.bind("<Key>", key_pressed)` en dessous des autres contrôles. Ensuite en dessous des fonctions d'importation de modules créez cette fonction:
```python
bloc = False
def key_pressed(key):
    print(key)
    global bloc
    position = editor.index(INSERT)
    x = position.split(".")[0]
    y = position.split(".")[1]
    if key.keysym == "quoteright":
        editor.insert(position, "}")
        editor.mark_set("insert", f"{x}.{y}")
    if key.keysym == "colon":
        bloc = True
    if key.keysym == "parenleft":
        editor.insert(position, ")")
        editor.mark_set("insert", f"{x}.{y}")
    if key.keysym == "quotedbl":
        editor.insert(position, "\"")
        editor.mark_set("insert", f"{x}.{y}")
    if key.keysym == "Return" and bloc == True:
        editor.insert(position, "\t")

    if key.keysym == "BackSpace" and bloc == True and key.char == "\x08":
        bloc = False
    if not file_path:
        return
```

La suite se passe dans le fichier [`SUITE.md`](https://github.com/liam-gen/idepython/blob/main/SUITE.md)
