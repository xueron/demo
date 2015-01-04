
## NAME
       git-pull - Fetch from and merge with another repository or a local branch

## SYNOPSIS
       git pull <options> <repository> <refspec>...

## DESCRIPTION
       Runs git fetch with the given parameters, and calls git merge to merge the retrieved head(s) into the current branch. With --rebase,
       calls git rebase instead of git merge.

       Note that you can use . (current directory) as the <repository> to pull from the local repository — this is useful when merging local
       branches into the current branch.

       Also note that options meant for git pull itself and underlying git merge must be given before the options meant for git fetch.

       Warning: Running git pull (actually, the underlying git merge) with uncommitted changes is discouraged: while possible, it leaves you
       in a state that is hard to back out of in the case of a conflict.

## OPTIONS
       -q, --quiet
           This is passed to both underlying git-fetch to squelch reporting of during transfer, and underlying git-merge to squelch output
           during merging.

       -v, --verbose
           Pass --verbose to git-fetch and git-merge.

   Options related to merging
       --commit, --no-commit
           Perform the merge and commit the result. This option can be used to override --no-commit.

           With --no-commit perform the merge but pretend the merge failed and do not autocommit, to give the user a chance to inspect and
           further tweak the merge result before committing.

       --ff, --no-ff
           Do not generate a merge commit if the merge resolved as a fast-forward, only update the branch pointer. This is the default
           behavior of git-merge.

           With --no-ff Generate a merge commit even if the merge resolved as a fast-forward.

       --log, --no-log
           In addition to branch names, populate the log message with one-line descriptions from the actual commits that are being merged.

           With --no-log do not list one-line descriptions from the actual commits being merged.

       --stat, -n, --no-stat
           Show a diffstat at the end of the merge. The diffstat is also controlled by the configuration option merge.stat.

           With -n or --no-stat do not show a diffstat at the end of the merge.

       --squash, --no-squash
           Produce the working tree and index state as if a real merge happened (except for the merge information), but do not actually make
           a commit or move the HEAD, nor record $GIT_DIR/MERGE_HEAD to cause the next git commit command to create a merge commit. This
           allows you to create a single commit on top of the current branch whose effect is the same as merging another branch (or more in
           case of an octopus).

           With --no-squash perform the merge and commit the result. This option can be used to override --squash.

       --ff-only
           Refuse to merge and exit with a non-zero status unless the current HEAD is already up-to-date or the merge can be resolved as a
           fast-forward.

       -s <strategy>, --strategy=<strategy>
           Use the given merge strategy; can be supplied more than once to specify them in the order they should be tried. If there is no -s
           option, a built-in list of strategies is used instead (git merge-recursive when merging a single head, git merge-octopus
           otherwise).

       -X <option>, --strategy-option=<option>
           Pass merge strategy specific option through to the merge strategy.

       --summary, --no-summary
           Synonyms to --stat and --no-stat; these are deprecated and will be removed in the future.

       -q, --quiet
           Operate quietly.

       -v, --verbose
           Be verbose.

       --rebase
           Instead of a merge, perform a rebase after fetching. If there is a remote ref for the upstream branch, and this branch was
           rebased since last fetched, the rebase uses that information to avoid rebasing non-local changes. To make this the default for
           branch <name>, set configuration branch.<name>.rebase to true.

               Note
               This is a potentially dangerous mode of operation. It rewrites history, which does not bode well when you published that
               history already. Do not use this option unless you have read git-rebase(1) carefully.

       --no-rebase
           Override earlier --rebase.

   Options related to fetching
       --all
           Fetch all remotes.

       -a, --append
           Append ref names and object names of fetched refs to the existing contents of .git/FETCH_HEAD. Without this option old data in
           .git/FETCH_HEAD will be overwritten.

       --depth=<depth>
           Deepen the history of a shallow repository created by git clone with --depth=<depth> option (see git-clone(1)) by the specified
           number of commits.

       -f, --force
           When git fetch is used with <rbranch>:<lbranch> refspec, it refuses to update the local branch <lbranch> unless the remote branch
           <rbranch> it fetches is a descendant of <lbranch>. This option overrides that check.

       -k, --keep
           Keep downloaded pack.

       --no-tags
           By default, tags that point at objects that are downloaded from the remote repository are fetched and stored locally. This option
           disables this automatic tag following.

       -t, --tags
           Most of the tags are fetched automatically as branch heads are downloaded, but tags that do not point at objects reachable from
           the branch heads that are being tracked will not be fetched by this mechanism. This flag lets all tags and their associated
           objects be downloaded.

       -u, --update-head-ok
           By default git fetch refuses to update the head which corresponds to the current branch. This flag disables the check. This is
           purely for the internal use for git pull to communicate with git fetch, and unless you are implementing your own Porcelain you
           are not supposed to use it.

       --upload-pack <upload-pack>
           When given, and the repository to fetch from is handled by git fetch-pack, --exec=<upload-pack> is passed to the command to
           specify non-default path for the command run on the other end.

       --progress
           Progress status is reported on the standard error stream by default when it is attached to a terminal, unless -q is specified.
           This flag forces progress status even if the standard error stream is not directed to a terminal.

       <repository>
           The "remote" repository that is the source of a fetch or pull operation. This parameter can be either a URL (see the section GIT
           URLS below) or the name of a remote (see the section REMOTES below).

       <refspec>
           The format of a <refspec> parameter is an optional plus +, followed by the source ref <src>, followed by a colon :, followed by
           the destination ref <dst>.

           The remote ref that matches <src> is fetched, and if <dst> is not empty string, the local ref that matches it is fast-forwarded
           using <src>. If the optional plus + is used, the local ref is updated even if it does not result in a fast-forward update.

               Note
               If the remote branch from which you want to pull is modified in non-linear ways such as being rewound and rebased frequently,
               then a pull will attempt a merge with an older version of itself, likely conflict, and fail. It is under these conditions
               that you would want to use the + sign to indicate non-fast-forward updates will be needed. There is currently no easy way to
               determine or declare that a branch will be made available in a repository with this behavior; the pulling user simply must
               know this is the expected usage pattern for a branch.

               Note
               You never do your own development on branches that appear on the right hand side of a <refspec> colon on Pull: lines; they
               are to be updated by git fetch. If you intend to do development derived from a remote branch B, have a Pull: line to track it
               (i.e.  Pull: B:remote-B), and have a separate branch my-B to do your development on top of it. The latter is created by git
               branch my-B remote-B (or its equivalent git checkout -b my-B remote-B). Run git fetch to keep track of the progress of the
               remote side, and when you see something new on the remote branch, merge it into your development branch with git pull .
               remote-B, while you are on my-B branch.

               Note
               There is a difference between listing multiple <refspec> directly on git pull command line and having multiple Pull:
               <refspec> lines for a <repository> and running git pull command without any explicit <refspec> parameters. <refspec> listed
               explicitly on the command line are always merged into the current branch after fetching. In other words, if you list more
               than one remote refs, you would be making an Octopus. While git pull run without any explicit <refspec> parameter takes
               default <refspec>s from Pull: lines, it merges only the first <refspec> found into the current branch, after fetching all the
               remote refs. This is because making an Octopus from remote refs is rarely done, while keeping track of multiple remote heads
               in one-go by fetching more than one is often useful.
           Some short-cut notations are also supported.

           ·    tag <tag> means the same as refs/tags/<tag>:refs/tags/<tag>; it requests fetching everything up to the given tag.

           ·   A parameter <ref> without a colon is equivalent to <ref>: when pulling/fetching, so it merges <ref> into the current branch
               without storing the remote branch anywhere locally

