# Bash Cheat Sheet

 A cheat sheet for bash commands.

## Navigating Directories

```bash
ls                     # List directories
ls -a                  # List directories including hidden
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
