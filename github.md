Working with GitHub
===================

## Pushing an existing repository

```shell
$ git remote add origin git@github.com:<USER>/<REPO>.git
$ git push -u origin main
```

## Deploy keys

### Granting access to a single repository using a deploy key

> You can launch projects from a repository on GitHub.com to your server
> by using a deploy key, which is an SSH key that grants access to a single
> repository.

Deploy keys are managed under:

    https://github.com/<USER>/<REPO>/settings/keys

> **WARNING**
>
> A particular deploy key can be added to a _single repository_ only. This means
> that it is not possible  to use the _same key_ to grant access to multiple re-
> positories in the same GitHub account. The following section explains how to
> deal with this issue.

### Granting access to multiple repositories using multiple keys

To overcome the limitation that there can be only one particular deploy key per
_whole_ account and to grant access to multiple repositories to a particular
user, the user needs to use multiple distinct deploy keys -- one key per a repo-
sitory. This can be managed in Git by providing a custom `sshcommand` and point-
ing it to the per repo deploy key, like so:

```ini
[core]
    sshcommand = ssh -i ~/.ssh/com.github/<USER>/<REPO>.git
```

The key itself can be generated like so:

    $ ssh-keygen -t ed25519 -f ~/.ssh/com.github/<USER>/<REPO>.git

