# Linux 常用命令

#### `sed` (Stream Editor)

1.  **替换文本**

    ```sh
    sed 's/原文本/新文本/' 文件名
    ```

    将匹配的文本替换为新文本。
2.  **删除行**

    ```sh
    sed 'Nd' 文件名
    ```

    删除指定行。
3.  **显示特定行**

    ```sh
    sed -n 'Np' 文件名
    ```

    仅显示指定行。
4.  **插入文本**

    ```sh
    sed 'N i\插入的文本' 文件名
    ```

    在指定行前插入文本。
5.  **追加文本**

    ```sh
    sed 'N a\追加的文本' 文件名
    ```

    在指定行后追加文本。

#### `awk`

1.  **打印特定列**

    ```sh
    awk '{print $N}' 文件名
    ```

    打印指定列。
2.  **条件打印**

    ```sh
    awk '条件 {print $N}' 文件名
    ```

    满足条件时打印指定列。
3.  **计算和**

    ```sh
    awk '{sum += $N} END {print sum}' 文件名
    ```

    计算列的总和。
4.  **格式化输出**

    ```sh
    awk '{printf "格式", $N}' 文件名
    ```

    以指定格式输出。
5.  **统计行数**

    ```sh
    awk 'END {print NR}' 文件名
    ```

    统计总行数。

#### `grep`

1.  **搜索文本**

    ```sh
    grep 'pattern' 文件名
    ```

    搜索匹配模式的行。
2.  **递归搜索**

    ```sh
    grep -r 'pattern' 目录名
    ```

    在目录中递归搜索匹配模式的文件。

#### `cut`

1.  **提取特定列**

    ```sh
    cut -d '分隔符' -f N 文件名
    ```

    提取指定列。
2.  **提取特定字符范围**

    ```sh
    cut -c M-N 文件名
    ```

    提取指定字符范围。

#### `sort`

1.  **基本排序**

    ```sh
    sort 文件名
    ```

    对文本进行字母顺序排序。
2.  **按数字排序**

    ```sh
    sort -n 文件名
    ```

    对文本进行数值排序。

#### `uniq`

1.  **删除重复行**

    ```sh
    uniq 文件名
    ```

    删除重复行。
2.  **统计重复行**

    ```sh
    uniq -c 文件名
    ```

    统计每行重复的次数。

#### `tr`

1.  **替换字符**

    ```sh
    tr '原字符' '新字符' < 文件名
    ```

    替换字符。
2.  **删除字符**

    ```sh
    tr -d '字符' < 文件名
    ```

    删除字符。

#### `head` 和 `tail`

1.  **查看前 N 行**

    ```sh
    head -n N 文件名
    ```

    查看文件的前 N 行。
2.  **查看后 N 行**

    ```sh
    tail -n N 文件名
    ```

    查看文件的后 N 行。

#### `wc`

1.  **统计行数、单词数和字符数**

    ```sh
    wc 文件名
    ```

    统计文件的行数、单词数和字符数。
2.  **仅统计行数**

    ```sh
    wc -l 文件名
    ```

    仅统计文件的行数。

这些命令可以组合使用，通过管道 (`|`) 将一个命令的输出作为下一个命令的输入，处理复杂的文本操作任务。例如，以下命令组合了 `grep`、`sort` 和 `uniq`：

```sh
grep 'error' 文件名 | sort | uniq -c | sort -nr
```

这样可以搜索包含 "error" 的行，并按重复次数进行排序。