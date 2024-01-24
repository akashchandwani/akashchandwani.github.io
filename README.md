# akashchandwani.com

A personal blogging website created to share my thoughts and experiences on software technologies and open source tools.

## Technologies used

1. Static website builder: [Hugo](https://gohugo.io/)
2. Theme: [PaperMod](https://themes.gohugo.io/themes/hugo-papermod/)

## First time setup

1. Clone the repository
2. Run `pre-commit install -f` to install the `pre-commit` hooks in the repository
3. Install hugo using the command: `brew install hugo`
4. Install the theme submodule using the command: `git submodule update --init --recursive --remote`
5. Install `pre-commit` extension in your text editor to maintain consistency in formatting. To install, run: `brew install pre-commit` and then `pre-commit-install` to update the pre-commit hook in your local repository

## Frequently used commands

1. Run `pre-commit autoupdate` to fetch and install the latest version of the `pre-commit` hooks
2. To generate a blog page, run `hugo new content blog/<page-name>.md`
3. To run the server with draft views enabled, run `hugo server -D`
4. To run the server `hugo server`
