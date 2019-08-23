# tasks.json and launch.json for gfortran running on Linux

# Requirement
- Visual Studio Code
- gfortran
- gdb
- C/C++ extension by Microsoft (ms-vscode.cpptools)
C/C++ extensionは，gdbを利用するために必要です．

# Usage
## tasks.jsonとlaunch.jsonの配置
ソースファイルのあるディレクトリ以下に.vscodeディレクトリを作成し，tasks.jsonとlaunch.jsonを置いてください．

## 設定ファイルの編集
その後，ソースファイルの構成に従って，tasks.jsonとlaunch.jsonを編集してください．編集にあたり，VSCodeの変数が役に立ちます．

|変数名|意味|
|:--|:--|
|`${fileBasename}`|現在開いているファイル名|
|`${fileBasenameNoExtension}`|現在開いているファイル名（拡張子を除く）|
|`${workspaceFolder}`|VSCodeで開いているディレクトリ名（パスを含む）|
|`${workspaceFolderBasename}`|VSCodeで開いているディレクトリ名（パスを含まない）|

### tasks.json
- `PUT SOURCE-FILE-NAME HERE`をソースファイル(.f90)に書き換えてください．
- `PUT EXECUTABLE-FILE-NAME HERE`を実行ファイル名に書き換えてください．

```JSON
"args": [
    "-g",
    "-O0",
    "-o", "PUT EXECUTABLE-FILE-NAME HERE",
    "PUT SOURCE-FILE-NAME HERE"
],
```

#### 例1
hello.f90というソースファイルをコンパイルしてhello.outを作る場合．

```JSON
"args": [
    "-g",
    "-O0",
    "-o", "hello.out",
    "hello.f90"
],
```

#### 例2
VSCodeの変数を利用する場合．

```JSON
"args": [
    "-g",
    "-O0",
    "-o", "${workspaceFolder}/${fileBasenameNoExtension}.out",
    "${fileBasename}"
],
```

### launch.json
- `PUT EXECUTABLE-FILE-NAME HERE`を実行ファイル名に書き換えてください．
- `PUT WORKIND DIRECTORY HERE`を実行ファイルのあるパスに書き換えてください．

```JSON
"program": "PUT EXECUTABLE-FILE-NAME HERE",
"cwd": "PUT WORKIND DIRECTORY HERE",
```

#### 例

```JSON
"program": "${workspaceFolder}/${fileBasenameNoExtension}.out",
"cwd": "${workspaceFolder}",
```
