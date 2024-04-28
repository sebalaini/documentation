# Linux

## [Mitchell Krog (Linux specialist)](https://github.com/mitchellkrogza?tab=repositories)

## find

<details>
<summary>How to use the find command</summary>

### Find Linux Files by Name or Extension

Use `find` from the command line to locate a specific file by name or extension. The following example searches for `*.err` files in the `/home/username/` directory and all sub-directories:

```bash
find /home/username/ -name "*.err"
```

### Common Linux Find Commands and Syntax

`find` expressions take the following form:

```bash
find options starting/path expression
```

- The `options` attribute will control the behavior and optimization method of the `find` process.
- The `starting/path` attribute will define the top level directory where `find` begins filtering.
- The `expression` attribute controls the tests that search the directory hierarchy to produce output.

Consider the following example command:

```bash
find -O3 -L /var/www/ -name "*.html"
```

This command enables the maximum optimization level \(-O3\) and allows `find` to follow symbolic links \(`-L`\). `find` searches the entire directory tree beneath `/var/www/` for files that end with `.html`.

#### Basic Examples

| Command                                              | Description                                                                                            |
| :--------------------------------------------------- | :----------------------------------------------------------------------------------------------------- |
| `find . -name testfile.txt`                          | Find a file called testfile.txt in current and sub-directories.                                        |
| `find /home -name \*.jpg`                            | Find all `.jpg` files in the `/home` and sub-directories.                                              |
| `find . -type f -empty`                              | Find an empty file within the current directory.                                                       |
| `find /home -user exampleuser -mtime 7 -iname ".db"` | Find all `.db` files \(ignoring text case\) modified in the last 7 days by a user named `exampleuser`. |

</details>

## remote script from local

<details>
<summary>How to run a remote script from local</summary>

To run a remote script from local you need two scripts:

- one on the source machine,
- another one on the destination machine.

The script on the source machine should be something like:

```bash
rsync ... ... ... syncuser@destination:/dest/path
ssh syncuser@destination "sudo /some/path/to/completesync.sh"
```

And on the destination machine, the script `/some/path/to/completesync.sh` which contains something like this:

```bash
#!/bin/sh

php artisan cache:clear
php artisan config:cache
# whatever else you need to run as root
```

Be careful to have restricted rights on this script:

```bash
chown root:root /path/to/completesync.sh && chmod 700 /path/to/completesync.sh
```

Last, modify `/etc/sudoers` on the destination machine so that `syncuser` can run both `rsync` and your script as root:

```bash
syncuser ALL=NOPASSWD: /usr/bin/rsync, /path/to/completesync.sh
```

Now running the script on the source machine should complete the whole process in one operation.

</details>

## symlink

<details>
<summary>How to create a symlink</summary>

### How to create a symlink to a file

Here is the basic syntax for creating a symlink to a file in your terminal.

```bash
ln -s existing_source_file optional_symbolic_link
```

You use the `ln` command to create the links for the files and the `-s` option to specify that this will be a symbolic link. If you omit the `-s` option, then a hard link will be created instead.

- The `existing_source_file` represents the file you want to create the symbolic link for.
- The `optional_symbolic_link` parameter is the name of the symbolic link you want to create. If omitted, then the system will create a new link for you in the current directory you are in.

</details>
