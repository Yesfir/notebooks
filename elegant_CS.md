# VS Code
much credit to:  
https://github.com/Yang-Xijie  
shortcuts:  
1. option & cmd to choose word/line
2. cmd + N to create new file and name it immediately (self-defined)
3. shift + cmd + {} to change tabs
4. shift + opt + F to format with (e.g."Google")
5. Code Runner ("cmd + R" to run)
```
g++ hello_world.cpp -o hello.out -W -Wall -O2 -std=c++17
./hello.cpp
```
an example: 
```json
{
  // Code Runner
  // To run code:
  //   use shortcut "Ctrl Opt N" * or...
  // To stop the running code:
  //   use shortcut "Ctrl Opt M" * or...
  "code-runner.executorMap": {
    // Introduction:
    //   Make sure the executor PATH of each language is set in the environment variable.
    //   You could also add entry into "code-runner.executorMap" to set the executor PATH.
    // Supported customized parameters:
    //   $workspaceRoot: The path of the folder opened in VS Code
    //   $dir: The directory of the code file being run
    //   $fullFileName: The full name of the code file being run
    //   $fileName: The base name of the code file being run, that is the file without the directory
    //   $fileNameWithoutExt: The base name of the code file being run without its extension
    /* ------ 编译、运行只有一个文件的cpp文件 ------ */
    // 注：路径中有空格不会出现问题
    "cpp": "g++ $fullFileName -o $dir\"$fileNameWithoutExt\"\".out\" -W -Wall -O2 -std=c++17 && $dir\"$fileNameWithoutExt\"\".out\"",
    // 其中 $fullFileName 是绝对路径，是主文件
    // 自己决定是否加入 && rm $dir\"$fileNameWithoutExt\"\".out\"（也可以添加"files.exclude"）
    /* ------ 编译、运行多个cpp文件 ------ */
    // "cpp": "g++ $fullFileName <file_to_link> -o $dir\"$fileNameWithoutExt\"\".out\" -W -Wall -O2 -std=c++17 && $dir\"$fileNameWithoutExt\"\".out\"",
    // <file_to_link>的写法：
    //   一般的，你也可以直接写绝对路径
    //     \"/path/xxxx.cpp\"
    //   如果你链接的cpp文件和主文件在一个目录下：
    //     $dir\"xxxx.cpp\"
    //   更一般的，如果你链接的cpp文件不和主文件在一个目录下，需要从当前VSCode的工作目录补充相对路径从而形成绝对路径：
    //     $workspaceRoot\"relative/path/xxxx.cpp\"
    /* ------ 编译c文件 ------ */
    "c": "gcc $fullFileName -o $dir\"$fileNameWithoutExt\"\".out\" -W -Wall -O2 -std=c17 && $dir\"$fileNameWithoutExt\"\".out\"",
    // "c": "gcc $fullFileName <file_to_link> -o $dir\"$fileNameWithoutExt\"\".out\" -W -Wall -O2 -std=c17 && $dir\"$fileNameWithoutExt\"\".out\"",
  },
  // Whether to clear previous output before each run (default is false):
  "code-runner.clearPreviousOutput": true,
  // Whether to save all files before running (default is false):
  "code-runner.saveAllFilesBeforeRun": false,
  // Whether to save the current file before running (default is false):
  "code-runner.saveFileBeforeRun": true,
  // Whether to show extra execution message like [Running] ... and [Done] ... (default is true):
  "code-runner.showExecutionMessage": true, // cannot see that message is you set "code-runner.runInTerminal" to true
  // Whether to run code in Integrated Terminal (only support to run whole file in Integrated Terminal, neither untitled file nor code snippet) (default is false):
  "code-runner.runInTerminal": true, // cannot input data when setting to false
  // Whether to preserve focus on code editor after code run is triggered (default is true, the code editor will keep focus; when it is false, Terminal or Output Channel will take focus):
  "code-runner.preserveFocus": false,
  // Whether to ignore selection to always run entire file. (Default is false)
  "code-runner.ignoreSelection": true,
  // --------------------------------------------------------------------------------------
}
```
6. how to debug.
tasks.json
launch.json