## GIT URLS
       In general, URLs contain information about the transport protocol, the address of the remote server, and the path to the repository.
       Depending on the transport protocol, some of this information may be absent.

       Git natively supports ssh, git, http, https, ftp, ftps, and rsync protocols. The following syntaxes may be used with them:

       ·   ssh://[user@]host.xz[:port]/path/to/repo.git/

       ·   git://host.xz[:port]/path/to/repo.git/

       ·   http[s]://host.xz[:port]/path/to/repo.git/

       ·   ftp[s]://host.xz[:port]/path/to/repo.git/

       ·   rsync://host.xz/path/to/repo.git/

       An alternative scp-like syntax may also be used with the ssh protocol:

       ·   [user@]host.xz:path/to/repo.git/

       The ssh and git protocols additionally support ~username expansion:

       ·   ssh://[user@]host.xz[:port]/~[user]/path/to/repo.git/

       ·   git://host.xz[:port]/~[user]/path/to/repo.git/

       ·   [user@]host.xz:/~[user]/path/to/repo.git/

       For local respositories, also supported by git natively, the following syntaxes may be used:

       ·   /path/to/repo.git/

       ·    file:///path/to/repo.git/

       These two syntaxes are mostly equivalent, except when cloning, when the former implies --local option. See git-clone(1) for details.

       When git doesn’t know how to handle a certain transport protocol, it attempts to use the remote-<transport> remote helper, if one
       exists. To explicitly request a remote helper, the following syntax may be used:

       ·   <transport>::<address>

       where <address> may be a path, a server and path, or an arbitrary URL-like string recognized by the specific remote helper being
       invoked. See git-remote-helpers(1) for details.

       If there are a large number of similarly-named remote repositories and you want to use a different format for them (such that the
       URLs you use will be rewritten into URLs that work), you can create a configuration section of the form:

                   [url "<actual url base>"]
                           insteadOf = <other url base>

       For example, with this:

                   [url "git://git.host.xz/"]
                           insteadOf = host.xz:/path/to/
                           insteadOf = work:

       a URL like "work:repo.git" or like "host.xz:/path/to/repo.git" will be rewritten in any context that takes a URL to be
       "git://git.host.xz/repo.git".

       If you want to rewrite URLs for push only, you can create a configuration section of the form:

                   [url "<actual url base>"]
                           pushInsteadOf = <other url base>

       For example, with this:

                   [url "ssh://example.org/"]
                           pushInsteadOf = git://example.org/

       a URL like "git://example.org/path/to/repo.git" will be rewritten to "ssh://example.org/path/to/repo.git" for pushes, but pulls will
       still use the original URL.

