Perforce (p4)
=============

## List depots

_Depot_ can be thought of as a repository in git/svn.
And also as a _Perforce_ server.

    $ p4 depots

## List workspaces (clients)

_Workspace_ is a configuration sitting on the Perforce server. It configures the
relation between depot and user workstation. For example, it contains mapping
between depot's and local's paths, among other things. There can be multiple
workspaces.

     $ p4 workspaces # Also: $ p4 clients
     $ p4 workspaces -u <USERNAME>

## Edit workspace

     $ p4 workspace <WS_NAME>

## Delete workspace

> **NOTE**
>
> Before deleting a workspace, revert (or submit) any pending or
> shelved changelists associated with the workspace.
> Also, all opened files need to be closed first.

     $ p4 workspace -d <WS_NAME>

## List files in a depot

### Non-recursively

    $ p4 files //depot/'*'

### Recursively

    $ p4 files //depot/...

## List directories in a depot

> **NOTE**
>
> It's not possible to list directories recursively.

    $ p4 dirs //depot/'*'

## Submitting (committing) changes

### Create a changelist

_Changelist_ is a _Perforce_ term for a list of files to be manipulated in various
ways, e.g. shelving, submitting to the depot, etc.. By default, there is a changelist
named _default_ available in the workspace. The default changelist is the target
changelist for _Perforce_ commands when no particular changelist is specified to the
command in question.

To send a changelist for a review under _Swarm_, add _#review_ tag to
the description field.

> **WARNING**
>
> If you shelve a changelist and subsequently edit the description to include #review,
> a review is not started. You must **re-shelve** the files after adding #review.

    $ p4 change
    Change XYZ created.

### Add a file to a changelist, if the file ALREADY EXISTS in the depot

```
$ p4 edit -c <XYZ> path/to/main.c
//depot/path/to/main.c#1 - opened for edit

-n: Preview which files would be opened for edit,
    without actually changing any files or metadata.
```

> **WARNING**
>
> Limitations on characters in filenames and their replacements. The following
> characters need to be replaced with their %-prefixed replacements when
> operating on files in a filesystem.
>
> - @: %40
> - #: %23
> - *: %2A
> - %: %25

### Add a file to a changelist, if the file does NOT YET EXIST in the depot

```
$ p4 add [-n] -c <XYZ> path/to/main.c

-n: Preview which files would be opened for add,
    without actually changing any files or metadata.
```

### Inspect a changelist

```
$ p4 describe <XYZ>
Change XYZ by <name> on <date> <time> *pending*

    <description>

Affected files ...

... //depot/path/to/main.c#1
```

or

    $ p4 change <XYZ>

### Shelve files

_Shelving_ is a process of temporary storing changed files in the depot, so that the
files can be seen by others, without being _submitted_ to the depot. It is also a way
of making a snapshot of the current state of the files, allowing for example to
manage dependant changes to the same files. (Kind of _patch series_.)

Shelving copies files, as they are, from the workspace to the depot. The particular
version (shelf, contents) of the files can referenced by the changelist number.

    $ p4 shelve -c <XYZ>
    Change XYZ shelved.

## Shelves management

### Delete shelved files

> **NOTE**
>
> Shelved files persist in the depot until they are discarded (by means of
> `p4 shelve -d`) or replaced by subsequent p4 shelve commands.

    $ p4 shelve -d -c <XYZ>
    Shelved change XYZ deleted.

### Update shelved files

    $ p4 shelve -r -c <XYZ>

## Changelist management

## List changelists

```
$ p4 changes [-l] [-u <USERNAME>]
Change XYZ on <date> <name> *pending* '<description>'
Change ABC on <date> <name> *pending* '<description>'

-l:     List long output, with the full text of each changelist description.
-m max: List only the highest numbered max changes.
```
