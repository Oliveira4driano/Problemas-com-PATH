# Problemas-com-PATH

Pessoal, estou usando o Debian wheezy, e depois de dar um upgrade no sistema, estou tendo problemas para instalação de programas, sempre que tento instalar algo aparece.

dpkg: aviso: 'ldconfig' não foi encontrado em PATH ou não é executável.
dpkg: aviso: 'start-stop-daemon' não foi encontrado em PATH ou não é executável.
dpkg: error: 2 expected programs not found in PATH or not executable.
Note: root's PATH should usually contain /usr/local/sbin, /usr/sbin and /sbin.
E: Sub-process /usr/bin/dpkg returned an error code (2)

Já verifiquei o meu PATH e está: /usr/local/bin:/usr/bin:/bin:/usr/games

Agradeço demais se alguém puder me ajudar.

para resolver é simples, muito simples:

1) entre no terminal e digite: nano /etc/profile

vai aparecer algo do tipo


# /etc/profile: system-wide .profile file for the Bourne shell (sh(1))
# and Bourne compatible shells (bash(1), ksh(1), ash(1), ...).

if [ "`id -u`" -eq 0 ]; then
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
else
PATH="/usr/local/bin:/usr/bin:/bin:/usr/games"
fi

não sei pq raios ele tá pegando a segunda instrução, então, para solucionar, é só vc colocar o /sbin após game, pra ficar assim

if [ "`id -u`" -eq 0 ]; then
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
else
PATH="/usr/local/bin:/usr/bin:/bin:/usr/games/sbin"
fi

e pronto.

salve e feche esse arquivo e digite o seguinte comando: source /etc/profile
