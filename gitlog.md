## NAME
       git-log - Show commit logs

## SYNOPSIS
       git log [<options>] [<since>..<until>] [[--] <path>...]

## DESCRIPTION
       Shows the commit logs.

       The command takes options applicable to the git rev-list command to control what is shown and how, and options applicable to the git
       diff-* commands to control how the changes each commit introduces are shown.

## OPTIONS
       -p, -u
           Generate patch (see section on generating patches).

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
           Separate the commits with NULs instead of with new newlines.

           Also, when --raw or --numstat has been given, do not munge pathnames and use NULs as output field terminators.

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

       -<n>
           Limits the number of commits to show.

       <since>..<until>
           Show only commits between the named two commits. When either <since> or <until> is omitted, it defaults to HEAD, i.e. the tip of
           the current branch. For a more complete list of ways to spell <since> and <until>, see "SPECIFYING REVISIONS" section in git-rev-
           parse(1).

       --decorate[=short|full]
           Print out the ref names of any commits that are shown. If short is specified, the ref name prefixes refs/heads/, refs/tags/ and
           refs/remotes/ will not be printed. If full is specified, the full ref name (including prefix) will be printed. The default option
           is short.

       --source
           Print out the ref name given on the command line by which each commit was reached.

       --full-diff
           Without this flag, "git log -p <path>..." shows commits that touch the specified paths, and diffs about the same specified paths.
           With this, the full diff is shown for commits that touch the specified paths; this means that "<path>..." limits only commits,
           and doesn’t limit diff for those commits.

       --follow
           Continue listing the history of a file beyond renames.

       --log-size
           Before the log message print out its size in bytes. Intended mainly for porcelain tools consumption. If git is unable to produce
           a valid value size is set to zero. Note that only message is considered, if also a diff is shown its size is not included.

       [--] <path>...
           Show only commits that affect any of the specified paths. To prevent confusion with options and branch names, paths may need to
           be prefixed with "-- " to separate them from options or refnames.

   Commit Formatting
       --pretty[=<format>], --format[=<format>]
           Pretty-print the contents of the commit logs in a given format, where <format> can be one of oneline, short, medium, full,
           fuller, email, raw and format:<string>. When omitted, the format defaults to medium.

           Note: you can specify the default pretty format in the repository configuration (see git-config(1)).

       --abbrev-commit
           Instead of showing the full 40-byte hexadecimal commit object name, show only a partial prefix. Non default number of digits can
           be specified with "--abbrev=<n>" (which also modifies diff output, if it is displayed).

           This should make "--pretty=oneline" a whole lot more readable for people using 80-column terminals.

       --oneline
           This is a shorthand for "--pretty=oneline --abbrev-commit" used together.

       --encoding[=<encoding>]
           The commit objects record the encoding used for the log message in their encoding header; this option can be used to tell the
           command to re-code the commit log message in the encoding preferred by the user. For non plumbing commands this defaults to
           UTF-8.

       --no-notes, --show-notes[=<ref>]
           Show the notes (see git-notes(1)) that annotate the commit, when showing the commit log message. This is the default for git log,
           git show and git whatchanged commands when there is no --pretty, --format nor --oneline option is given on the command line.

           With an optional argument, add this ref to the list of notes. The ref is taken to be in refs/notes/ if it is not qualified.

       --[no-]standard-notes
           Enable or disable populating the notes ref list from the core.notesRef and notes.displayRef variables (or corresponding
           environment overrides). Enabled by default. See git-config(1).

       --relative-date
           Synonym for --date=relative.

       --date={relative,local,default,iso,rfc,short,raw}
           Only takes effect for dates shown in human-readable format, such as when using "--pretty".  log.date config variable sets a
           default value for log command’s --date option.

           --date=relative shows dates relative to the current time, e.g. "2 hours ago".

           --date=local shows timestamps in user’s local timezone.

           --date=iso (or --date=iso8601) shows timestamps in ISO 8601 format.

           --date=rfc (or --date=rfc2822) shows timestamps in RFC 2822 format, often found in E-mail messages.

           --date=short shows only date but not time, in YYYY-MM-DD format.

           --date=raw shows the date in the internal raw git format %s %z format.

           --date=default shows timestamps in the original timezone (either committer’s or author’s).

       --parents
           Print the parents of the commit. Also enables parent rewriting, see History Simplification below.

       --children
           Print the children of the commit. Also enables parent rewriting, see History Simplification below.

       --left-right
           Mark which side of a symmetric diff a commit is reachable from. Commits from the left side are prefixed with < and those from the
           right with >. If combined with --boundary, those commits are prefixed with -.

           For example, if you have this topology:

                            y---b---b  branch B
                           / \ /
                          /   .
                         /   / \
                        o---x---a---a  branch A

           you would get an output like this:

                       $ git rev-list --left-right --boundary --pretty=oneline A...B

                       >bbbbbbb... 3rd on b
                       >bbbbbbb... 2nd on b
                       <aaaaaaa... 3rd on a
                       <aaaaaaa... 2nd on a
                       -yyyyyyy... 1st on b
                       -xxxxxxx... 1st on a

       --graph
           Draw a text-based graphical representation of the commit history on the left hand side of the output. This may cause extra lines
           to be printed in between commits, in order for the graph history to be drawn properly.

           This implies the --topo-order option by default, but the --date-order option may also be specified.

   Diff Formatting
       Below are listed options that control the formatting of diff output. Some of them are specific to git-rev-list(1), however other diff
       options may be given. See git-diff-files(1) for more options.

       -c
           With this option, diff output for a merge commit shows the differences from each of the parents to the merge result
           simultaneously instead of showing pairwise diff between a parent and the result one at a time. Furthermore, it lists only files
           which were modified from all parents.

       --cc
           This flag implies the -c options and further compresses the patch output by omitting uninteresting hunks whose contents in the
           parents have only two variants and the merge result picks one of them without modification.

       -m
           This flag makes the merge commits show the full diff like regular commits; for each merge parent, a separate log entry and diff
           is generated. An exception is that only diff against the first parent is shown when --first-parent option is given; in that case,
           the output represents the changes the merge brought into the then-current branch.

       -r
           Show recursive diffs.

       -t
           Show the tree objects in the diff output. This implies -r.

   Commit Limiting
       Besides specifying a range of commits that should be listed using the special notations explained in the description, additional
       commit limiting may be applied.

       -n number, --max-count=<number>
           Limit the number of commits output.

       --skip=<number>
           Skip number commits before starting to show the commit output.

       --since=<date>, --after=<date>
           Show commits more recent than a specific date.

       --until=<date>, --before=<date>
           Show commits older than a specific date.

       --author=<pattern>, --committer=<pattern>
           Limit the commits output to ones with author/committer header lines that match the specified pattern (regular expression).

       --grep=<pattern>
           Limit the commits output to ones with log message that matches the specified pattern (regular expression).

       --all-match
           Limit the commits output to ones that match all given --grep, --author and --committer instead of ones that match at least one.

       -i, --regexp-ignore-case
           Match the regexp limiting patterns without regard to letters case.

       -E, --extended-regexp
           Consider the limiting patterns to be extended regular expressions instead of the default basic regular expressions.

       -F, --fixed-strings
           Consider the limiting patterns to be fixed strings (don’t interpret pattern as a regular expression).

       --remove-empty
           Stop when a given path disappears from the tree.

       --merges
           Print only merge commits.

       --no-merges
           Do not print commits with more than one parent.

       --first-parent
           Follow only the first parent commit upon seeing a merge commit. This option can give a better overview when viewing the evolution
           of a particular topic branch, because merges into a topic branch tend to be only about adjusting to updated upstream from time to
           time, and this option allows you to ignore the individual commits brought in to your history by such a merge.

       --not
           Reverses the meaning of the ^ prefix (or lack thereof) for all following revision specifiers, up to the next --not.

       --all
           Pretend as if all the refs in refs/ are listed on the command line as <commit>.

       --branches[=pattern]
           Pretend as if all the refs in refs/heads are listed on the command line as <commit>. If pattern is given, limit branches to ones
           matching given shell glob. If pattern lacks ?, , or [, / at the end is implied.

       --tags[=pattern]
           Pretend as if all the refs in refs/tags are listed on the command line as <commit>. If pattern is given, limit tags to ones
           matching given shell glob. If pattern lacks ?, , or [, / at the end is implied.

       --remotes[=pattern]
           Pretend as if all the refs in refs/remotes are listed on the command line as <commit>. If ‘pattern‘is given, limit remote
           tracking branches to ones matching given shell glob. If pattern lacks ?, , or [, / at the end is implied.

       --glob=glob-pattern
           Pretend as if all the refs matching shell glob glob-pattern are listed on the command line as <commit>. Leading refs/, is
           automatically prepended if missing. If pattern lacks ?, , or [, / at the end is implied.

       --bisect
           Pretend as if the bad bisection ref refs/bisect/bad was listed and as if it was followed by --not and the good bisection refs
           refs/bisect/good-* on the command line.

       --stdin
           In addition to the <commit> listed on the command line, read them from the standard input. If a -- separator is seen, stop
           reading commits and start reading paths to limit the result.

       --cherry-pick
           Omit any commit that introduces the same change as another commit on the "other side" when the set of commits are limited with
           symmetric difference.

           For example, if you have two branches, A and B, a usual way to list all commits on only one side of them is with --left-right,
           like the example above in the description of that option. It however shows the commits that were cherry-picked from the other
           branch (for example, "3rd on b" may be cherry-picked from branch A). With this option, such pairs of commits are excluded from
           the output.

       -g, --walk-reflogs
           Instead of walking the commit ancestry chain, walk reflog entries from the most recent one to older ones. When this option is
           used you cannot specify commits to exclude (that is, ^commit, commit1..commit2, nor commit1...commit2 notations cannot be used).

           With --pretty format other than oneline (for obvious reasons), this causes the output to have two extra lines of information
           taken from the reflog. By default, commit@{Nth} notation is used in the output. When the starting commit is specified as
           commit@{now}, output also uses commit@{timestamp} notation instead. Under --pretty=oneline, the commit message is prefixed with
           this information on the same line. This option cannot be combined with --reverse. See also git-reflog(1).
       --merge
           After a failed merge, show refs that touch files having a conflict and don’t exist on all heads to merge.

       --boundary
           Output uninteresting commits at the boundary, which are usually not shown.

   History Simplification
       Sometimes you are only interested in parts of the history, for example the commits modifying a particular <path>. But there are two
       parts of History Simplification, one part is selecting the commits and the other is how to do it, as there are various strategies to
       simplify the history.

       The following options select the commits to be shown:

       <paths>
           Commits modifying the given <paths> are selected.

       --simplify-by-decoration
           Commits that are referred by some branch or tag are selected.

       Note that extra commits can be shown to give a meaningful history.

       The following options affect the way the simplification is performed:

       Default mode
           Simplifies the history to the simplest history explaining the final state of the tree. Simplest because it prunes some side
           branches if the end result is the same (i.e. merging branches with the same content)

       --full-history
           As the default mode but does not prune some history.

       --dense
           Only the selected commits are shown, plus some to have a meaningful history.

       --sparse
           All commits in the simplified history are shown.

       --simplify-merges
           Additional option to --full-history to remove some needless merges from the resulting history, as there are no selected commits
           contributing to this merge.

       A more detailed explanation follows.

       Suppose you specified foo as the <paths>. We shall call commits that modify foo !TREESAME, and the rest TREESAME. (In a diff filtered
       for foo, they look different and equal, respectively.)

       In the following, we will always refer to the same example history to illustrate the differences between simplification settings. We
       assume that you are filtering for a file foo in this commit graph:

                     .-A---M---N---O---P
                    /     /   /   /   /
                   I     B   C   D   E
                    \   /   /   /   /
                     ‘-------------´

       The horizontal line of history A—P is taken to be the first parent of each merge. The commits are:

       ·    I is the initial commit, in which foo exists with contents "asdf", and a file quux exists with contents "quux". Initial commits
           are compared to an empty tree, so I is !TREESAME.

       ·   In A, foo contains just "foo".

       ·    B contains the same change as A. Its merge M is trivial and hence TREESAME to all parents.

       ·    C does not change foo, but its merge N changes it to "foobar", so it is not TREESAME to any parent.

       ·    D sets foo to "baz". Its merge O combines the strings from N and D to "foobarbaz"; i.e., it is not TREESAME to any parent.

       ·    E changes quux to "xyzzy", and its merge P combines the strings to "quux xyzzy". Despite appearing interesting, P is TREESAME to
           all parents.

       rev-list walks backwards through history, including or excluding commits based on whether --full-history and/or parent rewriting (via
       --parents or --children) are used. The following settings are available.

       Default mode
           Commits are included if they are not TREESAME to any parent (though this can be changed, see --sparse below). If the commit was a
           merge, and it was TREESAME to one parent, follow only that parent. (Even if there are several TREESAME parents, follow only one
           of them.) Otherwise, follow all parents.

           This results in:

                         .-A---N---O
                        /         /
                       I---------D

           Note how the rule to only follow the TREESAME parent, if one is available, removed B from consideration entirely.  C was
           considered via N, but is TREESAME. Root commits are compared to an empty tree, so I is !TREESAME.

           Parent/child relations are only visible with --parents, but that does not affect the commits selected in default mode, so we have
           shown the parent lines.

       --full-history without parent rewriting
           This mode differs from the default in one point: always follow all parents of a merge, even if it is TREESAME to one of them.
           Even if more than one side of the merge has commits that are included, this does not imply that the merge itself is! In the
           example, we get

                       I  A  B  N  D  O

           P and M were excluded because they are TREESAME to a parent.  E, C and B were all walked, but only B was !TREESAME, so the others
           do not appear.

           Note that without parent rewriting, it is not really possible to talk about the parent/child relationships between the commits,
           so we show them disconnected.

       --full-history with parent rewriting
           Ordinary commits are only included if they are !TREESAME (though this can be changed, see --sparse below).

           Merges are always included. However, their parent list is rewritten: Along each parent, prune away commits that are not included
           themselves. This results in

                         .-A---M---N---O---P
                        /     /   /   /   /
                       I     B   /   D   /
                        \   /   /   /   /
                         ‘-------------´

           Compare to --full-history without rewriting above. Note that E was pruned away because it is TREESAME, but the parent list of P
           was rewritten to contain E´s parent I. The same happened for C and N. Note also that P was included despite being TREESAME.

       In addition to the above settings, you can change whether TREESAME affects inclusion:

       --dense
           Commits that are walked are included if they are not TREESAME to any parent.

       --sparse
           All commits that are walked are included.

           Note that without --full-history, this still simplifies merges: if one of the parents is TREESAME, we follow only that one, so
           the other sides of the merge are never walked.

       Finally, there is a fourth simplification mode available:

       --simplify-merges
           First, build a history graph in the same way that --full-history with parent rewriting does (see above).

           Then simplify each commit ‘C‘ to its replacement C’ in the final history according to the following rules:

           ·   Set ‘C’‘ to C.

           ·   Replace each parent ‘P‘ of C’ with its simplification ‘P’‘. In the process, drop parents that are ancestors of other parents,
               and remove duplicates.

           ·   If after this parent rewriting, ‘C’‘ is a root or merge commit (has zero or >1 parents), a boundary commit, or !TREESAME, it
               remains. Otherwise, it is replaced with its only parent.
               The effect of this is best shown by way of comparing to --full-history with parent rewriting. The example turns into:

                             .-A---M---N---O
                            /     /       /
                           I     B       D
                            \   /       /
                             ‘---------´

               Note the major differences in N and P over --full-history:

               ·    N´s parent list had I removed, because it is an ancestor of the other parent M. Still, N remained because it is
                   !TREESAME.

               ·    P´s parent list similarly had I removed.  P was then removed completely, because it had one parent and is TREESAME.

           The --simplify-by-decoration option allows you to view only the big picture of the topology of the history, by omitting commits
           that are not referenced by tags. Commits are marked as !TREESAME (in other words, kept after history simplification rules
           described above) if (1) they are referenced by tags, or (2) they change the contents of the paths given on the command line. All
           other commits are marked as TREESAME (subject to be simplified away).

   Commit Ordering
       By default, the commits are shown in reverse chronological order.

       --topo-order
           This option makes them appear in topological order (i.e. descendant commits are shown before their parents).

       --date-order
           This option is similar to --topo-order in the sense that no parent comes before all of its children, but otherwise things are
           still ordered in the commit timestamp order.

       --reverse
           Output the commits in reverse order. Cannot be combined with --walk-reflogs.

   Object Traversal
       These options are mostly targeted for packing of git repositories.

       --objects
           Print the object IDs of any object referenced by the listed commits.  --objects foo ^bar thus means "send me all object IDs which
           I need to download if I have the commit object bar, but not foo".

       --objects-edge
           Similar to --objects, but also print the IDs of excluded commits prefixed with a "-" character. This is used by git-pack-
           objects(1) to build "thin" pack, which records objects in deltified form based on objects contained in these excluded commits to
           reduce network traffic.

       --unpacked
           Only useful with --objects; print the object IDs that are not in packs.

       --no-walk
           Only show the given revs, but do not traverse their ancestors.

       --do-walk
           Overrides a previous --no-walk.

## PRETTY FORMATS
       If the commit is a merge, and if the pretty-format is not oneline, email or raw, an additional line is inserted before the Author:
       line. This line begins with "Merge: " and the sha1s of ancestral commits are printed, separated by spaces. Note that the listed
       commits may not necessarily be the list of the direct parent commits if you have limited your view of history: for example, if you
       are only interested in changes related to a certain directory or file.

       Here are some additional details for each format:

       ·    oneline

               <sha1> <title line>

           This is designed to be as compact as possible.

       ·    short

               commit <sha1>
               Author: <author>

               <title line>

       ·    medium

               commit <sha1>
               Author: <author>
               Date:   <author date>

               <title line>

               <full commit message>

       ·    full

               commit <sha1>
               Author: <author>
               Commit: <committer>

               <title line>

               <full commit message>

       ·    fuller

               commit <sha1>
               Author:     <author>
               AuthorDate: <author date>
               Commit:     <committer>
               CommitDate: <committer date>

               <title line>

               <full commit message>

       ·    email

               From <sha1> <date>
               From: <author>
               Date: <author date>
               Subject: [PATCH] <title line>

               <full commit message>

       ·    raw

           The raw format shows the entire commit exactly as stored in the commit object. Notably, the SHA1s are displayed in full,
           regardless of whether --abbrev or --no-abbrev are used, and parents information show the true parent commits, without taking
           grafts nor history simplification into account.

       ·    format:

           The format: format allows you to specify which information you want to show. It works a little bit like printf format, with the
           notable exception that you get a newline with %n instead of \n.

           E.g, format:"The author of %h was %an, %ar%nThe title was >>%s<<%n" would show something like this:

               The author of fe6e0ee was Junio C Hamano, 23 hours ago
               The title was >>t4119: test autocomputing -p<n> for traditional diff input.<<

           The placeholders are:

           ·    %H: commit hash

           ·    %h: abbreviated commit hash

           ·    %T: tree hash

           ·    %t: abbreviated tree hash

           ·    %P: parent hashes

           ·    %p: abbreviated parent hashes

           ·    %an: author name

           ·    %aN: author name (respecting .mailmap, see git-shortlog(1) or git-blame(1))

           ·    %ae: author email

           ·    %aE: author email (respecting .mailmap, see git-shortlog(1) or git-blame(1))

           ·    %ad: author date (format respects --date= option)

           ·    %aD: author date, RFC2822 style

           ·    %ar: author date, relative

           ·    %at: author date, UNIX timestamp

           ·    %ai: author date, ISO 8601 format

           ·    %cn: committer name

           ·    %cN: committer name (respecting .mailmap, see git-shortlog(1) or git-blame(1))

           ·    %ce: committer email

           ·    %cE: committer email (respecting .mailmap, see git-shortlog(1) or git-blame(1))

           ·    %cd: committer date

           ·    %cD: committer date, RFC2822 style

           ·    %cr: committer date, relative

           ·    %ct: committer date, UNIX timestamp

           ·    %ci: committer date, ISO 8601 format

           ·    %d: ref names, like the --decorate option of git-log(1)

           ·    %e: encoding

           ·    %s: subject

           ·    %f: sanitized subject line, suitable for a filename

           ·    %b: body

           ·    %N: commit notes

           ·    %gD: reflog selector, e.g., refs/stash@{1}

           ·    %gd: shortened reflog selector, e.g., stash@{1}

           ·    %gs: reflog subject

           ·    %Cred: switch color to red

           ·    %Cgreen: switch color to green

           ·    %Cblue: switch color to blue

           ·    %Creset: reset color

           ·    %C(...): color specification, as described in color.branch.* config option

           ·    %m: left, right or boundary mark

           ·    %n: newline

           ·    %%: a raw %

           ·    %x00: print a byte from a hex code

           ·    %w([<w>[,<i1>[,<i2>]]]): switch line wrapping, like the -w option of git-shortlog(1).

           Note
           Some placeholders may depend on other options given to the revision traversal engine. For example, the %g* reflog options will
           insert an empty string unless we are traversing reflog entries (e.g., by git log -g). The %d placeholder will use the "short"
           decoration format if --decorate was not already provided on the command line.

       If you add a + (plus sign) after % of a placeholder, a line-feed is inserted immediately before the expansion if and only if the
       placeholder expands to a non-empty string.

       If you add a - (minus sign) after % of a placeholder, line-feeds that immediately precede the expansion are deleted if and only if
       the placeholder expands to an empty string.

       ·    tformat:

           The tformat: format works exactly like format:, except that it provides "terminator" semantics instead of "separator" semantics.
           In other words, each commit has the message terminator character (usually a newline) appended, rather than a separator placed
           between entries. This means that the final entry of a single-line format will be properly terminated with a new line, just as the
           "oneline" format does. For example:

               $ git log -2 --pretty=format:%h 4da45bef \
                 | perl -pe ´$_ .= " -- NO NEWLINE\n" unless /\n/´
               4da45be
               7134973 -- NO NEWLINE

               $ git log -2 --pretty=tformat:%h 4da45bef \
                 | perl -pe ´$_ .= " -- NO NEWLINE\n" unless /\n/´
               4da45be
               7134973

           In addition, any unrecognized string that has a % in it is interpreted as if it has tformat: in front of it. For example, these
           two are equivalent:

               $ git log -2 --pretty=tformat:%h 4da45bef
               $ git log -2 --pretty=%h 4da45bef

## GENERATING PATCHES WITH -P
       When "git-diff-index", "git-diff-tree", or "git-diff-files" are run with a -p option, "git diff" without the --raw option, or "git
       log" with the "-p" option, they do not produce the output described above; instead they produce a patch file. You can customize the
       creation of such patches via the GIT_EXTERNAL_DIFF and the GIT_DIFF_OPTS environment variables.
           ·    %w([<w>[,<i1>[,<i2>]]]): switch line wrapping, like the -w option of git-shortlog(1).

           Note
           Some placeholders may depend on other options given to the revision traversal engine. For example, the %g* reflog options will
           insert an empty string unless we are traversing reflog entries (e.g., by git log -g). The %d placeholder will use the "short"
           decoration format if --decorate was not already provided on the command line.

       If you add a + (plus sign) after % of a placeholder, a line-feed is inserted immediately before the expansion if and only if the
       placeholder expands to a non-empty string.

       If you add a - (minus sign) after % of a placeholder, line-feeds that immediately precede the expansion are deleted if and only if
       the placeholder expands to an empty string.

       ·    tformat:

           The tformat: format works exactly like format:, except that it provides "terminator" semantics instead of "separator" semantics.
           In other words, each commit has the message terminator character (usually a newline) appended, rather than a separator placed
           between entries. This means that the final entry of a single-line format will be properly terminated with a new line, just as the
           "oneline" format does. For example:

               $ git log -2 --pretty=format:%h 4da45bef \
                 | perl -pe ´$_ .= " -- NO NEWLINE\n" unless /\n/´
               4da45be
               7134973 -- NO NEWLINE

               $ git log -2 --pretty=tformat:%h 4da45bef \
                 | perl -pe ´$_ .= " -- NO NEWLINE\n" unless /\n/´
               4da45be
               7134973

           In addition, any unrecognized string that has a % in it is interpreted as if it has tformat: in front of it. For example, these
           two are equivalent:

               $ git log -2 --pretty=tformat:%h 4da45bef
               $ git log -2 --pretty=%h 4da45bef

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

## EXAMPLES
       git log --no-merges
           Show the whole commit history, but skip any merges

       git log v2.6.12.. include/scsi drivers/scsi
           Show all commits since version v2.6.12 that changed any file in the include/scsi or drivers/scsi subdirectories

       git log --since="2 weeks ago" -- gitk
           Show the changes during the last two weeks to the file gitk. The "--" is necessary to avoid confusion with the branch named gitk

       git log --name-status release..test
           Show the commits that are in the "test" branch but not yet in the "release" branch, along with the list of paths each commit
           modifies.

       git log --follow builtin-rev-list.c
           Shows the commits that changed builtin-rev-list.c, including those commits that occurred before the file was given its present
           name.

       git log --branches --not --remotes=origin
           Shows all commits that are in any of local branches but not in any of remote tracking branches for origin (what you have that
           origin doesn’t).

       git log master --not --remotes=*/master
           Shows all commits that are in local master but not in any remote repository master branches.

       git log -p -m --first-parent
           Shows the history including change diffs, but only from the "main branch" perspective, skipping commits that come from merged
           branches, and showing full diffs of changes introduced by the merges. This makes sense only when following a strict policy of
           merging all topic branches when staying on a single integration branch.

## DISCUSSION
       At the core level, git is character encoding agnostic.

       ·   The pathnames recorded in the index and in the tree objects are treated as uninterpreted sequences of non-NUL bytes. What
           readdir(2) returns are what are recorded and compared with the data git keeps track of, which in turn are expected to be what
           lstat(2) and creat(2) accepts. There is no such thing as pathname encoding translation.

       ·   The contents of the blob objects are uninterpreted sequences of bytes. There is no encoding translation at the core level.

       ·   The commit log messages are uninterpreted sequences of non-NUL bytes.

       Although we encourage that the commit log messages are encoded in UTF-8, both the core and git Porcelain are designed not to force
       UTF-8 on projects. If all participants of a particular project find it more convenient to use legacy encodings, git does not forbid
       it. However, there are a few things to keep in mind.

        1.  git commit and git commit-tree issues a warning if the commit log message given to it does not look like a valid UTF-8 string,
           unless you explicitly say your project uses a legacy encoding. The way to say this is to have i18n.commitencoding in .git/config
           file, like this:

               [i18n]
                       commitencoding = ISO-8859-1

           Commit objects created with the above setting record the value of i18n.commitencoding in its encoding header. This is to help
           other people who look at them later. Lack of this header implies that the commit log message is encoded in UTF-8.

        2.  git log, git show, git blame and friends look at the encoding header of a commit object, and try to re-code the log message into
           UTF-8 unless otherwise specified. You can specify the desired output encoding with i18n.logoutputencoding in .git/config file,
           like this:

               [i18n]
                       logoutputencoding = ISO-8859-1

           If you do not have this configuration variable, the value of i18n.commitencoding is used instead.

       Note that we deliberately chose not to re-code the commit log message when a commit is made to force UTF-8 at the commit object
       level, because re-coding to UTF-8 is not necessarily a reversible operation.

