# Bash Cheat Sheet

 A cheat sheet for bash commands.

## Navigating Directories

```bash
ls     # List directories
ls -a  # List directories including hidden
cd foo # Go to foo sub-directory
cd ~   # Go to home directory
cd -   # Go to last directory
```

## Creating Directories

```bash
# Create a directory
mkdir reptiles
# Create multiple directories
mkdir alligator crocodile snake
# Create nested directory
mkdir --parents turtle/images
# Create multiple nested directories
mkdir --parents {alligator,crocodile}/videos
```

## Creating Files

```bash
# Create file
touch foo.txt
# Create multiple files
touch foo.txt bar.txt
touch {foo,bar}.txt
# Overwrite file with content
echo "foo" > bar.txt
# Append to file with content
echo "foo" >> bar.txt
```

## Bash Profile

- bash - `.bashrc`
- zsh - `.zshrc`

```bash
# Always run ls after cd
function cd {
  builtin cd "$@" && ls
}
```
