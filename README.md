# Ansible Role: idolize.dotfiles_stow

Installs a set of dotfiles from a given Git repostiory.

Works for all dotfile repos that follow the [stow][stow] format ([blog post](https://brandon.invergo.net/news/2012-05-26-using-gnu-stow-to-manage-your-dotfiles.html)).

## Example playbook

```
---
- hosts: localhost
  roles:
    - role: idolize.dotfiles_stow
      vars:
        dotfiles_repo: https://github.com/myusername/mydotfiles
        dotfiles_conflict_mode: adopt_and_reset
```

## Configuration

### Dotfiles Repository

Before using the role, you must define the `dotfiles_repo` variable somewhere. This is the git repo where your dotfiles are stored (e.g. "`https://github.com/myusername/mydotfiles`").

You may also specify `dotfiles_repo_version` (default = "main"), which specifies the [`version`](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/git_module.html#parameter-version) of the repo to checkout (e.g. branch, tag, or commit).

### Directories

The dotfiles repository clone location and dotfiles symlink destination can be configured using the following variables:

`dotfiles_repo_local_destination` (default = "~/dotfiles") - Where to clone the `dotfiles_repo` git repository (the [source stow directory](https://www.gnu.org/software/stow/manual/stow.html#Terminology)).

`dotfiles_home` (default = "~") - Where to symlink the final dotfiles (stow's [target directory](https://www.gnu.org/software/stow/manual/stow.html#Terminology)).

### Conflicts

If there are already existing configuration files in the `dotfiles_home` target directory then, by default, the task will throw an error. This matches [the default behavior of stow](https://www.gnu.org/software/stow/manual/stow.html#Conflicts).

If, instead, you want to change the behavior of how conflicts are handled you can set the `dotfiles_conflict_mode` variable to one of the following options:

`abort` (default) - Throws an error and exits on conflict.

`adopt` - Follows the ["adopt" behavior from stow](https://www.gnu.org/software/stow/manual/stow.html#Invoking-Stow), where the existing config files overwrite the ones in the dotfiles repo.

`adopt_and_reset` - This is [semi-equivalent to overwriting the existing config files](https://unix.stackexchange.com/q/680413/414698) with the ones from the `dotfiles_repo`, but there are a few caveats to be aware of. Instead of directly overwriting the files, it instead runs using `--adopt`, and then resets the `dotfiles_repo` repo back to the previous state using git.

## Dependencies

None

## Tests

Fully tested on:

* Fedora 36
* Ubuntu 20.04
* macOS 13.4.1

## Credits

Forked from: https://github.com/mariuskimmina/ansible-role-dotfiles

Inspired by: https://github.com/geerlingguy/ansible-role-dotfiles. The main difference between the original project and this one is the usage of [stow][stow].

[stow]: https://www.gnu.org/software/stow/
