Bien! Voici donc le code de cette fin de chapitre:
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

bloc = False
def key_pressed(key):
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

# Vous pouvez les changer a votre guise
compiler.bind("<Control-o>", open_file)
compiler.bind("<Control-s>", save_as)
compiler.bind("<Control-a>", save_as)
compiler.bind("<Control-Key-5>", run)
compiler.bind("<Key>", key_pressed)

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

### Finitions 

Pour finir sur cet ide nous alons ajouter un menu popup. C'est très simple.
Ajoutez `compiler.bind('<Button-3>', popup)` dans les contrôles puis ajoutez cette fonction sous la dernière fonction key_pressed:
```python
def popup(e):
    drop_menu.tk_popup(e.x_root, e.y_root)
```

Ajoutez ensuite ce menu avec les autres
```python
drop_menu = Menu(menu_bar, tearoff=0)
drop_menu.add_command(label='Open', command=open_file)
drop_menu.add_command(label='Save', command=save_as)
drop_menu.add_command(label='Save As', command=save_as)
drop_menu.add_command(label='Exit', command=exit)
```

Testez maintenant de faire un clic droit. Le menu apparait!

Bien. Nous allons maintenant ajouter un texte qui nous avertis si le fichier est sauvegardé ou pas.
Pour commencer ajoutez ceci `status = Label(compiler, textvariable=status_value)` là ou nous avons précédement ajouter l'editeur

Ajoutez maintenant 
```python
else:
        file = f = open(file_path, 'r')
        if (file.read() != editor.get(1.0, END)):
            status_value.set("Not saved")
        else: 
            status_value.set("Saved")
            ```
dans la fonction key_pressed. Vous pouvez aussi ajouter `status_value.set("Saved")` dans la fonction save_as

### Conversion EXE

Pour la conversion en exe nous allons utiliser cx_Freeze. Tapez `pip install cx_Freeze` dans le terminal puis créez un fichier setup.py

Voici son contenu :

```python
import sys
from cx_Freeze import setup, Executable

# *Mettez ici les packages utilisés
build_exe_options = {"packages": ["os", "tkinter", "subprocess", "time", "sys", "tkhtmlview", "time", "markdown"]}


base = None
if sys.platform == "win32":
    base = "Win32GUI"

setup(
    name = "Mon ide", # Nom de votre app
    version = "0.1", # Version de l'app
    description = "IDE fait en Python", # Description de l'app
    options = {"build_exe": build_exe_options},
    executables = [Executable("code/main.py", base=base, icon="assets\logo.ico", targetName="FiveCode.exe")]
)
```