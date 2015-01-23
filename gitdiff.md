## NAME
       git-diff - Show changes between commits, commit and working tree, etc

## SYNOPSIS
       git diff [<common diff options>] <commit>{0,2} [--] [<path>...]

## DESCRIPTION
       Show changes between two trees, a tree and the working tree, a tree and the index file, or the index file and the working tree.

       git diff [--options] [--] [<path>...]
           This form is to view the changes you made relative to the index (staging area for the next commit). In other words, the
           differences are what you could tell git to further add to the index but you still haven’t. You can stage these changes by using
           git-add(1).

           If exactly two paths are given, and at least one is untracked, compare the two files / directories. This behavior can be forced
           by --no-index.

       git diff [--options] --cached [<commit>] [--] [<path>...]
           This form is to view the changes you staged for the next commit relative to the named <commit>. Typically you would want
           comparison with the latest commit, so if you do not give <commit>, it defaults to HEAD. --staged is a synonym of --cached.

       git diff [--options] <commit> [--] [<path>...]
           This form is to view the changes you have in your working tree relative to the named <commit>. You can use HEAD to compare it
           with the latest commit, or a branch name to compare with the tip of a different branch.

       git diff [--options] <commit> <commit> [--] [<path>...]
           This is to view the changes between two arbitrary <commit>.

       git diff [--options] <commit>..<commit> [--] [<path>...]
           This is synonymous to the previous form. If <commit> on one side is omitted, it will have the same effect as using HEAD instead.

       git diff [--options] <commit>...<commit> [--] [<path>...]
           This form is to view the changes on the branch containing and up to the second <commit>, starting at a common ancestor of both
           <commit>. "git diff A...B" is equivalent to "git diff $(git-merge-base A B) B". You can omit any one of <commit>, which has the
           same effect as using HEAD instead.

       Just in case if you are doing something exotic, it should be noted that all of the <commit> in the above description, except for the
       last two forms that use ".." notations, can be any <tree-ish>.

       For a more complete list of ways to spell <commit>, see "SPECIFYING REVISIONS" section in git-rev-parse(1). However, "diff" is about
       comparing two endpoints, not ranges, and the range notations ("<commit>..<commit>" and "<commit>...<commit>") do not mean a range as
       defined in the "SPECIFYING RANGES" section in git-rev-parse(1).

