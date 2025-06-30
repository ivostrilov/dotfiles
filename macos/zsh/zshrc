#! /bin/zsh

configure_alias() {
  alias ll="ls -l"
}

configure_path() {
  my_paths=(
    "$HOME/.local/bin"
  )

  local my_path=""
  for my_path in "${my_paths[@]}"; do
    if [[ ":$PATH:" != *":$my_path:"* ]]; then
      export PATH="$my_path:$PATH"
    fi
  done
}

configure_git_completion() {
  # $1 - dir with completion scripts
  #
  # Required files from
  # https://github.com/git/git
  # - contrib/copletion/git-prompt.sh
  # - contrib/copletion/git-completion.bash
  # - contrib/copletion/git-completion.zsh named by '_git'

  local completion_dir="$1"

  # Highlight the current branch below

  local git_promt_sh="${completion_dir}/git-prompt.sh"
  setopt prompt_subst
  . "$git_promt_sh"
  export RPROMPT=$'$(__git_ps1 "%s")'

  # Git commands completion below

  # Add path to zsh for scaning completion funcs
  fpath=("${completion_dir}" $fpath)

  # Initialize completion system
  autoload -Uz compinit && compinit
}

main() {
  configure_alias
  configure_path
  configure_git_completion "$HOME/.local/completion"
}

main "$@"
