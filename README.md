# Programmatically colorize files in elementary OS

Want to highlight files that fit a certain criteria for later use, and not satisified with search? Then this script is for you.

`pantheon-files-colorize` is a command that lets you set display colors for arbitrary files that will be displayed in elementary OS file manager, `pantheon-files`. You can use it from shell scripts or any other programs to highlight files based on arbitrarily complex criteria.

Run `pantheon-files-colorize` without parameters to see the list of supported colors and detailed usage instructions.

## Examples

### Taint code with TODOs or FIXMEs
`for file in ./*; do (grep -q TODO "$file" || grep -q FIXME "$file") && pantheon-files-colorize red "$file"`

### Get horrified by the sizes of binaries in /usr/bin
```
for file in /usr/bin/*; do
    size_in_bytes=$(stat --format='%s' "$file")
    if [ "$size_in_bytes" -lt 100000]; then
        pantheon-files-colorize green "$file" # under 100kb
    elif [ "$size_in_bytes" -lt 1000000 ]; then
        pantheon-files-colorize yellow "$file" # under 1Mb
    else
        pantheon-files-colorize red "$file" # over 1Mb
    fi
done
```

### Reset color for all files in the current folder and all of its subfolders
`pantheon-files-colorize none **`


## Limitations

You need to refresh the directory in pantheon-files to see changes made by this script. The keyboard shortcut for that is `Ctrl+R`
