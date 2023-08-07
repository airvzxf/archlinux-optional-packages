# ArchLinux: Optional packages

It is a command-line tool to get the optional dependencies from some specific package using pacman. Furthermore,
you can install it in your Arch Linux.

## INFORMATION

### USAGE:

`optional-packages [OPTIONS] <PACKAGE-1> <PACKAGE-2> <…>`

### DESCRIPTION

Command-line tool that finds all the optional packages of the packages that were pointed by you. It has different
options to filter these packets. Beyond that, you can install the packages you pointed to the dependencies and the
optional packages you found and filtered.

### ARGS:

- The name of the packages separate by spaces.
    - `<PACKAGE-1> <PACKAGE-2> <…>`.

### OPTIONS:

| **Abbr** | **Long**         | **Information**                                                                                                                                                       |
|----------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -e       | --exclude        | Excludes packages mentioned during a deep search.<br> - Required: no<br> - Type: string<br> - Values: package-1 package-2 …<br> - Default: none                       |
| -h       | --help           | Display information for this command and exit.<br> - Required: no<br> - Type: none<br> - Values: none<br> - Default: none                                             |
| -i       | --install        | Install all the packages found.<br> - Required: no<br> - Type: boolean<br> - Values: yes or no<br> - Default: no                                                      |
| -p       | --packages       | The core packages from which to start the search for optional packages.<br> - Required: no<br> - Type: string<br> - Values: package-1 package-2 …<br> - Default: none |
| -s       | --skip-installed | Skip the installed packages.<br> - Required: no<br> - Type: boolean<br> - Values: yes or no<br> - Default: no                                                         |
| -v       | --version        | Display the version of this tool along with the project information and exit.<br> - Required: no<br> - Type: none<br> - Values: none<br> - Default: none              |
|          | --version-simple | Display the version of this tool and exit.<br> - Required: no<br> - Type: none<br> - Values: none<br> - Default: none                                                 |

**Note:** Multiple values are separated by spaces.

### EXAMPLES:

- Search for three packages.
    - Commands:
        - `optional-packages bash lsd rust`
        - `optional-packages -p bash lsd rust`
        - `optional-packages --packages bash lsd rust`

- Search for a package, but exclude some optional packages.
    - Commands:
        - `optional-packages -p kitty -e imagemagick python-pygments`
        - `optional-packages -packages kitty -exclude imagemagick python-pygments`

- Install the core packages and any additional packages found.
    - Commands:
        - `optional-packages -p lsd -i yes`
        - `optional-packages -packages lsd --install yes`

- Search for optional packages, just for any core packages or optional packages that are not installed.
    - In this case, `lsd` is already installed, it will not look for any optional dependencies because it is already
      installed.
    - Otherwise, if the value of this option is `no` (the default value), then it would look for dependencies on
      the `lsd` package or any package.
    - Commands:
        - `optional-packages -p lsd -s yes`
        - `optional-packages -packages lsd --skip-installed yes`

- All words at the end of the command are considered core packages. In this example are `bash lsd rust`.
    - Commands:
        - `optional-packages bash lsd rust`
        - `optional-packages --install yes bash lsd rust`
        - `optional-packages --exclude bat --install yes bash lsd rust`
    - Warning: if your last option is `exclude`, all words at the end count as exclusion and not for parent packages. In
      this case, nothing will be installed because no parent package was pointed to.
        - `optional-packages --install yes --exclude bat bash lsd rust`

- Multiple options can be used multiple times, plus core packages can be at the end.
    - In this example, it will search for optional packages within the following core
      packages `lsd kitty virtualbox bat xterm`; exclude `python gtk3 perl` optional packages; **avoid installed
      packages**; and finally, **install the packages** found.
    - Note: For options that have a single value (boolean), when the same option is entered multiple times, it will take
      the last option and its value. The order matters.
    - Commands:
        - `optional-packages -s no -p lsd kitty -s yes -e python gtk3 -p virtualbox -e perl -i no -i yes bat xterm`

## CONTRIBUTE

You can always follow the official GitHub guides: [contributing to projects][contributing to projects]
and [fork a repository][fork a repository].

In short, you can perform the following steps. Let's assume your GitHub user is `XxXxXx`.

Here is a small script that can be run after the first step, which is to fork the project in your account.

```bash
#!/usr/bin/env bash

# Replace these two values to customize your execution.
MY_GITHUB_USER="XxXxXx"
BRANCH_NAME="add-new-options"

git clone "https://github.com/${MY_GITHUB_USER}/archlinux-optional-packages.git"
cd archlinux-optional-packages
git remote add upstream "https://github.com/airvzxf/archlinux-optional-packages.git"
git remote --verbose
git branch "${BRANCH_NAME}"
git checkout "${BRANCH_NAME}"
```

