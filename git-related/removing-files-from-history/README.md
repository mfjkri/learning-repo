# Installing git-extras:

- Arch-based distro:

  You can install `git-extras` as an `AUR` package through your package manager.

- Debian-based distro:

  Install `git-extras` using the `apt` package manager.

  ```bash:
  $ sudo apt update
  $ sudo apt install git-extras
  ```

- Windows:

  Clone the git repo:

  ```
  $ git clone https://github.com/tj/git-extras
  ```

  Install script:

  ```
  $ cd git-extras
  $ install.cmd "C:\git"
  ```

  Note: You can also choose to follow the installation steps of the project [here](https://github.com/tj/git-extras/blob/master/Installation.md)

&nbsp;

# Using git-extras (obliterate):

```bash
# Removing a file from commits history
$ git obliterate path/to/$FILE.EXTENSION

# Removing a directory from commits history
$ git obliterate path/to/directory/
```