## OPTIONS
       -p, -u
           Generate patch (see section on generating patches). This is the default.

       -U<n>, --unified=<n>
           Generate diffs with <n> lines of context instead of the usual three. Implies -p.

       --raw
           Generate the raw format.

       --patch-with-raw
           Synonym for -p --raw.

       --patience
           Generate a diff using the "patience diff" algorithm.

       --stat[=width[,name-width]]
           Generate a diffstat. You can override the default output width for 80-column terminal by --stat=width. The width of the filename
           part can be controlled by giving another width to it separated by a comma.

       --numstat
           Similar to --stat, but shows number of added and deleted lines in decimal notation and pathname without abbreviation, to make it
           more machine friendly. For binary files, outputs two - instead of saying 0 0.

       --shortstat
           Output only the last line of the --stat format containing total number of modified files, as well as number of added and deleted
           lines.

       --dirstat[=limit]
           Output the distribution of relative amount of changes (number of lines added or removed) for each sub-directory. Directories with
           changes below a cut-off percent (3% by default) are not shown. The cut-off percent can be set with --dirstat=limit. Changes in a
           child directory is not counted for the parent directory, unless --cumulative is used.

       --dirstat-by-file[=limit]
           Same as --dirstat, but counts changed files instead of lines.

       --summary
           Output a condensed summary of extended header information such as creations, renames and mode changes.

       --patch-with-stat
           Synonym for -p --stat.

       -z
           When --raw, --numstat, --name-only or --name-status has been given, do not munge pathnames and use NULs as output field
           terminators.

           Without this option, each pathname output will have TAB, LF, double quotes, and backslash characters replaced with \t, \n, \",
           and \\, respectively, and the pathname will be enclosed in double quotes if any of those replacements occurred.

       --name-only
           Show only names of changed files.

       --name-status
           Show only names and status of changed files. See the description of the --diff-filter option on what the status letters mean.

       --submodule[=<format>]
           Chose the output format for submodule differences. <format> can be one of short and log.  short just shows pairs of commit names,
           this format is used when this option is not given.  log is the default value for this option and lists the commits in that commit
           range like the summary option of git-submodule(1) does.

       --color[=<when>]
           Show colored diff. The value must be always (the default), never, or auto.

       --no-color
           Turn off colored diff, even when the configuration file gives the default to color output. Same as --color=never.

       --color-words[=<regex>]
           Show colored word diff, i.e., color words which have changed. By default, words are separated by whitespace.

           When a <regex> is specified, every non-overlapping match of the <regex> is considered a word. Anything between these matches is
           considered whitespace and ignored(!) for the purposes of finding differences. You may want to append |[^[:space:]] to your
           regular expression to make sure that it matches all non-whitespace characters. A match that contains a newline is silently
           truncated(!) at the newline.

           The regex can also be set via a diff driver or configuration option, see gitattributes(1) or git-config(1). Giving it explicitly
           overrides any diff driver or configuration setting. Diff drivers override configuration settings.

       --no-renames
           Turn off rename detection, even when the configuration file gives the default to do so.

       --check
           Warn if changes introduce trailing whitespace or an indent that uses a space before a tab. Exits with non-zero status if problems
           are found. Not compatible with --exit-code.

       --full-index
           Instead of the first handful of characters, show the full pre- and post-image blob object names on the "index" line when
           generating patch format output.

       --binary
           In addition to --full-index, output a binary diff that can be applied with git-apply.

       --abbrev[=<n>]
           Instead of showing the full 40-byte hexadecimal object name in diff-raw format output and diff-tree header lines, show only a
           partial prefix. This is independent of the --full-index option above, which controls the diff-patch output format. Non default
           number of digits can be specified with --abbrev=<n>.

       -B
           Break complete rewrite changes into pairs of delete and create.

       -M
           Detect renames.

       -C
           Detect copies as well as renames. See also --find-copies-harder.

       --diff-filter=[ACDMRTUXB*]
           Select only files that are Added (A), Copied (C), Deleted (D), Modified (M), Renamed (R), have their type (i.e. regular file,
           symlink, submodule, ...) changed (T), are Unmerged (U), are Unknown (X), or have had their pairing Broken (B). Any combination of
           the filter characters may be used. When * (All-or-none) is added to the combination, all paths are selected if there is any file
           that matches other criteria in the comparison; if there is no file that matches other criteria, nothing is selected.

       --find-copies-harder
           For performance reasons, by default, -C option finds copies only if the original file of the copy was modified in the same
           changeset. This flag makes the command inspect unmodified files as candidates for the source of copy. This is a very expensive
           operation for large projects, so use it with caution. Giving more than one -C option has the same effect.

       -l<num>
           The -M and -C options require O(n^2) processing time where n is the number of potential rename/copy targets. This option prevents
           rename/copy detection from running if the number of rename/copy targets exceeds the specified number.

       -S<string>
           Look for differences that introduce or remove an instance of <string>. Note that this is different than the string simply
           appearing in diff output; see the pickaxe entry in gitdiffcore(7) for more details.

       --pickaxe-all
           When -S finds a change, show all the changes in that changeset, not just the files that contain the change in <string>.

       --pickaxe-regex
           Make the <string> not a plain string but an extended POSIX regex to match.

       -O<orderfile>
           Output the patch in the order specified in the <orderfile>, which has one shell glob pattern per line.

       -R
           Swap two inputs; that is, show differences from index or on-disk file to tree contents.

       --relative[=<path>]
           When run from a subdirectory of the project, it can be told to exclude changes outside the directory and show pathnames relative
           to it with this option. When you are not in a subdirectory (e.g. in a bare repository), you can name which subdirectory to make
           the output relative to by giving a <path> as an argument.

       -a, --text
           Treat all files as text.

       --ignore-space-at-eol
           Ignore changes in whitespace at EOL.

       -b, --ignore-space-change
           Ignore changes in amount of whitespace. This ignores whitespace at line end, and considers all other sequences of one or more
           whitespace characters to be equivalent.

       -w, --ignore-all-space
           Ignore whitespace when comparing lines. This ignores differences even if one line has whitespace where the other line has none.

       --inter-hunk-context=<lines>
           Show the context between diff hunks, up to the specified number of lines, thereby fusing hunks that are close to each other.

       --exit-code
           Make the program exit with codes similar to diff(1). That is, it exits with 1 if there were differences and 0 means no
           differences.

       --quiet
           Disable all output of the program. Implies --exit-code.

       --ext-diff
           Allow an external diff helper to be executed. If you set an external diff driver with gitattributes(5), you need to use this
           option with git-log(1) and friends.

       --no-ext-diff
           Disallow external diff drivers.

       --ignore-submodules
           Ignore changes to submodules in the diff generation.

       --src-prefix=<prefix>
           Show the given source prefix instead of "a/".

       --dst-prefix=<prefix>
           Show the given destination prefix instead of "b/".

       --no-prefix
           Do not show any source or destination prefix.

       For more detailed explanation on these common options, see also gitdiffcore(7).

       <path>...
           The <paths> parameters, when given, are used to limit the diff to the named paths (you can give directory names and get diff for
           all files under them).

