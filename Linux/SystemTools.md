---

---

Development enviroment setup
============================

- Vim 
1. Config by edit the file ~/.vimrc
2. Install Plugins and theme. Use package manager Vundle

- oh-my-zsh
1. Config by edit the file ~/.zshrc
2. Select theme and copy variables from ~/.bash_profile

- Tmux
1. Config by edit the file ~/.tmux.conf

2. Use plugin manager to install plugin
  * tmux-resurrect
  * tmux-mem-cpu-load

3. Some frequently use command
  * Ctl-b, Ctl-I to install plugin
  * Ctl-b, R to reload config settings
  * Ctl-b, Ctl-s to save current session layout
  * Ctl-b, Ctl-r to restore layout
  * Ctl-b, :resize-p -U 10 to change panel size
  * Ctl-b, z to zoom panel
  * Ctl-b, o to switch panel
  * Ctl-b, x to close panel
  * Ctl-b, d to detach session
  * tmux new -s session_name to create new session
  * tmux kill-session -t session_name to kill session
  * tmux ls to list all session