- Navigate to [archlinux-optional-packages][optional packages GitHub project] and create a branch by clicking the branch
  button. Or just click this [link to create it automatically][fork optional packages project].
- On your computer, clone your forked project: `git clone https://github.com/XxXxXx/archlinux-optional-packages.git`.
- Go inside the repository folder: `cd archlinux-optional-packages`.
- Configure Git to sync your fork with the upstream repository.
    - `git remote add upstream https://github.com/airvzxf/archlinux-optional-packages.git`.
    - `git remote --verbose`.
- Always create a new branch to work on your changes.
    - `git branch BRANCH_NAME`.
    - `git checkout BRANCH_NAME`.
- Make your changes and commit them.
    - `git add .`.
    - `git commit --message "Brief description of the changes"`.
- Push your changes to our repository on the GitHub server. The first time you need to specify the upstream, the next
  time use basic push.
    - First time: `git push --set-upstream origin BRANCH_NAME`.
    - `git push`.
- The last step is to create a pull request to push your changes to our repository. This request must
  be accepted by the project owner or maintainers for the changes to take effect.
    - If you go to your repository with the web browser (`https://github.com/XxXxXx/archlinux-optional-packages`), it
      will display the 'Compare & pull request' button. Or use this URL to do it
      easily: `https://github.com/XxXxXx/archlinux-optional-packages/compare/BRANCH_NAME`
    - Fill in all the required information and review the 'Files changed' tab to verify the changes.
    - Tap the 'Create pull request' button to finish.

## RELEASE TO THE AUR SERVER

Use the version format vX.X.X, where X equals to numbers, for example: v45.7.211.

### Change in the source code.

- Manually change the version in [./src/optional-packages][package file in GitHub]. Find the variable `VERSION="vX.X.X"`
  in the first few lines and change it to the new version.

### Create a [new release][new release url].

- You can choose between a branch or a specific commitment.
    - If your commit is the latest at this time, you can select the 'main' branch.
    - Otherwise, if your commit is old, it's better to choose a specific commit.
- Create a new tag that is larger than the previous one (vX.X.X).
- Add a release title. Preferred to use 'Release vX.X.X'.
- Add a description. It is recommended to add a brief description and use the 'Generate release notes' button.
- Select the option: 'Set as the latest release'.
- Finally, tap the 'Publish release' button.

### Review in the '[CI ➟ Deploy to AUR][CI deploy to AUR]' actions.

- A new workflow run should be started with the title of the version you added in the previous steps.
- It validates that it has finished successfully (green color). If not, review the bug, fix it, and rebuild this
  version.
- If it finished successfully, in the logs at the end, it provides an AUR URL for this specific commit on its servers.
- You can check the [AUR repository information][AUR repository].
- You can check the [package in the AUR website][AUR webpage package].

## TO-DO LIST

### RELEASE

- [ ] Version of this tool. It is not defined, and we have to find the best approach. But definitely, the expectation is
  to look for the simplest and most automated way.
    - Option #1: When you create the release on GitHub, automatically modify the source code by changing the version in
      the script file. Furthermore, make a new commit with these changes, along with a push, and modify in the release
      the commit that is pointed to this last commit.
    - Option #2: It is precisely the opposite of Option #1. The version is assigned in the script or a file. Then find a
      way to automate the release and have it grab the version of the script or file on GitHub. Or even that the release
      is already automated with line commands and not through the website on GitHub, creating an action in the workflow.

Review the complete [To-Do list][ToDo] to review what is pending.

[new release url]: https://github.com/airvzxf/archlinux-optional-packages/releases/new

[package file in GitHub]: ./src/optional-packages

[CI deploy to AUR]: https://github.com/airvzxf/archlinux-optional-packages/actions/workflows/deploy-to-aur.yml

[AUR repository]: https://aur.archlinux.org/cgit/aur.git/?h=optional-packages

[AUR webpage package]: https://aur.archlinux.org/packages/optional-packages

[contributing to projects]: https://docs.github.com/en/get-started/quickstart/contributing-to-projects

[fork a repository]: https://docs.github.com/en/get-started/quickstart/contributing-to-projects#creating-a-branch-to-work-on

[optional packages GitHub project]: https://github.com/airvzxf/archlinux-optional-packages

[fork optional packages project]: https://github.com/airvzxf/archlinux-optional-packages/fork

[ToDo]: ./TODO.md
