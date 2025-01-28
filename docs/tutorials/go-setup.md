# Setting up a dev container for Go

* Primary author: [Yunseok Hwang](https://github.com/yunseok19)
* Reviewer: [Bamlak Tesfaye](https://github.com/bamlak363)

## **Prerequisites**
Before you begin, ensure you have the following:

- **GitHub account**: Sign up at [Github](https://github.com/) if you haven't done so already.
- **Git installed**: Install Git [here](https://git-scm.com/) if you haven't done so already.
- **VS Code**: Download and install Visual Studio Code from [here](https://code.visualstudio.com/).
- **Docker installed**: Required to run the dev container. Download it [here](https://www.docker.com/).
- **Command-line basics**: Your COMP211 command-line knowledge will serve you well here. If in doubt, review the Learn a CLI text!
## **Part 1. Project Setup: Creating the Repository**
### Step 1. Create a Local Directory and Initialize Git
(A) Open your terminal or command prompt.

(B) Create a new directory for your project. (Note: Of course, if you'd like to organize this tutorial somewhere else on your machine, go ahead and change into that parent directory first. By default this will be in your user's home directory.):
```
mkdir go-dev-container
cd go-dev-container
```
(C) Initialize a new Git repository:
```
git init
```
(D) Create a README file:
```
echo "# COMP423 Go Notes" > README.md
git add README.md
git commit -m "Initial commit with README"
```
###Step 2. Create a Remote Repository on GitHub
(A) Log in to your GitHub account and navigate to the [**Create a New Repository**](https://github.com/new) page.

(B) Fill in the details as follows:

- **Repository Name**: `comp423-go-notes`

- **Description**: "Tutorial for Go"

- **Visibility**: Public

(C) Do **not** initialize the repository with a README, .gitignore, or license.

(D) Click **Create Repository**.
### Step 3. Link your Local Repository to GitHub
(A) Add the GitHub repository as a remote:
```
git remote add origin https://github.com/<your-username>/comp423-go-notes.git
```
(B) Check your default branch name with the subcommand `git branch`. If it's not `main`, rename it to `main` with the following command: `git branch -M main`. Old versions of `git` choose the name `master` for the primary branch, but these days `main` is the standard primary branch name.

(C) Push your local commits to the GitHub repository:
```
git push --set-upstream origin main
```
## **Part 2. Setting Up the Development Environment**
### Step 1. Add Development Container Configuration
(A) In VS Code, open the `comp423-go-notes directory`. You can do this via: File > Open Folder.

(B) Install the **Dev Containers** extension for VS Code.

(C) Create a `.devcontainer` directory in the root of your project with the following file inside of this "hidden" configuration directory:
```
.devcontainer/devcontainer.json
```
The `devcontainer.json` file defines the configuration for your development environment. Here, we're specifying the following:

- **name**: Descriptive name for the dev container.

- **image**:  Docker image for Go development. [Microsoft maintains a collection of base images for many programming language environments](https://hub.docker.com/r/microsoft/vscode-devcontainers), but you can also create your own!

- **customizations**: Automatically installs the Go extension in VS Code.
```
{
  "name": "Gp Tutorial",
  "image": "mcr.microsoft.com/devcontainers/go:latest",
  "customizations": {
    "vscode": {
      "settings": {},
      "extensions": ["golang.go"]
    }
  }
}
```
## **Step 3. Reopen the Project in a Dev Container**
(A) In VS Code, press `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac)

(B) Search for **"Dev Containers: Reopen in Container"** and select it

(C) Wait for the container to initialize

Once the setup completes, open a new terminal in VS Code and verify the Go installation:
```
go version 
```
## **Step 4. Create a "Hello COMP423" Program**
(A) Create a hello directory for the first Go source code
For example, use the following commands:
```
mkdir hello
cd hello
```
(B) Enable dependency tracking for your code

When your code imports packages contained in other modules, you manage those dependencies through your code's own module. That module is defined by a go.mod file that tracks the modules that provide those packages. That go.mod file stays with your code, including in your source code repository.

To enable dependency tracking for your code by creating a go.mod file, run the [go mod init command](https://go.dev/ref/mod#go-mod-init), giving it the name of the module your code will be in. The name is the module's module path.

In actual development, the module path will typically be the repository location where your source code will be kept. For example, the module path might be github.com/mymodule. If you plan to publish your module for others to use, the module path must be a location from which Go tools can download your module. For more about naming a module with a module path, see [Managing dependencies](https://go.dev/doc/modules/managing-dependencies#naming_module).

For the purpose of this tutorial, just use `example/hello`
```
$ go mod init example/hello
```
(C) In your text editor, create a file hello.go in which to write your code.

(D) Paste the following code into your hello.go file and save the file.
```
package main

import "fmt"

func main() {
    fmt.Println("Hello, COMP423!")
}
```
This is your Go code. In this code, you:

- Declare a main package (a package is a way to group functions, and it's made up of all the files in the same directory).
- Import the popular [fmt package](https://pkg.go.dev/fmt), which contains functions for formatting text, including printing to the console. This package is one of the [standard library](https://pkg.go.dev/std) packages you got when you installed Go.
- Implement a main function to print a message to the console. A main function executes by default when you run the main package.

(E) Run your code to see the greeting
```
$ go run .
Hello, COMP423!
```
The [go run command](https://go.dev/cmd/go/#hdr-Compile_and_run_Go_program) is one of many go commands you'll use to get things done with Go. Use the following command to get a list of the others:
```
$ go help
```
### Go build
The go build command compiles the packages, along with their dependencies, but it doesn't install the results.

From the command line in the hello directory, run the go build command to compile the code into an executable.

`$ go build`

From the command line in the hello directory, run the new hello executable to confirm that the code works.
```
$ ./hello
map[Darrin:Great to see you, Darrin! Gladys:Hail, Gladys! Well met! Samantha:Hail, Samantha! Well met!]
```

The `go build` command compiles Go code into an executable binary, similar to how `gcc` compiles C programs into runnable files. It creates a binary you can run direclty with `./binary-name`, making it reusable and easy to share. In comparison, `go run` compiles the code and runs it right away.

## **Congrats**
You have succesfully finished your first Go program!