## REMOTES
       The name of one of the following can be used instead of a URL as <repository> argument:

       ·   a remote in the git configuration file: $GIT_DIR/config,

       ·   a file in the $GIT_DIR/remotes directory, or

       ·   a file in the $GIT_DIR/branches directory.

       All of these also allow you to omit the refspec from the command line because they each contain a refspec which git will use by
       default.

   Named remote in configuration file
       You can choose to provide the name of a remote which you had previously configured using git-remote(1), git-config(1) or even by a
       manual edit to the $GIT_DIR/config file. The URL of this remote will be used to access the repository. The refspec of this remote
       will be used by default when you do not provide a refspec on the command line. The entry in the config file would appear like this:

                   [remote "<name>"]
                           url = <url>
                           pushurl = <pushurl>
                           push = <refspec>
                           fetch = <refspec>

       The <pushurl> is used for pushes only. It is optional and defaults to <url>.

   Named file in $GIT_DIR/remotes
       You can choose to provide the name of a file in $GIT_DIR/remotes. The URL in this file will be used to access the repository. The
       refspec in this file will be used as default when you do not provide a refspec on the command line. This file should have the
       following format:

                   URL: one of the above URL format
                   Push: <refspec>
                   Pull: <refspec>

       Push: lines are used by git push and Pull: lines are used by git pull and git fetch. Multiple Push: and Pull: lines may be specified
       for additional branch mappings.

   Named file in $GIT_DIR/branches
       You can choose to provide the name of a file in $GIT_DIR/branches. The URL in this file will be used to access the repository. This
       file should have the following format:

                   <url>#<head>

       <url> is required; #<head> is optional.

       Depending on the operation, git will use one of the following refspecs, if you don’t provide one on the command line. <branch> is the
       name of this file in $GIT_DIR/branches and <head> defaults to master.

       git fetch uses:

                   refs/heads/<head>:refs/heads/<branch>

       git push uses:

                   HEAD:refs/heads/<head>

