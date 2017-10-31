# How to use Visual Studio Code to build, run and test a Spring Boot application using Maven

1. Install **"Java Extension Pack"** https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack
2. Add the "Debug (Attach)" configuration to your **"launch.json"**:
```json
{
    "type": "java",
    "name": "Debug (Attach)",
    "request": "attach",
    "hostName": "localhost",
    "port": 8000
}
```
A quick way to do this is to type **Command+Shift+P** on Mac or **Ctrl+Shift+P** on Windows or Linux and type **"open launch.json"**

*Note: You may be able to use the "Debug (Launch)" but I wasn't able to get it to work. Maybe the future version of Java Debugger for VS Code fixes this issue.*
3. Add the following tasks to your **"tasks.json"**:
```json
"tasks": [
    {
        "taskName": "debug",
        "type": "shell",
        "command": "mvn spring-boot:run -Drun.jvmArguments=\"-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=y,address=8000\"",
        "group": "build"
    },
    {
        "taskName": "build",
        "type": "shell",
        "command": "mvn clean install",
        "group": "build"
    },
    {
        "taskName": "debug test",
        "type": "shell",
        "command": "mvnDebug test -DforkMode=never",
        "group": "test"
    },
    {
        "taskName": "test",
        "type": "shell",
        "command": "mvn test",
        "group": "test"
    }
]
```
A quick way to do this is to type **Command+Shift+P** on Mac or **Ctrl+Shift+P** on Windows or Linux and type **"configure task"** to create the tasks.json file.

## How to debug
1. Run the **"debug"** task by hitting **"Command+Shift+B"** on Mac or **"Ctrl+Shift+B"** on Windows or Linux and select **"Debug->Continue without scanning the task output"**.
2. As soon as you see "Listening for transport dt_socket at address: 8000", go to the Debug view in VS Code (Command+Shift+D/Ctrl+Shift+D) and hit play for **"Debug (Attach)"**.

## How to do a clean build
1. Run the **"build"** task by hitting **"Command+Shift+B"** on Mac or **"Ctrl+Shift+B"** on Windows or Linux and select **"Build->Continue without scanning the task output"**.

## How to run unit tests
1. Run the **"test"** task (**Command+Shift+P/Ctrl+Shift+P -> "Run test task" -> "test"**)

## How to debug unit tests
1. Run the **"debug test"** task (**Command+Shift+P/Ctrl+Shift+P -> "Run test task" -> "debug test"**)
2. As soon as you see "Listening for transport dt_socket at address: 8000", go to the Debug view in VS Code (Command+Shift+D/Ctrl+Shift+D) and hit play for **"Debug (Attach)**".