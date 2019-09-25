# Instalar e configurar Tmux no Ubuntu


### Instalar Tmux no Ubuntu
```shell script
$ sudo apt install tmux
```

### Customizar configurações do Tmux

O arquivo padrão de configuração do tmux para um usuário fica em `~/.tmux.conf`
Caso não exista, é necessário cria-lo.

Crie o arquivo, caso necessário
```
$ touch ~/.tmux.conf
```

Copie as configurações abaixo e cole no arquivo `~/.tmux.conf`
```shell script
# GENERAL

# open new tab/window in the current $PWD
bind '"' split-window -c '#{pane_current_path}'
bind % split-window -h -c '#{pane_current_path}'
bind c new-window -c '#{pane_current_path}'

# set scrollback buffer to 10000 lines
set -g history-limit 10000

# set vim shortcuts for help and copy modes
setw -g mode-keys vi

# key bind
set -g prefix M-b
bind M-b send-prefix

# Pressing Ctrl+Shift+Left (will move the current window to the left. Similarly right. No need to use the modifier (C-b).
bind-key -n C-S-Left swap-window -t -1
bind-key -n C-S-Right swap-window -t +1


# NESTED TMUX SESSIONS

# press shift-up to toggle to the inner session
bind -n S-up \
        set -g status-right ' #[fg=colour253,bg=colour124] Nested Session: ON #[fg=colour233,bg=colour241,bold] %d/%m #[fg=colour233,bg=colour245,bold] %H:%M:%S ' \; \
        set -qg prefix C-b

# press shift-down to toggle to the outer session
bind -n S-down \
        set -g status-right '#[fg=colour237,bg=colour28] Nested Session: OFF #[fg=colour233,bg=colour241,bold] %d/%m #[fg=colour233,bg=colour245,bold] %H:%M:%S ' \; \
        set -qg prefix M-b


# APPEARANCE

set -g default-terminal 'screen-256color'

# panes
set -g pane-border-bg default
set -g pane-border-fg default
set -g pane-active-border-bg default
set -g pane-active-border-fg colour82

# statusbar
set -g status-position bottom
set -g status-bg colour234
set -g status-fg colour137
set -g status-attr dim
set -g status-left ''
set -g status-right '#[fg=colour237,bg=colour28] Nested Session: OFF #[fg=colour233,bg=colour241,bold] %d/%m #[fg=colour233,bg=colour245,bold] %H:%M:%S '
set -g status-right-length 50
set -g status-left-length 20

setw -g window-status-current-fg colour82
setw -g window-status-current-bg colour238
setw -g window-status-current-attr bold
setw -g window-status-current-format ' #I#[fg=colour250]:#[fg=colour255]#W#[fg=colour82]#F '

setw -g window-status-fg colour100
setw -g window-status-bg colour235
setw -g window-status-attr none
setw -g window-status-format ' #I#[fg=colour237]:#[fg=colour250]#W#[fg=colour244]#F '

setw -g window-status-bell-attr bold
setw -g window-status-bell-fg colour255
setw -g window-status-bell-bg colour1


# PLUGINS

set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'tmux-plugins/tmux-resurrect'

# initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'
```

### Usando Tmux

Para começar usar o tmux é só rodar o seguinte comando no terminal:
```
$ tmux
```

Ao rodar esse comando, o tmux será iniciado e criará uma nova sessão no tmux.
Sessões podem ter 1...N janelas. E janelas podem ter de 1...N tabs

Para criar uma nova Janela:
```
alt+b c 
```

Para criar uma nova Tab na horizontal:
```
alt+b "
```

Para criar uma nova Tab na vertical:
```
alt+b %
``` 


### Referências bacanas
https://leimao.github.io/blog/Tmux-Tutorial/
