# akashchandwani.com

A personal blogging website created to share my thoughts and experiences on software technologies and open source tools.

## Technologies Used

1. Static website builder: [Hugo](https://gohugo.io/)
2. Theme: [PaperMod](https://themes.gohugo.io/themes/hugo-papermod/)
3. Comments: [Disqus](https://disqus.com/)
4. Diagrams: [Mermaid](https://gohugo.io/content-management/diagrams/#mermaid-diagrams)
5. Dev Containers: [Dev Containers](https://containers.dev)

## Setting up the application:

There are two ways to spin up this application

1. The hard way: Install everything in local and hope everything works in CI/CD as well :)
2. The easy way: Using dev containers. Just spin up the application in a docker container.

### Setting up the application: The Hard Way

Make sure you have the following tools installed as pre-requisite. The steps are for mac, but you can use alternatives for your OS.

#### Pre-requisites

1. Install Hugo: `brew install hugo`
2. install pre-commit tool: `pip install pre-commit`

#### Steps

1. Clone the repository
2. Install pre-commit in your system by running: `pip install pre-commit`
3. Run `pre-commit install -f` to install the `pre-commit` hooks in the repository
4. Install hugo using the command: `brew install hugo`
5. Install the theme submodule using the command: `git submodule update --init --recursive --remote`
6. Install `pre-commit` extension in your text editor to maintain consistency in formatting. To install, run: `brew install pre-commit` and then `pre-commit-install` to update the pre-commit hook in your local repository

### Setting up the application: The Easy Way

You can use the devcontainers to run a pre-configured developement environment in your machine. This repository already has a prec-configured template in `devcontainer/devcontainer.json`. All you have to do is to run this application on `github codespaces`, `vs code dev containers` or any devcontainer of your choice.

## Create a new content page

To create a new content page run the command
```sh
hugo new content content/blog/<your-page-name>.md
```

## Publish content

To publish the content you will have to

1. Set the `draft` key to false in the content page
2. Push the changes using `git push` command

## Frequently used commands

1. Run `pre-commit autoupdate` to fetch and install the latest version of the `pre-commit` hooks
2. To generate a blog page, run `hugo new content blog/<page-name>.md`
3. To run the server with draft views enabled, run `hugo server -D`
4. To run the server `hugo server`

