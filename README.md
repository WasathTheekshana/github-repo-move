# Duplicate GitHub Repos

### Step 1
Change the Remote Origin
```bash
git remote add new-origin git@github.com:username/your-new-repo.git
```

### Step 2
Verify the Remote location (optional)
```bash
git remote -v
```

### Step 3
Push all branches to the remote repo
```bash
git push new-origin --all
git push new-origin --tags
```

### Step 4
Fetch the origin
```bash
git fetch origin
```

### Step 5
Create local tracting branches for remote repo
```bash
for branch in $(git branch -r | grep 'origin/' | grep -v 'origin/HEAD' | sed 's/origin\///'); do
    # Check if the branch already exists locally
    if git show-ref --verify --quiet "refs/heads/$branch"; then
        echo "Branch '$branch' already exists locally, skipping."
    else
        git checkout -b "$branch" "origin/$branch" || echo "Failed to create branch '$branch'"
    fi
done
```

### Step 6
Push all branches individually
```bash
for branch in $(git branch | sed 's/\* //'); do
    git push new-origin "$branch"
done
```

