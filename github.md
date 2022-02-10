

# Push an existing repository

> **TODO**
>
> Add description about how to create the remote repository
> from command line. Some info can be found here:
>
> https://gist.github.com/alexpchin/dc91e723d4db5018fef8

    $ git remote add origin git@github.com:${USER}/${REPO}.git
    $ git push -u origin main

# Grant access to a single repository using a deploy key

> You can launch projects from a repository on GitHub.com
> to your server by using a deploy key, which is an SSH key
> that grants access to a single repository.

Deploy keys are managed under:

    https://github.com/${USER}/${REPO}/settings/keys
