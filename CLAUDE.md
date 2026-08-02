# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Personal dotfiles repo (Ruby/Rake-based installer, holman-style). Files are symlinked from
this repo into `$HOME` so editing a file here immediately affects the live config once
installed (they are the same inode via symlink, not a copy).

## Commands

- `rake install` (or plain `rake`, since `install` is the default task) — symlinks every
  `*.symlink` file into `$HOME` as `~/.<basename>` (e.g. `zsh/zshrc.symlink` -> `~/.zshrc`).
  Prompts per-file for skip/overwrite/backup if the target already exists (also supports
  "all" answers: `S`/`O`/`B`).
- `rake uninstall` — removes symlinks created by install and restores any `.backup` files
  it made.

There is no build, lint, or test suite in this repo — it's shell/Ruby config files.

## Structure and conventions

- **Only files ending in `.symlink` get installed.** The Rakefile globs `**/*.symlink`
  and derives the target dotfile name by stripping `.symlink` (e.g.
  `git/gitconfig.symlink` -> `~/.gitconfig`). Non-`.symlink` files (like `shell/common`,
  `zsh/includes/config`) are not linked directly into `$HOME`; instead they are `source`d
  from an installed symlink file. Concretely: `zsh/zshrc.symlink` sources
  `~/.dotfiles/shell/common` and `~/.dotfiles/zsh/includes/config` by absolute path assuming
  the repo lives at `~/.dotfiles`.
- Directories are organized by tool: `zsh/`, `shell/`, `git/`, `gem/`, `ruby/`.
  Adding config for a new tool means creating a new top-level directory with a
  `<name>.symlink` file inside it (the directory name doesn't need to match the tool name).
- `shell/scripts/` holds standalone executable scripts (not symlinked as dotfiles) that get
  added to `PATH` via `shell/common`. `shell/secret_scripts` is referenced in `PATH` too but
  is gitignored — it's a local-only, untracked directory for private scripts.
- Shell aliases/env live in two places with different scope: `shell/common` is
  shell-agnostic (PATH, `$EDITOR`, aliases for git, `zoxide`, `mise` init) and is
  sourced by both zsh (and presumably bash) setups; `zsh/includes/config` is zsh-only
  (reload alias, `unsetopt correct`).
- Prompt is provided by starship.rs (`eval "$(starship init zsh)"` in `zsh/zshrc.symlink`),
  not oh-my-zsh/prezto — a prior version of this repo used zprezto and was migrated away
  from it (see git log).
- `git/gitconfig.symlink` hardcodes the user's name/email (Winston /
  winston.yongwei@gmail.com) — update in place if forking/reusing this repo.
