# Useful Documentation

Welcome to my documentation, I decided to create this repo to save all the thing I may need in the future (such as how to reinstall a software and configure it again) or stuff that I rarely use and I always need to search for it.

<details open>
<summary>Table of Content</summary>

- [Github / git](#github)
- [Linux](#linux)
  - [Mitchell Krog (Linux specialist)](#mitchell-krog-linux-specialist)
  - [find](#find)
  - [remote script from local](#remote-script-from-local)
  - [symlink](#symlink)
- [SEO](#seo)
  - [SEO general](#seo-general)
  - [SEO for social networks](#seo-for-social-networks)
  - [SEO tools](#seo-tools)
- [Design](#design)
  - [Mockup generator](#mockup-generator)
  - [Design inspiration](#design-inspiration)
  - [Colors tools](#colors-tools)
  - [Icon sets](#icon-sets)
  - [Fonts](#fonts)
  - [Google maps styles](#google-maps-styles)
  - [Images](#images)
    - [Free Images](#free-images)
    - [Images tools](#images-tools)
- [CSS](#css)
  - [CSS triangle](#css-triangle)
  - [hidden element for accessibility](#hidden-elements-for-accessibility)
- [SVG](#svg)
  - [SVGO](#svgo)
  - [SVG libraries](#svg-libraries)

</details>
<br>

# GitHub / git

- Create useful [.gitignore](https://www.toptal.com/developers/gitignore) files for your project.
- Reset local changes alias.
  ```bash
  alias nah="git reset HEAD --hard && git checkout . && git clean -df ."
  ```
- Git amend last commit using last message & push alias.
  ```bash
  alias gitamendforce="git add . && git commit --amend --no-edit && git push --force"
  ```
  The `--no-edit` reuse the last commit message.<br>
  If you want to squash multiple commit you need to run this command:
  ```bash
  $ git rebase -i HEAD~3 #where 3 is the number of commit to merge
  ```

<br>

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

| Command | Description |
| :---    | :--- |
| find . -name testfile.txt | Find a file called testfile.txt in current and sub-directories. |
| find /home -name \*.jpg | Find all `.jpg` files in the `/home` and sub-directories. |
| find . -type f -empty | Find an empty file within the current directory. |
| find /home -user exampleuser -mtime 7 -iname ".db" | Find all `.db` files \(ignoring text case\) modified in the last 7 days by a user named exampleuser. |

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

Last, modify `/etc/sudoers` on the destination machine so that `syncuser` can run both rsync and your script as root:

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

<br>

# SEO

## SEO general
- [beginner guide to SEO](https://moz.com/beginners-guide-to-seo)
- [recommended minimum HEAD](https://github.com/joshbuchea/HEAD#recommended-minimum)
- [A simple guide to HTML `<head>` elements](https://htmlhead.dev/)

## SEO for social networks
- [essentials meta tags for social network](https://css-tricks.com/essential-meta-tags-social-media/)
- [Facebook sharing preview](https://developers.facebook.com/tools/debug/)
- [Facebook debugger](https://developers.facebook.com/tools/debug/)
- [Linkedin sharing preview](https://www.linkedin.com/post-inspector/)

## SEO tools
- [Google Console](https://search.google.com/search-console)
- [Remove outdated content from Google search](https://www.google.com/webmasters/tools/removals)
- [Rich Results Test – Google Search Console](https://search.google.com/test/rich-results)

<br>

# Design

## Mockup generator

- [smartmockup](https://smartmockups.com/category/digital/all?filter=free)
  - [Portfolio Projects mockup](https://smartmockups.com/mockup/Wu8A4epzz)
- [multimockup](http://techsini.com/multi-mockup/index.php)
- [mockdrop](http://mockdrop.io/)

## Design inspiration

- [landingfolio](https://www.landingfolio.com/inspiration/landing-page)
- [dribbble](https://dribbble.com/)

## Colors tools

- [materials io](https://material.io/tools/color/#!/?view.left=0&view.right=0)
- [colorspace](https://mycolor.space/)

## Icon sets

- [Heroicons UI](https://github.com/sschoger/heroicons-ui)
- [Zondicons](http://www.zondicons.com/)
- [Entypo](http://www.entypo.com/)
- [Streamline](https://www.streamlinehq.com/)

## Fonts

- [Google webfonts helper](https://gwfh.mranftl.com/fonts)
- [best free Google fonts](https://daveyandkrista.com/best-free-google-fonts/)

## Google maps styles

- [snazzymaps](https://snazzymaps.com/)

## Images

### Free Images

- [unsplash](https://unsplash.com/)
- [videezy](https://www.videezy.com/)

### Images tools

- [tinypng compressor](https://tinypng.com/)
- [compressor.io](https://compressor.io/)
- [edit resize, crop and compress jpeg and png images](https://mozjpeg.com/)
- [Convert many images to JPG online at once](https://www.iloveimg.com/convert-to-jpg)
- [Resize batches of images](https://bulkresizephotos.com/en)

<br>

# CSS

## CSS triangle

How to create triangles with pure CSS

```css
.left-arrow {
	border-color: transparent black;
	border-style: solid;
	border-width: 20px 20px 20px 0px;
	height: 0px;
	width: 0px;
}

.right-arrow {
	border-color: transparent black;
	border-style: solid;
	border-width: 20px 0px 20px 20px;
	height: 0px;
	width: 0px;
}

.down-arrow {
	border-color: black transparent;
	border-style: solid;
	border-width: 20px 20px 0px 20px;
	height: 0px;
	width: 0px;
}

.up-arrow {
	border-color: black transparent;
	border-style: solid;
	border-width: 0px 20px 20px 20px;
	height: 0px;
	width: 0px;
}
```

## hidden elements for accessibility

A useful class for hidden visual element and let the screen reader see the elements 

```css
.visuallyhidden {
    border: 0;
    clip: rect(0 0 0 0);
    height: 1px;
    margin: -1px;
    overflow: hidden;
    padding: 0;
    position: absolute;
    width: 1px;
    left: 103px;
    top: 71px;
}
```
<br>

# SVG

## SVGO

- [CLI](https://github.com/svg/svgo)
- [GUI (svgomg)](https://jakearchibald.github.io/svgomg/)

## SVG libraries

- [svgrepo](https://www.svgrepo.com/)
