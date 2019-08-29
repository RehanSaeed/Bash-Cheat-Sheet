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
cp --recursive foo bar                                  # Copy directory
mv foo bar                                              # Move directory
rmdir foo                                               # Delete directory

rsync -z|--compress -v|--verbose /foo /bar              # Copy directory, overwrites destination
rsync -a|--archive -z|--compress -v|--verbose /foo /bar # Copy directory, without overwriting destination
rsync -avz /foo username@hostname:/bar                  # Copy local directory to remote directory
rsync -avz username@hostname:/foo /bar                  # Copy remote directory to local directory
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
cp foo.txt bar.txt                                # Copy file
mv foo.txt bar.txt                                # Move file
rm foo.txt                                        # Delete file

rsync -z|--compress -v|--verbose /foo.txt /bar    # Copy file quickly if not changed
rsync z|--compress -v|--verbose /foo.txt /bar.txt # Copy and rename file quickly if not changed
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

## Compressing Files

### zip

Compresses one or more files into *.zip files.

```bash
zip foo.zip /bar.txt                # Compress bar.txt into foo.zip
zip foo.zip /bar.txt /baz.txt       # Compress bar.txt and baz.txt into foo.zip
zip foo.zip /{bar,baz}.txt          # Compress bar.txt and baz.txt into foo.zip
zip -r|--recurse-paths foo.zip /bar # Compress directory bar into foo.zip
```

### gzip

Compresses a single file into *.gz files.

```bash
gzip /bar.txt foo.gz           # Compress bar.txt into foo.gz and then delete bar.txt
gzip -k|--keep /bar.txt foo.gz # Compress bar.txt into foo.gz
```

### tar -c

Compresses (optionally) and combines one or more files into a single *.tar, *.tar.gz, *.tpz or *.tgz file.

```bash
tar -c|--create -z|--gzip -f|--file=foo.tgz /bar.txt /baz.txt # Compress bar.txt and baz.txt into foo.tgz
tar -c|--create -z|--gzip -f|--file=foo.tgz /{bar,baz}.txt    # Compress bar.txt and baz.txt into foo.tgz
tar -c|--create -z|--gzip -f|--file=foo.tgz /bar              # Compress directory bar into foo.tgz
```

## Decompressing Files

### unzip

```bash
unzip foo.zip          # Unzip foo.zip into current directory
```

### gunzip

```bash
gunzip foo.gz           # Unzip foo.gz into current directory and delete foo.gz
gunzip -k|--keep foo.gz # Unzip foo.gz into current directory
```

### tar -x

```bash
tar -x|--extract -z|--gzip -f|--file=foo.tar.gz # Uncompress foo.tar.gz into current directory
tar -x|--extract -f|--file=foo.tar              # Uncombine foo.tar into current directory
```

## Disk Usage

```bash
df                     # List disks, size, used and available space
df -h|--human-readable # List disks, size, used and available space in a humarn readable format

du                     # List current directory, subdirectories and file sizes
du /foo/bar            # List specified directory, subdirectories and file sizes
du -h|--human-readable # List current directory, subdirectories and file sizes in a humarn readable format
du -d|--max-depth      # List current directory, subdirectories and file sizes within the max depth
du -d 0                # List current directory size
```

## Shutdown and Reboot

```bash
shutdown                     # Shutdown in 1 minute
shutdown now "Cya later"     # Immediately shut down
shutdown +5 "Cya later"      # Shutdown in 5 minutes

shutdown --reboot            # Reboot in 1 minute
shutdown -r now "Cya later"  # Immediately reboot
shutdown -r +5 "Cya later"   # Reboot in 5 minutes

shutdown -c                  # Cancel a shutdown or reboot

reboot                       # Reboot now
reboot -f                    # Force a reboot
```

## Identifying Processes

```bash
top                    # List all processes
htop             #
pidof foo              # Return the PID of all foo processes

sleep 30 &             # Sleep for 30 seconds and move the process into the background
jobs                   # List all background jobs
jobs -p                # List all background jobs with their PID

lsof                   # List all open files and the process using them
lsof -itcp:4000        # Return the process listening on port 4000
```

## Process Priority

Process priorities go from -20 (highest) to 19 (lowest).

```bash
nice -n -20 foo        # Change process priority by name
renice 20 PID          # Change process priority by PID
ps -o ni PID           # Return the process priority of PID
```

## Killing Processes

```bash
kill PID               # Shut down process by PID gracefully. Sends TERM signal.
kill -9 PID            # Force shut down of process by PID. Sends SIGKILL signal.
pkill foo              # Shut down process by name gracefully. Sends TERM signal.
pkill -9 foo           # force shut down process by name. Sends SIGKILL signal.
killall foo            # Kill all process with the specified name gracefully.
```

## Scheduled Tasks

```pre
   *      *         *         *           *
Minute, Hour, Day of month, Month, Day of the week
```

```bash
crontab -l                 # List cron tab
crontab -e                 # Edit cron tab in Vim
crontab /path/crontab      # Load cron tab from a file
crontab -l > /path/crontab # Save cron tab to a file

* * * * * foo              # Run foo every minute
*/15 * * * * foo           # Run foo every 15 minutes
0 * * * * foo              # Run foo every hour
15 6 * * * foo             # Run foo daily at 6:15 AM
44 4 * * 5 foo             # Run foo every Friday at 4:44 AM
0 0 1 * * foo              # Run foo at midnight on the first of the month
0 0 1 1 * foo              # Run foo at midnight on the first of the year

at -l                      # List scheduled tasks
at -c 1                    # Show task with ID 1
at -r 1                    # Remove task with ID 1
at now + 2 minutes         # Create a task in Vim to execute in 2 minutes
at 12:34 PM next month     # Create a task in Vim to execute at 12:34 PM next month
at tomorrow                # Create a task in Vim to execute tomorrow
```

## Network Troubleshooting

```bash
ping example.com                 # Send multiple ping requests using the ICMP protocol
ping -c 10 -i 5 example.com      # Make 10 attempts, 5 seconds apart
traceroute example.com           # List all servers the network traffic goes through
mtr -w|--report-wide example.com                                    # Continually list all servers the network traffic goes through
mtr -r|--report -w|--report-wide -c|--report-cycles 100 example.com # Output a report that lists network traffic 100 times
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

# Always show disk usage in a human readable format
alias df='df -h'
alias du='du -h'
```
