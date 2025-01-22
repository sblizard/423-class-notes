# Setting up a dev container for Go

By the end of this walkthrough, you should be able to:  
- Install Go on your computer  
- Create a Go program  
- Use a `go.mod` file to manage dependencies  
- Print "Hello, World!" to the terminal  
- Run your program  

## Preparing your workspace
Navigate to the [Go instillation site](https://go.dev/dl/) and download the correct file based on your device specifications. 

!!! note
    Ensure you have the latest version of Go installed by running `$ go version`.

Create a directory to host your program. Navigate to your desired location and run:  
`$ mkdir hello`  
`$ cd hello`  

## Manage dependcies
Create a directory to maintain your Dev Controller:
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
Next, create a mod file to track and manage dependcies:
`$ go mod init example/hello`  
Open VSCode and navigate to the *hello* directory. Under **Extensions**, locate and install the official Go VSCode Plugin.

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

## Understanding the `build` subcommand
The `go build` command creates a binary executable that you can run directly. This is similar to using `gcc` in COMP211 to compile a C program into an executable.

**Example (C Program in COMP211):**
```bash
gcc -o hello hello.c
./hello

* Primary author: [Sean Blizard](https://github.com/sblizard)
* Reviewer: [Grace Odondi](https://github.com/godondi)