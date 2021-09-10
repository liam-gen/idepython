# Créer un ide complet en Python - Partie 2
## Pour commencer cette dexuième partie nous allons repartir de zéro. Bien sûr les connaisances acquises dans la partie 1 nous sevira dans cette partie.

## Chapitres<br>
1 - [Application de base](#application-de-base)<br>
2 - [Système de fichiers](#système-de-fichiers)<br>
3 - [Lancement du code](#lancement-du-code)<br>
4 - [Ajout d'autres langages](#ajout-de-langages)<br>
5 - [Importation de packages](#importation-des-packages)<br>
6 - [Contrôles](#contrôles)<br>
7 - [Finitions](https://github.com/liam-gen/idepython/blob/main/SUITE.md#finitions)<br>
8 - [Convertion EXE](https://github.com/liam-gen/idepython/blob/main/SUITE.md#conversion-exe)<br>

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
