1 demo

```
# Initialize a new Git repository
git init example-repo
cd example-repo

# Create a file and make the first commit
echo 'Hello, Git!' > hello.txt
git add hello.txt
git commit -m "Initial commit"

# Look inside the .git/objects directory
ls .git/objects
```

2 demo

```
# View the commit object
git log --oneline

# Take the SHA of the commit and inspect it
SHA=$(git rev-parse HEAD)
git cat-file -t $SHA  # This shows the type of the object (commit)
git cat-file -p $SHA  # This shows the content of the commit object
```

3 demo

```
# Inspect the tree object that the commit points to
TREE=$(git cat-file -p $SHA | grep tree | awk '{print $2}')
git cat-file -t $TREE  # This shows the type of the object (tree)
git cat-file -p $TREE  # This shows the content of the tree object
```

4 demo

```
# Inspect a blob object
BLOB=$(git cat-file -p $TREE | grep blob | awk '{print $3}')
git cat-file -t $BLOB  # This shows the type of the object (blob)
git cat-file -p $BLOB  # This shows the content of the blob (the file's contents)
```

```
# Copy and rename files in the repository
cp hello.txt hello_renamed.txt
git add hello_renamed.txt
git commit -m "Rename file"

# Inspect the new tree and blob objects
SHA_LATEST=$(git rev-parse HEAD)
TREE_LATEST=$(git cat-file -p $SHA_LATEST | grep tree | awk '{print $2}')
git cat-file -p $TREE_LATEST  # Notice the same blob SHA for the copied file
```

5 demo

```
# Inspect the branch pointer
cat .git/refs/heads/master

# Demonstrate the HEAD pointer
cat .git/HEAD

# Demonstrate changing HEAD
echo 'ref: refs/heads/new-branch' > .git/HEAD
git status  # This will now reflect the new branch
```