## RAW OUTPUT FORMAT
       The raw output format from "git-diff-index", "git-diff-tree", "git-diff-files" and "git diff --raw" are very similar.

       These commands all compare two sets of things; what is compared differs:

       git-diff-index <tree-ish>
           compares the <tree-ish> and the files on the filesystem.

       git-diff-index --cached <tree-ish>
           compares the <tree-ish> and the index.

       git-diff-tree [-r] <tree-ish-1> <tree-ish-2> [<pattern>...]
           compares the trees named by the two arguments.

       git-diff-files [<pattern>...]
           compares the index and the files on the filesystem.

       The "git-diff-tree" command begins its output by printing the hash of what is being compared. After that, all the commands print one
       output line per changed file.

       An output line is formatted this way:

           in-place edit  :100644 100644 bcd1234... 0123456... M file0
           copy-edit      :100644 100644 abcd123... 1234567... C68 file1 file2
           rename-edit    :100644 100644 abcd123... 1234567... R86 file1 file3
           create         :000000 100644 0000000... 1234567... A file4
           delete         :100644 000000 1234567... 0000000... D file5
           unmerged       :000000 000000 0000000... 0000000... U file6

       That is, from the left to the right:

        1. a colon.

        2. mode for "src"; 000000 if creation or unmerged.

        3. a space.

        4. mode for "dst"; 000000 if deletion or unmerged.

        5. a space.

        6. sha1 for "src"; 0{40} if creation or unmerged.

        7. a space.

        8. sha1 for "dst"; 0{40} if creation, unmerged or "look at work tree".

        9. a space.

       10. status, followed by optional "score" number.

       11. a tab or a NUL when -z option is used.

       12. path for "src"

       13. a tab or a NUL when -z option is used; only exists for C or R.

       14. path for "dst"; only exists for C or R.

       15. an LF or a NUL when -z option is used, to terminate the record.

       Possible status letters are:

       ·   A: addition of a file

       ·   C: copy of a file into a new one

       ·   D: deletion of a file

       ·   M: modification of the contents or mode of a file

       ·   R: renaming of a file

       ·   T: change in the type of the file

       ·   U: file is unmerged (you must complete the merge before it can be committed)

       ·   X: "unknown" change type (most probably a bug, please report it)

       Status letters C and R are always followed by a score (denoting the percentage of similarity between the source and target of the
       move or copy), and are the only ones to be so.

       <sha1> is shown as all 0’s if a file is new on the filesystem and it is out of sync with the index.

       Example:

           :100644 100644 5be4a4...... 000000...... M file.c

       When -z option is not used, TAB, LF, and backslash characters in pathnames are represented as \t, \n, and \\, respectively.

## DIFF FORMAT FOR MERGES
       "git-diff-tree", "git-diff-files" and "git-diff --raw" can take -c or --cc option to generate diff output also for merge commits. The
       output differs from the format described above in the following way:

        1. there is a colon for each parent

        2. there are more "src" modes and "src" sha1

        3. status is concatenated status characters for each parent

        4. no optional "score" number

        5. single path, only for "dst"

       Example:

           ::100644 100644 100644 fabadb8... cc95eb0... 4866510... MM      describe.c

       Note that combined diff lists only files which were modified from all parents.

