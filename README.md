# Base PHP extension in C language with VSCode Debugger setup

Clone this repository and navigate to the directory.  
Want to learn more about PHP extension development? Read more [here](https://medium.com/@bogkonstantin/php-extension-create-a-simple-extension-and-set-up-development-environment-6434e9b89103).

### Build image

```bash
docker build --pull --rm -f "Dockerfile" -t php-dev:latest "."
```

### Run container

```bash
docker run --rm --name php-dev -it php-dev bash
```

### Test function

Check if it works from inside the container:
```bash
php -r "echo hello_world() . PHP_EOL;"
```

### Debug configuration for Visual Studio Code

VSCode launch config (tested on Mac M2). Use [Docker Dev containers](https://code.visualstudio.com/docs/devcontainers/containers) in VSCode

```json
{
    "name": "Launch Test Function (gdb)",
    "type": "cppdbg",
    "request": "launch",
    "program": "/usr/local/bin/php",
    "args": [
        "-r",
        "echo hello_world() . PHP_EOL;",
    ],
    "cwd": ".",
    "MIMode": "gdb",
    "additionalSOLibSearchPath": "/php-src;/php-ext",
    "setupCommands": [
        {
            "description": "Enable pretty-printing for gdb",
            "text": "-enable-pretty-printing",
            "ignoreFailures": true
        }
    ]
}
```
