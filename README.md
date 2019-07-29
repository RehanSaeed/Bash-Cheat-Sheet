## Directories

# Create a directory
mkdir reptiles
# Create multiple directories
mkdir alligator crocodile snake
# Create nested directory
mkdir --parents turtle/images
# Create multiple nested directories
mkdir --parents {alligator,crocodile}/videos

# Files

# Create file
touch foo.txt
# Create multiple files
touch foo.txt bar.txt
touch {foo,bar}.txt
# Overwrite file with content
echo "foo" > bar.txt
# Append to file with content
echo "foo" >> bar.txt