## GENERATING PATCHES WITH -P
       When "git-diff-index", "git-diff-tree", or "git-diff-files" are run with a -p option, "git diff" without the --raw option, or "git
       log" with the "-p" option, they do not produce the output described above; instead they produce a patch file. You can customize the
       creation of such patches via the GIT_EXTERNAL_DIFF and the GIT_DIFF_OPTS environment variables.

       What the -p option produces is slightly different from the traditional diff format.

        1. It is preceded with a "git diff" header, that looks like this:

               diff --git a/file1 b/file2

           The a/ and b/ filenames are the same unless rename/copy is involved. Especially, even for a creation or a deletion, /dev/null is
           not used in place of a/ or b/ filenames.

           When rename/copy is involved, file1 and file2 show the name of the source file of the rename/copy and the name of the file that
           rename/copy produces, respectively.

        2. It is followed by one or more extended header lines:

               old mode <mode>
               new mode <mode>
               deleted file mode <mode>
               new file mode <mode>
               copy from <path>
               copy to <path>
               rename from <path>
               rename to <path>
               similarity index <number>
               dissimilarity index <number>
               index <hash>..<hash> <mode>

        3. TAB, LF, double quote and backslash characters in pathnames are represented as \t, \n, \" and \\, respectively. If there is need
           for such substitution then the whole pathname is put in double quotes.

       The similarity index is the percentage of unchanged lines, and the dissimilarity index is the percentage of changed lines. It is a
       rounded down integer, followed by a percent sign. The similarity index value of 100% is thus reserved for two equal files, while 100%
       dissimilarity means that no line from the old file made it into the new one.

