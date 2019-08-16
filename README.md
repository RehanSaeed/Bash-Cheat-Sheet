# Bash Cheat Sheet

 A cheat sheet for bash commands.

## Navigating Directories

```bash
pwd                    # Print current directory path
ls                     # List directories
ls -a                  # List directories including hidden
tree                   # List directory and file tree
tree -a                # List directory and file tree including hidden
tree -d                # List directory tree
cd foo                 # Go to foo sub-directory
cd ~                   # Go to home directory
cd -                   # Go to last directory
```

## Creating Directories

```bash
mkdir foo                     # Create a directory
mkdir foo bar                 # Create multiple directories
mkdir --parents foo/bar       # Create nested directory
mkdir --parents {foo,bar}/baz # Create multiple nested directories
```

## Moving Directories

```bash
cp --recursive foo bar # Copy directory
mv foo bar             # Move directory
rmdir foo              # Delete directory
```

## Creating Files

```bash
touch foo.txt          # Create file
touch foo.txt bar.txt  # Create multiple files
touch {foo,bar}.txt    # Create multiple files

echo "foo" > bar.txt   # Overwrite file with content
echo "foo" >> bar.txt  # Append to file with content
```

## Moving Files

```bash
cp foo.txt bar.txt     # Copy file
mv foo.txt bar.txt     # Move file
rm foo.txt             # Delete file
```

## Reading Files

```bash
cat foo.txt            # Print all contents
less foo.txt           # Print some contents at a time
head foo.txt           # Print top 10 lines of file
tail foo.txt           # Print bottom 10 lines of file
```

## Finding Files

```bash
# locate uses an index and is fast
locate foo.txt                        # Find a file
locate --ignore-case                  # Find a file and ignore case
locate f*.txt                         # Find a text file starting with 'f'
# find doesn't use an index and is slow
find /path -name foo.txt              # Find a file
find /path -type f -name foo.txt      # Find a file
find /path -type d -name foo          # Find a directory
find /path -type l -name foo.txt      # Find a symbolic link
find /path -type f -mtime +30         # Find files that haven't been modified in 30 days
find /path -type f -mtime +30 -delete # Delete files that haven't been modified in 30 days
```

## Find in Files

```bash
grep 'foo' /bar.txt                         # Search for 'foo' in file 'bar.txt'
grep 'foo' /bar -r|--recursive              # Search for 'foo' in directory 'bar'
grep 'foo' /bar -R|--dereference-recusive   # Search for 'foo' in directory 'bar' and follow symbolic links
grep 'foo' /bar -l|--files-with-matches     # Show only files that match
grep 'foo' /bar -L|--files-without-match    # Show only files that don't match
grep 'Foo' /bar -i|--ignore-case            # Case insensitive search
grep 'foo' /bar -x|--line-regexp            # Match the entire line
grep 'foo' /bar -v|--invert-match           # Show only lines that don't match
grep 'foo' /bar -c|--count                  # Count the number lines that match
grep 'foo\|bar' /baz -R                     # Search for 'foo' or 'bar' in directory 'baz'
grep --extended-regexp|-E 'foo|bar' /baz -R # Use regular expressions
egrep 'foo|bar' /baz -R                     # Use regular expressions
```

## Bash Profile

- bash - `.bashrc`
- zsh - `.zshrc`

```bash
# Always run ls after cd
function cd {
  builtin cd "$@" && ls
}

# Prompt user before overwriting any files
alias cp='cp --interactive'
alias mv='mv --interactive'
alias rm='rm --interactive'
```
