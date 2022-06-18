# Installing git-filter-repo:

### Using `pip`:

You will need to have `python` and `pip` installed for this.\
(Needs git v2.22+ and python v3.5+. Check with git --version && python3 --version)

```bash
$ pip install git-filter-repo
```

### Using a `package manager`:

```bash
$ sudo PACKAGE_MANAGER install git-filter-repo
```

```bash
# pacman
$ sudo pacman -Syu git-filter-repo

# apt
$ sudo apt update
$ sudo apt install git-filter-repo
```

&nbsp;

# Using git-filter-repo:

## Email only

```bash
$ git filter-repo --email-callback '
    return email if email != b"incorrect@email" else b"correct@email"
'
```

## Email & Name

```bash
$ git filter-repo --commit-callback '
    if commit.author_email == b"incorrect@email":
        commit.author_email = b"correct@email"
        commit.author_name = b"Correct Name"
        commit.committer_email = b"correct@email"
        commit.committer_name = b"Correct Name"
'
```

&nbsp;

# Pushing out changes:

You will have to add the remote repo again.

```bash
$ git remote add origin git@github.com:$USERNAME/$REPO.git
```

All that is left to do is push the edited commits:

```
$ git push -u origin master --force
```

We had to set the `-u` flag (`set-upstream`) as we have just readded the remote repo.\
We also had to set the `--force` flag as we are overwriting previous commits.
