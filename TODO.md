# ToDo's list

## Pending

### Features

#### Command line

- [ ] Search optional deeply.
  - Set the limit of the deep levels of the optionals, if this options is '1' should be installed only the optional
    for this package. If it sets deep to `2`, it installs the optional packages for the main package and
    the children packages for the children.
  - For infinite deep levels set to `-1`.
  - Default: `-1`.
  - Example: `optional-packages --depth 2`.
- [ ] Install command.
  - Take the argument and execute it as a command, could be `pacman`, `powerpill` or other.
  - Default: `pacman`.
  - Example: `optional-packages --install-command powerpill`.
- [ ] Verbose.
  - The detail of the output.
  - Values: `silent`, `info`, `all`
  - Default: `info`
  - Example: `optional-packages --verbose all`.

#### Functionality

- [ ] Also take required dependencies, to search within them for optional packages.
  - Example: `pacman -Si skim`.
    - `Depends On      : ncurses`.

### Bugs

- [ ] Arch Linux has some Meta-packages which could install, but they don't appear in the search.
  - Example:
    - `sudo pacman -Si java-runtime` ➟ `error: package 'java-runtime' was not found`.
    - `sudo pacman -S java-runtime` ➟ `jre-openjdk-20.0.1.u9-3 is up to date -- reinstalling`.

---

## Completed

### Features

#### Command line

- [x] Add options.
  - Example: `optional-packages --depth 1 --packages vim tmux kitty`.
  - Example: `optional-packages -d 1 --p vim tmux kitty`.
- [x] Added simultaneous packages.
  - Example: `optional-packages vim tmux kitty`
- [x] Exclude packages.
  - Check the optional packages in every iteration and exclude the marked packages.
  - Example: `optional-packages --exclude kde plasma`.
- [x] Exclude installed packages.
  - If the package is installed during the research, it avoids from the list of packages.
  - Default: `yes`.
  - Example: `optional-packages --exclude-installed no`.
- [x] Install packages.
  - Execute the pacman command to install all the packages found.
  - Default: `no`.
  - Example: `optional-packages --install yes`.

### Bugs

- [x] .
