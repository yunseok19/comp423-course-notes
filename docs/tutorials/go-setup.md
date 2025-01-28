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
(1) Log in to your GitHub account and navigate to the [**Create a New Repository**](https://github.com/new) page.

(2) Fill in the details as follows:

- **Repository Name**: `comp423-go-notes`

- **Description**: "Course notes organized as a static website using Material for MkDocs."

- **Visibility**: Public

(3) Do **not** initialize the repository with a README, .gitignore, or license.

(4) Click **Create Repository**.
### Step 3. Link your Local Repository to GitHub
(1) Add the GitHub repository as a remote:

   ```
   git remote add origin https://github.com/<your-username>/comp423-course-notes.git
   ```
(2) Check your default branch name with the subcommand `git branch`. If it's not `main`, rename it to `main` with the following command: `git branch -M main`. Old versions of `git` choose the name `master` for the primary branch, but these days `main` is the standard primary branch name.

(3) Push your local commits to the GitHub repository:
```
git push --set-upstream origin main
```
## **Part 2. Setting Up the Development Environment**
### Step 1. Add Development Container Configuration
(1) In VS Code, open the `comp423-course-notes directory`. You can do this via: File > Open Folder.

(2) Install the **Dev Containers** extension for VS Code.

(3) Create a `.devcontainer` directory in the root of your project with the following file inside of this "hidden" configuration directory:
```
.devcontainer/devcontainer.json
```
The `devcontainer.json` file defines the configuration for your development environment. Here, we're specifying the following:

- **name**: Descriptive name for the dev container.

- **image**:  Docker image for Go development. [Microsoft maintains a collection of base images for many programming language environments](https://hub.docker.com/r/microsoft/vscode-devcontainers), but you can also create your own!

- **customizations**: Automatically installs the Go extension in VS Code.
```
{
  "name": "COMP423 Go Notes",
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
(1) In VS Code, press `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac)

(2) Search for **"Dev Containers: Reopen in Container"** and select it

(3) Wait for the container to initialize

Once the setup completes, open a new terminal in VS Code and verify the Go installation:
```
go version 
```