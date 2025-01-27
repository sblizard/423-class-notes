# Setting Up a Dev Container For Rust

* Primary author: [Grace Odondi](https://github.com/godondi)

* Reviewer: [Sean Blizard](https://github.com/sblizard)

## Prerequisites
Before you begin, make sure you have:

* **A GitHib account:** Create one [here](https://github.com/signup), if you haven't

* **Installed Git**: Install it [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git), if you haven't

* **Downloaded Visual Studio Code (VS Code)**: Download it [here](https://code.visualstudio.com/download), if you haven't

* **Downloaded Docker**: Download it [here](https://www.docker.com/products/docker-desktop/), if you haven't

* **Knowledge on Command-line basics** to back up your work on GitHub.

## Part 1: Creating the Repository

### Step 1. Create a Local Directory and Initialize Git

(A) Open your terminal or command prompt.

(B) Create a new directory for your project (If you want to store the directory in a different location on your computer go ahead and open that directory first. Otherwise, it will be in your home directory.)
```
mkdir comp423-EX00
cd comp423-EX00
```

(C) Initialize a new Git repository:
```
git init
```

(D) Create a README file:
```
echo "# Hello COMP423" > README.md
git add README.md
git commit -m "Initial commit with README"
```

!!! info "How to edit your website title"
    The text in the quotation marks following "echo" will be the title of your webpage. If you want to change it, simply change those words.

### Step 2. Create a Remote Repository on GitHub
(1) Log in to your GitHub account and navigate to the [Create a New Repository](https://github.com/new) page.

(2) Fill in the details as follows:

* **Repository Name**: `comp423-ex00`
* **Description**: "Website using Rust for COMP 423"
* **Visibility**: Public

(3) Do not initialize the repository with a README, .gitignore, or license.

(4) Click Create Repository.

### Step 3. Link your Local Repository to GitHub
(1) Add the GitHub repository as a remote repository by putting the following in the command in your terminal:

```
git remote add origin https://github.com/<your-username>/comp423-ex00.git
```
Put your GitHub username in place of `<your-username>`.

(2) Make sure your default branch is main by using the subcommand `git branch`. If it's not main, rename it to main with the following command: `git branch -M main`.

??? note "Git History"
    Old versions of git choose the name master for the primary branch, but these days main is the standard primary branch name.

(3) Push your local commits to the GitHub repository:

```
git push --set-upstream origin main
```
??? Note "What does the --set-upstream flag do?"
    `git push --set-upstream origin main` pushes the main branch to the remote repository origin and then sets up the main branch to track the remote branch. This is important so that future pushes and pulls can be done without specifying the branch name, you can just write `git push origin` when working on your local main branch. You can shorten this flag to `-u`.
(4) To see your commit in your remote, refresh your GitHub repository in your web browser. To see more information about your commit, including the commit ID, put `git log` in your terminal.

## Part 2: Setting Up Your Development Environement
### What is a Development (Dev) Container and why use it?
A Dev Container creates a coding environment with all the programming languages, dependencies, libraries, softwares, and tools you need for your project without downloading them each individually on your computer. Dev containers simplify onboarding and make set up consistent so that teammates don't run into nearly as many version errors or bugs in the code.

Starting the dev container runs the `requirements.txt` file with all the necessary depenencies, effectively allowing you to skip other installation steps.

### Step 1. Add Development Container Configuration
In VS Code, open the `comp423-EX00 directory` you made in part 1. You can do this by clicking file `File` the selecting `Open Folder`.
Install the Dev Containers extension for VS Code.
Create a `.devcontainer` directory in the root of your project with the following file inside of this "hidden" configuration directory: <br>
`.devcontainer/devcontainer.json`

!!! "Note on `.devcontainer/devcontainer.json`"
    This file defines the configuration for your development environment.


**name**: Names your container. <br>
**image**: Specifies the Docker image to use, in this case, the latest version of a Rust environment. Microsoft's collection of base images is very helpful and it works for many programming language environments, but you can also create your own! <br>
**customizations**: Adds useful configurations to VS Code, like installing the Rust extension. When you search for VSCode extensions on the marketplace, you will find the string identifier of each extension in its sidebar. Adding extensions here ensures other developers on your project have them installed in their dev containers automatically. <br>
**postCreateCommand**: A command to run after the container is created. In our case, it will use pip to install the dependencies listed in requirements.txt.

```
{
  "name": "COMP423 Course Notes",
  "image": "mcr.microsoft.com/vscode/devcontainers/rust",
  "customizations": {
    "vscode": {
      "settings": {},
      "extensions": ["rust-lang.rust-analyzer"]
    }
  },
  "postCreateCommand": "pip install -r requirements.txt"
}
```

### Step 2. Add requirements.txt Rust Dependency Configuration
`requirements.txt`

The requirements.txt file lists the Rust dependencies needed for the project. It should be in your project's root directory. You only need to include mkdocs-material pinned to a specific minor version its current release:
`mkdocs-material~=9.5`
This is signified by a tilde. Not specifying a specific version will allow the dependency to update automatically with the latest bug fixes for any version that starts with 9.5. So, you wouldn't have to manually update from 9.5.1 to 9.5.2. This is great for efficiency!

### Step 3. Reopen the Project in a VS Code Dev Container
Reopen the project in the container by pressing `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac), then typing "Dev Containers: Reopen in Container," and selecting the option. Don't be alarmed if it takes a few minutes, your computer is installing things!

To check the version of Rust being used, type `rustc --version` into your terminal.

## Part 3: Launch Your Site Locally

### Step 1. Create File

Run the following commands in your terminal (inside the container) to create the necessary files and enter the directory (this creates a binary project):

```
cargo new comp423-hello --vcs none
cd comp423-EX00
```
!!! info "What does `--vcs none' do?"
    This subcommand ensures that a new repository is not created.

### Step 2. Edit File

Edit your `main.rs` file to look like this:

```
fn main() {
    println!("Hello COMP423");
}
```
Next, edit the `index.md` markdown file in the `docs` directory to look like this:

`docs/index.md`

```
# Hello COMP 423
```

As you have seen, Markdown is a simple language that is very useful for making websites. Files using Markdown usually have the .md extension. Markdown is converted and run as HTML so you don't have to deal with that. People often prefer Markdown because it is easy, readable, and compatible with version control systems, like Git, and other platforms.

### Step 3. Preview Your Site Locally
Run the following command to start a local development server:
```
cargo build
```

This is the same thing as using the gcc command in C and creating an executable object file. To run the executable object file, run the following command:
```
./target/debug/comp423-EX00
```
To combine those steps (compile and executes), run the following command:
```
cargo run
```

#### What is the difference between `cargo build` and `cargo run`? <br>
`cargo build` is mostly used to access the executable object file whereas `cargo run` repeatedly compiles the project. `cargo run` is quicker as well.

To stop the server, return to your terminal and press `Ctrl+C`. This will terminate the build process.

You have successfully completed your website in Rust!!  :party_popper:

**Many thanks to Kris Jordan's Mkdocs Tutorial for inspiration. See his website [here](https://comp423-25s.github.io/resources/MkDocs/tutorial/).**