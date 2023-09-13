# containerscripts
scripting for containers

# add passphrase to private key:
ssh-keygen -o -p -f id_rsa -a 1000



 # .bash_ansible_aliases
alias docker-ansible-cli='sudo /bin/docker run --rm -it -v ~/.profile:/srv/ansible/.profile -v /srv/ansible:/srv/ansible -v ~/.ssh:/root/.ssh -v /etc/hosts:/etc/hosts --workdir=/srv/ansible willhallonline/ansible /bin/ash .profile'

 # .profile
         # Append "$1" to $PATH when not already in.
         # Append "$1" to $PATH when not already in.
         # Copied from Arch Linux, see #12803 for details.
append_path () {
        case ":$PATH:" in
                *:"$1":*)
                        ;;
                *)
                        PATH="${PATH:+$PATH:}$1"
                        ;;
        esac
}

append_path "/usr/local/sbin"
append_path "/usr/local/bin"
append_path "/usr/sbin"
append_path "/usr/bin"
append_path "/sbin"
append_path "/bin"
append_path "/srv/ansible/scripts"
unset -f append_path

export PATH
export PAGER=less
umask 022

        # use nicer PS1 for bash and busybox ash
if [ -n "$BASH_VERSION" -o "$BB_ASH_VERSION" ]; then
        PS1='\h:\w\$ '
        # use nicer PS1 for zsh
elif [ -n "$ZSH_VERSION" ]; then
        PS1='%m:%~%# '
        # set up fallback default PS1
else
        : "${HOSTNAME:=$(hostname)}"
        PS1='${HOSTNAME%%.*}:$PWD'
        [ "$(id -u)" -eq 0 ] && PS1="${PS1}# " || PS1="${PS1}\$ "
fi
export PS1


for script in /etc/profile.d/*.sh ; do
        if [ -r "$script" ] ; then
                . "$script"
        fi
done
unset script

eval `ssh-agent`
ssh-add /root/.ssh/id_rsa
/bin/ash

--


