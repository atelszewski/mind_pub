# sudo - execute a command as another user

```
root  ALL = (ALL:ALL)    ALL
^     ^      ^           ^
|     |      |           |
User  Hosts  User:Group  Command
```

Read it as:

User `root` can run _any_ command as _any_ user from _any_ group on _any_ host.
To put it very simple, it is:

```
WHO WHERE = (AS_WHOM) WHAT
```

- The first `ALL` is used to define hosts.
  We can define hostname/ IP address instead of `ALL`.
  `ALL` means any host.

- The second and third `ALL:ALL` is `user:group`.
  Instead of `ALL` we can define user or user with the group like `user:group`.
  `ALL:ALL` means _all_ users and _all_ groups.

- Last `ALL` is the _command_.
  Instead of `ALL`, we can define a command or set of commands.
  `ALL` means _any_ command.

> **NOTE**
>
> _Hosts_ is the **local** hostname/ IP address.
> It's often misunderstood as a remote host.
> _Hosts_ field will be rarely used and makes
> sense if a _centralized_ sudoers configuration
> is pushed to multiple hosts.

References:

- [Linux Fundamentals: A to Z of a Sudoers File](https://medium.com/kernel-space/linux-fundamentals-a-to-z-of-a-sudoers-file-a5da99a30e7f)
