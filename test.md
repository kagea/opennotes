---
layout: post
title: Test
permalink: /test/
---

Some information about you!

### More Information

A place to include any other types of information that you'd like to include about yourself.

### Contact me

[kage.anaguma@gmail.com](mailto:kage.abaguma@gmail.com)


### Some test of code highlighting

```powershell
Get-AdComputer -Filter * | Sort-Object -Name
```

```python
#!/usr/bin/env python
__author__ = 'me'

import sys
from PySide.QtCore import *
from PySide.QtGui import *

__appname__ = "Eight Video"

class Program(QDialog):

    def __init__(self, parent=None):
        super(Program, self).__init__(parent)

        openButton = QPushButton("Open")
        saveButton = QPushButton("Save")
        dirButton = QPushButton("Other")
        closeButton = QPushButton("Close...")
        self.connect(openButton, SIGNAL("clicked()"), self.open)

        layout = QVBoxLayout()
        layout.addWidget(openButton)
        layout.addWidget(saveButton)
        layout.addWidget(dirButton)
        layout.addWidget(closeButton)
        self.setLayout(layout)

    def open(self):
        dir = "."
        fileObj = QFileDialog.getOpenFileName(self, __appname__+ "Open File Dialog",dir = dir, filter="Text files (*.txt)")
        print(fileObj)
        print(type(fileObj))

app = QApplication(sys.argv)
form = Program()
form.show()
app.exec_()
```

This is a test 3