## MERGE STRATEGIES
       The merge mechanism (git-merge and git-pull commands) allows the backend merge strategies to be chosen with -s option. Some
       strategies can also take their own options, which can be passed by giving -X<option> arguments to git-merge and/or git-pull.

       resolve
           This can only resolve two heads (i.e. the current branch and another branch you pulled from) using a 3-way merge algorithm. It
           tries to carefully detect criss-cross merge ambiguities and is considered generally safe and fast.

       recursive
           This can only resolve two heads using a 3-way merge algorithm. When there is more than one common ancestor that can be used for
           3-way merge, it creates a merged tree of the common ancestors and uses that as the reference tree for the 3-way merge. This has
           been reported to result in fewer merge conflicts without causing mis-merges by tests done on actual merge commits taken from
           Linux 2.6 kernel development history. Additionally this can detect and handle merges involving renames. This is the default merge
           strategy when pulling or merging one branch.

           The recursive strategy can take the following options:

           ours
               This option forces conflicting hunks to be auto-resolved cleanly by favoring our version. Changes from the other tree that do
               not conflict with our side are reflected to the merge result.

               This should not be confused with the ours merge strategy, which does not even look at what the other tree contains at all. It
               discards everything the other tree did, declaring our history contains all that happened in it.

           theirs
               This is opposite of ours.

           subtree[=path]
               This option is a more advanced form of subtree strategy, where the strategy makes a guess on how two trees must be shifted to
               match with each other when merging. Instead, the specified path is prefixed (or stripped from the beginning) to make the
               shape of two trees to match.

       octopus
           This resolves cases with more than two heads, but refuses to do a complex merge that needs manual resolution. It is primarily
           meant to be used for bundling topic branch heads together. This is the default merge strategy when pulling or merging more than
           one branch.

       ours
           This resolves any number of heads, but the resulting tree of the merge is always that of the current branch head, effectively
           ignoring all changes from all other branches. It is meant to be used to supersede old development history of side branches. Note
           that this is different from the -Xours option to the recursive merge strategy.

       subtree
           This is a modified recursive strategy. When merging trees A and B, if B corresponds to a subtree of A, B is first adjusted to
           match the tree structure of A, instead of reading the trees at the same level. This adjustment is also done to the common
           ancestor tree.

## DEFAULT BEHAVIOUR
       Often people use git pull without giving any parameter. Traditionally, this has been equivalent to saying git pull origin. However,
       when configuration branch.<name>.remote is present while on branch <name>, that value is used instead of origin.

       In order to determine what URL to use to fetch from, the value of the configuration remote.<origin>.url is consulted and if there is
       not any such variable, the value on URL: ‘ line in ‘$GIT_DIR/remotes/<origin> file is used.

       In order to determine what remote branches to fetch (and optionally store in the tracking branches) when the command is run without
       any refspec parameters on the command line, values of the configuration variable remote.<origin>.fetch are consulted, and if there
       aren’t any, $GIT_DIR/remotes/<origin> file is consulted and its ‘Pull: ‘ lines are used. In addition to the refspec formats described
       in the OPTIONS section, you can have a globbing refspec that looks like this:

           refs/heads/*:refs/remotes/origin/*

       A globbing refspec must have a non-empty RHS (i.e. must store what were fetched in tracking branches), and its LHS and RHS must end
       with /*. The above specifies that all remote branches are tracked using tracking branches in refs/remotes/origin/ hierarchy under the
       same name.

       The rule to determine which remote branch to merge after fetching is a bit involved, in order not to break backward compatibility.

       If explicit refspecs were given on the command line of git pull, they are all merged.

       When no refspec was given on the command line, then git pull uses the refspec from the configuration or $GIT_DIR/remotes/<origin>. In
       such cases, the following rules apply:

        1. If branch.<name>.merge configuration for the current branch <name> exists, that is the name of the branch at the remote site that
           is merged.

        2. If the refspec is a globbing one, nothing is merged.

        3. Otherwise the remote branch of the first refspec is merged.

## EXAMPLES
       ·   Update the remote-tracking branches for the repository you cloned from, then merge one of them into your current branch:

               $ git pull, git pull origin

           Normally the branch merged in is the HEAD of the remote repository, but the choice is determined by the branch.<name>.remote and
           branch.<name>.merge options; see git-config(1) for details.

       ·   Merge into the current branch the remote branch next:

               $ git pull origin next

           This leaves a copy of next temporarily in FETCH_HEAD, but does not update any remote-tracking branches. Using remote-tracking
           branches, the same can be done by invoking fetch and merge:

               $ git fetch origin
               $ git merge origin/next

       If you tried a pull which resulted in a complex conflicts and would want to start over, you can recover with git reset.
