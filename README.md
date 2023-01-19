# SortFiles
Small program to quicky sort files into folders.

## Prerequisites
```
py -3 -m pip install -U easygui
```

## Code
```py
import easygui
import os
import shutil
# open a directory dialog
path = easygui.diropenbox()
# check if pressed cancel
if path == None: exit()
# list for saved filetypes
satisfied_filetypes = [ ]
for file in os.listdir(path):
    # skip directories
    if os.path.isdir(file):
        continue
    index = file.rfind('.')
    if index < 0:
        continue
    extension = file[index:]
    # check if extension is long enough
    if len(extension) < len('.js'): 
        continue
    # check if we've already created a folder
    if extension not in satisfied_filetypes:
        satisfied_filetypes.append(extension)
        # create a new folder for the extension
        try: os.makedirs(path + f"\\{extension[1:]}")
        except: pass
    # finally, move the file over to the new directory
    shutil.move(path + f"\\{file}", path + f"\\{extension[1:]}\\{file}")
```
