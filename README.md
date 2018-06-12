# bash_autocomplete [Ubuntu/Debian]

I was sitting and wondering how this works so I gave it a **bash**

If you file is called myservice.sh and you execute it as **myservice.sh** then the last line in the following code snippet is true, but if you execute it as **./myservice.sh** then you need to add the **./**

So create a bash_completion instruction file, **/etc/bash_completion.d/myservice**
```
_myservice()
{
    local cur prev opts
    COMPREPLY=()
    cur="${COMP_WORDS[COMP_CWORD]}"
    prev="${COMP_WORDS[COMP_CWORD-1]}"
    opts="start stop status"

# this can be alot more complicated like looking at 
# what was typed then displaying the appropiate options
#    if [[ ${cur} == st* ]] ; then
        COMPREPLY=( $(compgen -W "${opts}" -- ${cur}) )
#        return 0
#    fi
}
complete -F _myservice myservice.sh
```

Now the important bit:
issue the instruction to compile/run the completion script
```
. /etc/bash_completion.d/myservice
```
Now try it:
```
myservice.sh st[TAB][TAB]
```
