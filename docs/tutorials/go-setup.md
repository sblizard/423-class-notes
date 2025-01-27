# Setting Up a Dev Container for Go

By the end of this walkthrough, you should be able to:  
- Set up a dev container for Go  
- Create a Go program  
- Use a `go.mod` file to manage dependencies  
- Print "Hello, World!" to the terminal  
- Run your program  

## Preparing your workspace
Set up a dev container to manage your Go development environment. This avoids installing Go or other tools directly on your host machine.

Next, create a *.devcontainer* directory for your project:
```bash
$ mkdir hello
$ cd hello
```  

Next, create a *.devcontainer* directory to configure your development environment:
`$ mkdir devcontainer`  
`$ touch .devcontainer/devcontainer.json`  
Inside *devcontainer.json*, insert the following:  
```
{
  "name": "Go Dev Environment",
  "image": "mcr.microsoft.com/devcontainers/go:latest",
  "customizations": {
    "vscode": {
      "extensions": ["golang.go"]
    }
  }
}
```  
!!! Warning
    Ensure you open your project in VSCode and select Reopen in Container when prompted. This step builds and launches the dev container.  

## Verifying your setup
Once your dev container is up and running, verify that Go is installed by opening a terminal inside the container and running:  
```$ go version```

## Managing dependencies
Initalize your Go project by running the following command inside your project directory:  
`$ go mod init example/hello`  
This creates a go.mod file to track and manage your project dependencies. Open your project in VSCode and ensure the Go VSCode plugin is installed under the Extensions tab.  

## Creating your first Go program  
Create a new file named `hello.go`. Inside *hello.go*, add the following code:  
```
package main


import "fmt"


func main() {
    fmt.Println("Hello COMP423!")
}
```
This code creates a main package, imports [fmt](https://pkg.go.dev/fmt/) which contains functions retaining to formatting text, including printint it in terminal, and the main function.  

## Create your mod file
Create a `.mod` in order to track and manage your dependcies. Create it by running the following command:
```go mod init hello```

## Running your program  
In order to run you program use the following command:  
`$ go run .`  
You should expect the following to appear in terminal:  
`Hello COMP423!`  

## Building your program
To build your program you can use the following subcommand:  
`$ go build hello.go`  
This command generates a binary executable in the same directory named `hello` which contains the compuled, executable code that your machine can run without having to recompile. To run the executable, use the command:  
`./hello`

## Understanding the build subcommand
The `go build` command creates a binary executable file that you can run directly. This is similar to using `gcc` in COMP211 to compile a C program into an executable.

**Example (C Program in COMP211):**
`bash
gcc -o hello hello.c
./hello`

* Primary author: [Sean Blizard](https://github.com/sblizard)
* Reviewer: [Grace Odondi](https://github.com/godondi)