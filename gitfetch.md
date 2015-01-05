
## NAME
       git-fetch - Download objects and refs from another repository

## SYNOPSIS
       git fetch [<options>] [<repository> [<refspec>...]]

       git fetch [<options>] <group>

       git fetch --multiple [<options>] [<repository> | <group>]...

       git fetch --all [<options>]

## DESCRIPTION
       Fetches named heads or tags from one or more other repositories, along with the objects necessary to complete them.

       The ref names and their object names of fetched refs are stored in .git/FETCH_HEAD. This information is left for a later merge
       operation done by git merge.

       When <refspec> stores the fetched result in tracking branches, the tags that point at these branches are automatically followed. This
       is done by first fetching from the remote using the given <refspec>s, and if the repository has objects that are pointed by remote
       tags that it does not yet have, then fetch those missing tags. If the other end has tags that point at branches you are not
       interested in, you will not get them.

       git fetch can fetch from either a single named repository, or or from several repositories at once if <group> is given and there is a
       remotes.<group> entry in the configuration file. (See git-config(1)).

## OPTIONS
       --all
           Fetch all remotes.

       -a, --append
           Append ref names and object names of fetched refs to the existing contents of .git/FETCH_HEAD. Without this option old data in
           .git/FETCH_HEAD will be overwritten.

       --depth=<depth>
           Deepen the history of a shallow repository created by git clone with --depth=<depth> option (see git-clone(1)) by the specified
           number of commits.

       --dry-run
           Show what would be done, without making any changes.

       -f, --force
           When git fetch is used with <rbranch>:<lbranch> refspec, it refuses to update the local branch <lbranch> unless the remote branch
           <rbranch> it fetches is a descendant of <lbranch>. This option overrides that check.

       -k, --keep
           Keep downloaded pack.

       --multiple
           Allow several <repository> and <group> arguments to be specified. No <refspec>s may be specified.

       --prune
           After fetching, remove any remote tracking branches which no longer exist on the remote.

       -n, --no-tags
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

       -q, --quiet
           Pass --quiet to git-fetch-pack and silence any other internally used git commands. Progress is not reported to the standard error
           stream.

       -v, --verbose
           Be verbose.

       --progress
           Progress status is reported on the standard error stream by default when it is attached to a terminal, unless -q is specified.
           This flag forces progress status even if the standard error stream is not directed to a terminal.

       <repository>
           The "remote" repository that is the source of a fetch or pull operation. This parameter can be either a URL (see the section GIT
           URLS below) or the name of a remote (see the section REMOTES below).

       <group>
           A name referring to a list of repositories as the value of remotes.<group> in the configuration file. (See git-config(1)).

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

## EXAMPLES
       ·   Update the remote-tracking branches:

               $ git fetch origin

           The above command copies all branches from the remote refs/heads/ namespace and stores them to the local refs/remotes/origin/
           namespace, unless the branch.<name>.fetch option is used to specify a non-default refspec.

       ·   Using refspecs explicitly:

               $ git fetch origin +pu:pu maint:tmp

           This updates (or creates, as necessary) branches pu and tmp in the local repository by fetching from the branches (respectively)
           pu and maint from the remote repository.

           The pu branch will be updated even if it is does not fast-forward, because it is prefixed with a plus sign; tmp will not be.
