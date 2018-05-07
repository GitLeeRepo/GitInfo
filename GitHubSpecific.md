# Overview

Contains notes on GitHub specific commands

# Reference

* [GitHub Keyboard Reference](https://help.github.com/articles/using-keyboard-shortcuts/)

## My Own Notes

* [GitCommanNotes](https://github.com/GitLeeRepo/GitInfo/blob/master/GitCommandNotes.md#overview)
* [GitReferences](https://github.com/GitLeeRepo/GitInfo/blob/master/GitReferences.md#overview)
* [MarkdownTagsAndTips](https://github.com/GitLeeRepo/GitInfo/blob/master/MarkdownTagsAndTips.md#overview)

# Source / Text Editing

* **Ctrl-F** - Start searching in file editor
* **Ctrl-G** - Find next
* **Shift Ctrl-G** - Find previous
* **Shift Ctrl-F** - Replace
* **Shift Ctrl-R** - Replace all
* **Alt-G**	- Jump to line
* **Ctrl-Z** - 1Undo
* **Ctrl-Y** - Redo

# Add an Existing Remote Repository to a New GitHub Repository

1. Create an **empty** repository on GitHub.  Important: Don't add anything including README or gitignore.
2. Make sure remote git is committed and ready to go
3. Enter command **git remote add origin https://github.com/GitLeeRepo/\<GitHubRepoName>.git**
4. git push -u origin master

# Creating a Folder in the Web Interface

1. Click on the "New file" button.
2. Enter the name of the folder, followed by a foward slash (**/**), followed by a filename.  Note that you must include an initial file since GitHub will not create an empty folder, so provide something such as a README.md file.
3. Commit the changes.

# Max Repository size

From: [DiskQuota](https://help.github.com/articles/what-is-my-disk-quota/)

We recommend repositories be kept under 1GB each. This limit is easy to stay within if large files are kept out of the repository. If your repository exceeds 1GB, you might receive a polite email from GitHub Support requesting that you reduce the size of the repository to bring it back down.

In addition, we place a strict limit of files exceeding 100 MB in size. 
