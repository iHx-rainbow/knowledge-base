# gitignore 添加已推远程的文件

如果你不小心将应该被 `.gitignore` 忽略的目录推送到了远程仓库，你可以按照以下步骤来处理这个问题：

1.  **更新 `.gitignore` 文件：**\
    首先，确保你已经在 `.gitignore` 文件中添加了要忽略的目录。例如，如果要忽略的目录是 `dir_to_ignore`，那么 `.gitignore` 中应该有一行：

    ```
    dir_to_ignore/
    ```
2.  **删除缓存中的文件：**\
    即使你更新了 `.gitignore`，Git 仍然会追踪已经添加到版本控制中的文件。你需要从缓存中删除这些文件：

    ```bash
    git rm -r --cached dir_to_ignore/
    ```

    这个命令会从 Git 缓存中移除 `dir_to_ignore` 目录中的所有文件，但不会删除你的本地文件。
3.  **提交更改：**\
    现在，提交这个改动：

    ```bash
    git commit -m "Remove ignored directory from tracking"
    ```
4.  **推送到远程仓库：**\
    最后，推送你的更改到远程仓库：

    ```bash
    git push origin <branch_name>
    ```

    确保用你正在使用的分支名称替换 `<branch_name>`。

这样，远程仓库中将不会再包含被 `.gitignore` 忽略的目录。
