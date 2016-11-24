# repl

*   Node.js REPL

    ```
    .break    Sometimes you get stuck, this gets you out
    .clear    Alias for .break
    .editor   Enter editor mode
    .exit     Exit the repl
    .help     Print this help message
    .load     Load JS from a file into the REPL session
    .save     Save all evaluated commands in this REPL session to a file
    ```
    ```
    <ctrl>-C      pressed once(.break);   pressed twice(.exit)
    <ctrl>-D      Has the same effect as the .exit command
    <tab>         autocompletion
    ```

*   REPLServer

    ```
    repl.start([options])

    Events
      exit
      reset

    replServer.defineCommand(keyword, cmd)
    replServer.displayPrompt([preserveCursor])
    ```

