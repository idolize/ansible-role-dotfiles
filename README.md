# Ansible Role: Dotfiles Stow

Installs a set of dotfiles from a given Git repostiory.

Works for all dotfile repos that follow the [stow][stow] format ([blog post](https://brandon.invergo.net/news/2012-05-26-using-gnu-stow-to-manage-your-dotfiles.html)).

## Usage

1. Create a playbook with this Role
2. Set the `dotfiles_repo` variable somewhere
3. Run the playbook

## Dependencies

None

## Example playbook

```
---
- hosts: localhost
  roles:
    - role: idolize.dotfiles
      vars:
        dotfiles_repo: https://github.com/myusername/mydotfiles
```


## Tests

Fully tested on:

* Fedora 36
* Ubuntu 20.04
* macOS 13.4.1

## Credits

Forked from: https://github.com/mariuskimmina/ansible-role-dotfiles

Inspired by: https://github.com/geerlingguy/ansible-role-dotfiles. The main difference between the original project and this one is the usage of [stow][stow].

[stow]: https://www.gnu.org/software/stow/
