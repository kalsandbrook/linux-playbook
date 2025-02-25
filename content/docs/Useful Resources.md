A collection of useful resources, tutorials and information on various Linux subjects.

## man pages

The `man` command is probably the most important command for any Linux system. Users may see commands titled in the format `APPLICATION(1)`, the number at the end of these indicate the section of the manual being read. Some pages exist in multiple sections, and man will provide the first page found (according to a priority order of each section).

The sections are as follows:

| N   | Section Title                                                                                      |
| --- | -------------------------------------------------------------------------------------------------- |
| 1   | Executable programs or shell commands                                                              |
| 2   | System calls (functions provided by the kernel)                                                    |
| 3   | Library calls (functions within program libraries)                                                 |
| 4   | Special files (usually found in `/dev`)                                                            |
| 5   | File formations and conventions, e.g. `/etc/passwd`                                                |
| 6   | Games                                                                                              |
| 7   | Miscellaneous (including macro packages and conventions) e.g. `man(7)`, `groff(7)`, `man-pages(7)` |
| 8   | System administration commands (typically only for root)                                           |
| 9   | Kernel routines \[Non standard\]                                                                   |

This table is taken verbatim from `man man`, where more details can be found.
### Tips and Tricks

To pull up a page from a specific section, man can be used in the format `man [section] [page]`, for example: `man 1 bash`.

The commands `apropos` and `man -k` can be used to search through man pages by keyword.

Finally, `man -f [page]` can be used to to print a short description of a page.

## The ArchWiki

>[!important]
>Even though information on the ArchWiki is generally specific to the Arch Linux distribution, many of its articles on specific packages and utilities can prove valuable to those on other distributions.
>
>However, approach any commands and filepaths provided with caution.

[The Arch Linux Wiki](https://wiki.archlinux.org)

The wiki for Arch Linux contains a wealth of information on the Arch Linux distribution and many packages that can be found.

## Fedora Documentation

[Fedora Documentation](https://docs.fedoraproject.org/en-US/docs/)

Fedora documentation provides guides on system administration and troubleshooting for Fedora Linux. 