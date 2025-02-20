<web>

## Using Source Control in Web Studio


The Fabric Web Studio has an integrated source control management (SCM) system and it includes [Git](https://git-scm.com/) support in-the-box.

The Source Control <img src="images/web/scm.png" style="zoom:7%;" /> icon in the Activity Bar on the left-most menu provides an **indication of how many changes** you currently have in your repository.



Clicking the icon will show the details of your current repository changes: **CHANGES**, **STAGED CHANGES** and **MERGE CHANGES**.

> Tip: To bring the Source Control View up, you can also use the keyboard shortcut `CTRL+SHIFT+G`.

Clicking each item will show you in detail **the textual changes within each file**. Note that for unstaged changes, the editor on the right still lets you edit the file.

You can also find indicators of the **status of your repository** at the bottom-left corner of the status bar: the **current branch**, **dirty indicators**, and the number of **incoming and outgoing commits** of the current branch. You can **checkout** any branch in your repository by clicking that status indicator and selecting the Git reference from the list.



## Commit

**Staging** (Git add) and **unstaging** (Git reset) can be done either via contextual actions in the files or by a drag-and-drop feature.

You can type a commit message above the changes and press `Ctrl+Enter` (macOS: `⌘+Enter`) to commit them. When committing - it will look for staged changes and commit them. If all changes are un-staged, you will be asked to select them first and then to commit them.

More specific **Commit** actions can be found in the **Views and More Actions** `...`  (ellipsis) menu at the top of the Source Control view.



> **Tip:** If you commit your change to the wrong branch, undo your commit using the **Git: Undo Last Commit** command in the **Command Palette**.



## Git Status Bar Actions

There is a **Synchronize Changes** action icon in the Status Bar, next to the branch indicator; when clicked, it pulls remote changes down to your local repository and then pushes local commits to the upstream branch.



## Gutter Indicators

If you open a folder that is a Git repository and begin making changes, Web Studio will add useful annotations to the gutter and to the overview ruler. These annotations appear near the line numbers.

* A red triangle indicates where lines have been deleted
* A green bar indicates new added lines
* A blue bar indicates modified lines



## Merge Conflicts

Merge conflicts are recognized by Web Studio. Differences are highlighted and there are inline actions to accept either one or both changes. Once the conflicts are resolved, stage the conflicting file so you can commit those changes.



## Viewing Diffs

The Git tool supports viewing of diffs within Web Studio, showing both the original and the modified files, side by side. To view the differences between them, double-click on the file name.  



[![Previous](/articles/images/Previous.png)](/articles/04_fabric_studio/24_web_debug.md)
[<img align="right" width="60" height="54" src="/articles/images/Next.png">](/articles/04_fabric_studio/25_web_data_explorer.md)

</web>
