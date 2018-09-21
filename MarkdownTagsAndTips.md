# Overview

Contains notes on using the Markdown file format.

# References

* [Markdown info](https://guides.github.com/features/mastering-markdown/)
* [Markdown Cheat Sheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

# Image Tags

```
![GitHub Logo](/images/logo.png)
Format: ![Alt Text](url)
```

# Inline HTML

You can **embed inline HTML** for many HTML tags.

## HTML Table for Side-by-Side Images

```html
<table style="width:100%">
  <tr style="padding:4px; margin:0;">
    <td style="padding:2px; margin:0;">
      <img src="/Images/DockerVmCompareVm01.png" alt="DockerVmCompareVm01" width="448" height="448">
    </td>
    <td style="padding:2px; margin:0;">
      <img src="/Images/DockerVmCompareDocker01.png" alt="DockerVmCompareDocker01" width="448" height="448">
    </td>
  </tr>
</table>
```

# Block Quotes

Note that when using **block quotes** with the **\>** at the beginning of the line, it is not necessary to put in **line feeds**.  One **\>** symbol will be sufficient for text that wraps from one line to the next.   Keep in mind that a new paragraph needs to start with its own **block quote symbol**

Also note that you can continue to use **markdown codes** such as **bolding** within the quote.

> Multiple wrapping lines with a single **block quote indicator**: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras vitae facilisis neque. Maecenas nec mattis ante, quis auctor felis. Integer pulvinar ullamcorper lacus a aliquam. Nulla lacus sapien, rutrum sed justo sodales, vestibulum molestie velit. 

> But a new paragraph needs to start with its own **block quote symbol**: Donec malesuada semper ex maximus sagittis. In hac habitasse platea dictumst. Ut eget pulvinar quam, in mollis orci. Ut efficitur urna eros, ac cursus tortor mollis quis. Sed elementum dapibus placerat. 

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
