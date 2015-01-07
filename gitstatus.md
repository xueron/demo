## NAME
       git-status - Show the working tree status

## SYNOPSIS
       git status [<options>...] [--] [<pathspec>...]

## DESCRIPTION
       Displays paths that have differences between the index file and the current HEAD commit, paths that have differences between the
       working tree and the index file, and paths in the working tree that are not tracked by git (and are not ignored by gitignore(5)). The
       first are what you would commit by running git commit; the second and third are what you could commit by running git add before
       running git commit.

## OPTIONS
       -s, --short
           Give the output in the short-format.

       --porcelain
           Give the output in a stable, easy-to-parse format for scripts. Currently this is identical to --short output, but is guaranteed
           not to change in the future, making it safe for scripts.

       -u[<mode>], --untracked-files[=<mode>]
           Show untracked files (Default: all).

           The mode parameter is optional, and is used to specify the handling of untracked files. The possible options are:

           ·    no - Show no untracked files

           ·    normal - Shows untracked files and directories

           ·    all - Also shows individual files in untracked directories.
               See git-config(1) for configuration variable used to change the default for when the option is not specified.

           -z
               Terminate entries with NUL, instead of LF. This implies the --porcelain output format if no other format is given.

## OUTPUT
       The output from this command is designed to be used as a commit template comment, and all the output lines are prefixed with #. The
       default, long format, is designed to be human readable, verbose and descriptive. They are subject to change in any time.

       The paths mentioned in the output, unlike many other git commands, are made relative to the current directory if you are working in a
       subdirectory (this is on purpose, to help cutting and pasting). See the status.relativePaths config option below.

       In short-format, the status of each path is shown as

           XY PATH1 -> PATH2

       where PATH1 is the path in the HEAD, and ‘ → PATH2‘ part is shown only when PATH1 corresponds to a different path in the
       index/worktree (i.e. the file is renamed). The XY is a two-letter status code.

       The fields (including the →) are separated from each other by a single space. If a filename contains whitespace or other nonprintable
       characters, that field will be quoted in the manner of a C string literal: surrounded by ASCII double quote (34) characters, and with
       interior special characters backslash-escaped.

       For paths with merge conflicts, X and Y show the modification states of each side of the merge. For paths that do not have merge
       conflicts, X shows the status of the index, and Y shows the status of the work tree. For untracked paths, XY are ??. Other status
       codes can be interpreted as follows:

       ·   ´ ´ = unmodified

       ·    M = modified

       ·    A = added

       ·    D = deleted

       ·    R = renamed

       ·    C = copied

       ·    U = updated but unmerged

       Ignored files are not listed.

           X          Y     Meaning
           -------------------------------------------------
                     [MD]   not updated
           M        [ MD]   updated in index
           A        [ MD]   added to index
           D         [ M]   deleted from index
           R        [ MD]   renamed in index
           C        [ MD]   copied in index
           [MARC]           index and work tree matches
           [ MARC]     M    work tree changed since index
           [ MARC]     D    deleted in work tree
           -------------------------------------------------
           D           D    unmerged, both deleted
           A           U    unmerged, added by us
           U           D    unmerged, deleted by them
           U           A    unmerged, added by them
           D           U    unmerged, deleted by us
           A           A    unmerged, both added
           U           U    unmerged, both modified
           -------------------------------------------------
           ?           ?    untracked
           -------------------------------------------------

       There is an alternate -z format recommended for machine parsing. In that format, the status field is the same, but some other things
       change. First, the → is omitted from rename entries and the field order is reversed (e.g from → to becomes to from). Second, a NUL
       (ASCII 0) follows each filename, replacing space as a field separator and the terminating newline (but a space still separates the
       status field from the first filename). Third, filenames containing special characters are not specially formatted; no quoting or
       backslash-escaping is performed.

## CONFIGURATION
       The command honors color.status (or status.color — they mean the same thing and the latter is kept for backward compatibility) and
       color.status.<slot> configuration variables to colorize its output.

       If the config variable status.relativePaths is set to false, then all paths shown are relative to the repository root, not to the
       current directory.

       If status.submodulesummary is set to a non zero number or true (identical to -1 or an unlimited number), the submodule summary will
       be enabled for the long format and a summary of commits for modified submodules will be shown (see --summary-limit option of git-
       submodule(1)).