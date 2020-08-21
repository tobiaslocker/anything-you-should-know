## Bash
### Make a new directory and change into it
needs quotes for dirname with spaces
```console
$ mkdir foo && cd $_ 
```
### Check processes that listen on port (e.g. 80)
```console
$ sudo lsof -i -P -n | grep 80
```
### Open files in `src/` containin `foo` in `vim`
```console
$ grep -R -i -l foo src/ | xargs -o vim -o
```
