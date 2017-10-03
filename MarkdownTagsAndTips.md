# Overview

Contains notes on using the Markdown file format.

# References

* [Markdown info](https://guides.github.com/features/mastering-markdown/)
* [Markdown Cheat Sheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

# Tip - Internal heading links (bookmark anchors)

To link internally to the "**## Git remote branch commands**" h2 heading enter:

```
[Remote branch commands](#git-remote-branch-commands)
```

Note that even though it is an h2 heading with two ##, the link only includes one #, with the space removed after it.  All subsequent spaces are replaced with hyphens, and all uppercase letters are converted to lowercase.  An easy way to get this right is to look at the rendered markdown file on GitHub and click on the link icon to the left of the heading you want to link to.  This will open the page in your browser at that heading where you can copy the bookmark name from the address bar.

# Tip - Syntax highlighting a block of code

\`\`\`python

import mysql.connector

cnx = mysql.connector.connect(user='root', password='xxxxxx',
                              host='127.0.0.1',
                              database='test')
cnx.close()

\`\`\`

results in:

```python

import mysql.connector

cnx = mysql.connector.connect(user='root', password='xxxxxx',
                              host='127.0.0.1',
                              database='test')
cnx.close()

```