## COMBINED DIFF FORMAT
       "git-diff-tree", "git-diff-files" and "git-diff" can take -c or --cc option to produce combined diff. For showing a merge commit with
       "git log -p", this is the default format; you can force showing full diff with the -m option. A combined diff format looks like this:

           diff --combined describe.c
           index fabadb8,cc95eb0..4866510
           --- a/describe.c
           +++ b/describe.c
           @@@ -98,20 -98,12 +98,20 @@@
                   return (a_date > b_date) ? -1 : (a_date == b_date) ? 0 : 1;
             }

           - static void describe(char *arg)
            -static void describe(struct commit *cmit, int last_one)
           ++static void describe(char *arg, int last_one)
             {
            +      unsigned char sha1[20];
            +      struct commit *cmit;
                   struct commit_list *list;
                   static int initialized = 0;
                   struct commit_name *n;

            +      if (get_sha1(arg, sha1) < 0)
            +              usage(describe_usage);
            +      cmit = lookup_commit_reference(sha1);
            +      if (!cmit)
            +              usage(describe_usage);
            +
                   if (!initialized) {
                           initialized = 1;
                           for_each_ref(get_name);

        1. It is preceded with a "git diff" header, that looks like this (when -c option is used):

               diff --combined file

           or like this (when --cc option is used):

               diff --cc file

        2. It is followed by one or more extended header lines (this example shows a merge with two parents):

               index <hash>,<hash>..<hash>
               mode <mode>,<mode>..<mode>
               new file mode <mode>
               deleted file mode <mode>,<mode>

           The mode <mode>,<mode>..<mode> line appears only if at least one of the <mode> is different from the rest. Extended headers with
           information about detected contents movement (renames and copying detection) are designed to work with diff of two <tree-ish> and
           are not used by combined diff format.

        3. It is followed by two-line from-file/to-file header

               --- a/file
               +++ b/file

           Similar to two-line header for traditional unified diff format, /dev/null is used to signal created or deleted files.

        4. Chunk header format is modified to prevent people from accidentally feeding it to patch -p1. Combined diff format was created for
           review of merge commit changes, and was not meant for apply. The change is similar to the change in the extended index header:

               @@@ <from-file-range> <from-file-range> <to-file-range> @@@

           There are (number of parents + 1) @ characters in the chunk header for combined diff format.

       Unlike the traditional unified diff format, which shows two files A and B with a single column that has - (minus — appears in A but
       removed in B), + (plus — missing in A but added to B), or " " (space — unchanged) prefix, this format compares two or more files
       file1, file2,... with one file X, and shows how X differs from each of fileN. One column for each of fileN is prepended to the output
       line to note how X’s line is different from it.

       A - character in the column N means that the line appears in fileN but it does not appear in the result. A + character in the column
       N means that the line appears in the result, and fileN does not have that line (in other words, the line was added, from the point of
       view of that parent).

       In the above example output, the function signature was changed from both files (hence two - removals from both file1 and file2, plus
       ++ to mean one line that was added does not appear in either file1 nor file2). Also eight other lines are the same from file1 but do
       not appear in file2 (hence prefixed with +).

       When shown by git diff-tree -c, it compares the parents of a merge commit with the merge result (i.e. file1..fileN are the parents).
       When shown by git diff-files -c, it compares the two unresolved merge parents with the working tree file (i.e. file1 is stage 2 aka
       "our version", file2 is stage 3 aka "their version").

## OTHER DIFF FORMATS
       The --summary option describes newly added, deleted, renamed and copied files. The --stat option adds diffstat(1) graph to the
       output. These options can be combined with other options, such as -p, and are meant for human consumption.

       When showing a change that involves a rename or a copy, --stat output formats the pathnames compactly by combining common prefix and
       suffix of the pathnames. For example, a change that moves arch/i386/Makefile to arch/x86/Makefile while modifying 4 lines will be
       shown like this:

           arch/{i386 => x86}/Makefile    |   4 +--

       The --numstat option gives the diffstat(1) information but is designed for easier machine consumption. An entry in --numstat output
       looks like this:

           1       2       README
           3       1       arch/{i386 => x86}/Makefile

       That is, from left to right:

        1. the number of added lines;

        2. a tab;

        3. the number of deleted lines;

        4. a tab;

        5. pathname (possibly with rename/copy information);

        6. a newline.

       When -z output option is in effect, the output is formatted this way:

           1       2       README NUL
           3       1       NUL arch/i386/Makefile NUL arch/x86/Makefile NUL

       That is:

        1. the number of added lines;

        2. a tab;

        3. the number of deleted lines;

        4. a tab;

        5. a NUL (only exists if renamed/copied);

        6. pathname in preimage;

        7. a NUL (only exists if renamed/copied);

        8. pathname in postimage (only exists if renamed/copied);

        9. a NUL.

       The extra NUL before the preimage path in renamed case is to allow scripts that read the output to tell if the current record being
       read is a single-path record or a rename/copy record without reading ahead. After reading added and deleted lines, reading up to NUL
       would yield the pathname, but if that is NUL, the record will show two paths.

## EXAMPLES
       Various ways to check your working tree

               $ git diff            (1)
               $ git diff --cached   (2)
               $ git diff HEAD       (3)

           1. Changes in the working tree not yet staged for the next commit.
           2. Changes between the index and your last commit; what you would be committing if you run "git commit" without "-a" option.
           3. Changes in the working tree since your last commit; what you would be committing if you run "git commit -a"

       Comparing with arbitrary commits

               $ git diff test            (1)
               $ git diff HEAD -- ./test  (2)
               $ git diff HEAD^ HEAD      (3)

           1. Instead of using the tip of the current branch, compare with the tip of "test" branch.
           2. Instead of comparing with the tip of "test" branch, compare with the tip of the current branch, but limit the comparison to
           the file "test".
           3. Compare the version before the last commit and the last commit.

       Comparing branches

               $ git diff topic master    (1)
               $ git diff topic..master   (2)
               $ git diff topic...master  (3)

           1. Changes between the tips of the topic and the master branches.
           2. Same as above.
           3. Changes that occurred on the master branch since when the topic branch was started off it.

       Limiting the diff output

               $ git diff --diff-filter=MRC            (1)
               $ git diff --name-status                (2)
               $ git diff arch/i386 include/asm-i386   (3)

           1. Show only modification, rename and copy, but not addition nor deletion.
           2. Show only names and the nature of change, but not actual diff output.
           3. Limit diff output to named subtrees.

       Munging the diff output

               $ git diff --find-copies-harder -B -C  (1)
               $ git diff -R                          (2)

           1. Spend extra cycles to find renames, copies and complete rewrites (very expensive).
           2. Output diff in reverse.

