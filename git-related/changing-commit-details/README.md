# Installing git-filter-repo:

You will need to have `python` and `pip` installed for this.\
(Needs git v2.22+ and python v3.5+. Check with git --version && python3 --version)

```bash
$ pip install git-filter-repo
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
