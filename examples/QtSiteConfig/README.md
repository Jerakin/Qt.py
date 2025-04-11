## `QtSiteConfig` example

This example illustrates how to make a QtSiteConfig module and how it affects Qt.py at run-time.

**Usage**

```bash
$ cd to/this/directory
$ python main.py
# Qt.QtCore was successfully removed by QSiteConfig.py
```

Because `QtSiteConfig.py` is in the current working directory, it is available to import by Python. If running from a different directory, then you can append this directory to your `PYTHONPATH`

```bash
$ set PYTHONPATH=path/to/QtSiteConfig/
$ python main.py
# Qt.QtCore was successfully removed by QSiteConfig.py
```

> Linux and MacOS users: Replace `set` with `export`

<br>

**Advanced examples**

If you need to you can also add modules that are not in the standard Qt.py. All of these functions are optional in QtSiteConfig, so only implement the functions you need.

#### QtSiteConfig.py: Adding non-standard modules

By default Qt.py only exposes the "lowest common denominator" of all bindings. This example shows how to add the Qsci module that is not included by default with Qt.py.

```python
def update_members(members):
    """An example of adding Qsci to Qt.py.

    Arguments:
        members (dict): The default list of members in Qt.py.
            Update this dict with any modifications needed.
    """

    # Include Qsci module for scintilla lexer support.
    members["Qsci"] = [
        "QsciAPIs",
        "QsciAbstractAPIs",
        "QsciCommand",
        "QsciCommandSet",
        "QsciDocument",
        "QsciLexer",
        "QsciLexerAVS",
        "QsciLexerBash",
        "QsciLexerBatch",
        "QsciLexerCMake",
        "QsciLexerCPP",
        "QsciLexerCSS",
        "QsciLexerCSharp",
        "QsciLexerCoffeeScript",
        "QsciLexerCustom",
        "QsciLexerD",
        "QsciLexerDiff",
        "QsciLexerFortran",
        "QsciLexerFortran77",
        "QsciLexerHTML",
        "QsciLexerIDL",
        "QsciLexerJSON",
        "QsciLexerJava",
        "QsciLexerJavaScript",
        "QsciLexerLua",
        "QsciLexerMakefile",
        "QsciLexerMarkdown",
        "QsciLexerMatlab",
        "QsciLexerOctave",
        "QsciLexerPO",
        "QsciLexerPOV",
        "QsciLexerPascal",
        "QsciLexerPerl",
        "QsciLexerPostScript",
        "QsciLexerProperties",
        "QsciLexerPython",
        "QsciLexerRuby",
        "QsciLexerSQL",
        "QsciLexerSpice",
        "QsciLexerTCL",
        "QsciLexerTeX",
        "QsciLexerVHDL",
        "QsciLexerVerilog",
        "QsciLexerXML",
        "QsciLexerYAML",
        "QsciMacro",
        "QsciPrinter",
        "QsciScintilla",
        "QsciScintillaBase",
        "QsciStyle",
        "QsciStyledText",
    ]
```


#### QtSiteConfig.py: Standardizing the location of Qt classes

Some classes have been moved to new locations between bindings. Qt.py uses the namespace dictated by PySide2 and most members are already in place.
This example reproduces functionality already in Qt.py but it provides a good example of how use this function.

```python
def update_misplaced_members(members):
    """This optional function is called by Qt.py to standardize the location
    and naming of exposed classes.

    Arguments:
        members (dict): The members considered by Qt.py
    """
    # Standardize the Property name
    members["PySide2"]["QtCore.Property"] = "QtCore.Property"
    members["PyQt5"]["QtCore.pyqtProperty"] = "QtCore.Property"
```
