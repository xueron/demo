== NAME
       git-clone - Clone a repository into a new directory

== SYNOPSIS
       git clone [--template=<template_directory>]
                 [-l] [-s] [--no-hardlinks] [-q] [-n] [--bare] [--mirror]
                 [-o <name>] [-b <name>] [-u <upload-pack>] [--reference <repository>]
                 [--depth <depth>] [--recursive] [--] <repository> [<directory>]

== DESCRIPTION
       Clones a repository into a newly created directory, creates remote-tracking branches for each branch in the cloned repository
       (visible using git branch -r), and creates and checks out an initial branch that is forked from the cloned repository’s currently
       active branch.

       After the clone, a plain git fetch without arguments will update all the remote-tracking branches, and a git pull without arguments
       will in addition merge the remote master branch into the current master branch, if any.

       This default configuration is achieved by creating references to the remote branch heads under refs/remotes/origin and by
       initializing remote.origin.url and remote.origin.fetch configuration variables.

== OPTIONS
       --local, -l
           When the repository to clone from is on a local machine, this flag bypasses the normal "git aware" transport mechanism and clones
           the repository by making a copy of HEAD and everything under objects and refs directories. The files under .git/objects/
           directory are hardlinked to save space when possible. This is now the default when the source repository is specified with
           /path/to/repo syntax, so it essentially is a no-op option. To force copying instead of hardlinking (which may be desirable if you
           are trying to make a back-up of your repository), but still avoid the usual "git aware" transport mechanism, --no-hardlinks can
           be used.

       --no-hardlinks
           Optimize the cloning process from a repository on a local filesystem by copying files under .git/objects directory.

       --shared, -s
           When the repository to clone is on the local machine, instead of using hard links, automatically setup
           .git/objects/info/alternates to share the objects with the source repository. The resulting repository starts out without any
           object of its own.

           NOTE: this is a possibly dangerous operation; do not use it unless you understand what it does. If you clone your repository
           using this option and then delete branches (or use any other git command that makes any existing commit unreferenced) in the
           source repository, some objects may become unreferenced (or dangling). These objects may be removed by normal git operations
           (such as git commit) which automatically call git gc --auto. (See git-gc(1).) If these objects are removed and were referenced by
           the cloned repository, then the cloned repository will become corrupt.

           Note that running git repack without the -l option in a repository cloned with -s will copy objects from the source repository
           into a pack in the cloned repository, removing the disk space savings of clone -s. It is safe, however, to run git gc, which uses
           the -l option by default.

           If you want to break the dependency of a repository cloned with -s on its source repository, you can simply run git repack -a to
           copy all objects from the source repository into a pack in the cloned repository.

       --reference <repository>
           If the reference repository is on the local machine, automatically setup .git/objects/info/alternates to obtain objects from the
           reference repository. Using an already existing repository as an alternate will require fewer objects to be copied from the
           repository being cloned, reducing network and local storage costs.

           NOTE: see the NOTE for the --shared option.

       --quiet, -q
           Operate quietly. Progress is not reported to the standard error stream. This flag is also passed to the ‘rsync’ command when
           given.

       --verbose, -v
           Run verbosely. Does not affect the reporting of progress status to the standard error stream.

       --progress
           Progress status is reported on the standard error stream by default when it is attached to a terminal, unless -q is specified.
           This flag forces progress status even if the standard error stream is not directed to a terminal.

       --no-checkout, -n
           No checkout of HEAD is performed after the clone is complete.

       --bare
           Make a bare GIT repository. That is, instead of creating <directory> and placing the administrative files in <directory>/.git,
           make the <directory> itself the $GIT_DIR. This obviously implies the -n because there is nowhere to check out the working tree.
           Also the branch heads at the remote are copied directly to corresponding local branch heads, without mapping them to
           refs/remotes/origin/. When this option is used, neither remote-tracking branches nor the related configuration variables are
           created.

       --mirror
           Set up a mirror of the remote repository. This implies --bare.

       --origin <name>, -o <name>
           Instead of using the remote name origin to keep track of the upstream repository, use <name>.

       --branch <name>, -b <name>
           Instead of pointing the newly created HEAD to the branch pointed to by the cloned repository’s HEAD, point to <name> branch
           instead. In a non-bare repository, this is the branch that will be checked out.

       --upload-pack <upload-pack>, -u <upload-pack>
           When given, and the repository to clone from is accessed via ssh, this specifies a non-default path for the command run on the
           other end.

       --template=<template_directory>
           Specify the directory from which templates will be used; (See the "TEMPLATE DIRECTORY" section of git-init(1).)

       --depth <depth>
           Create a shallow clone with a history truncated to the specified number of revisions. A shallow repository has a number of
           limitations (you cannot clone or fetch from it, nor push from nor into it), but is adequate if you are only interested in the
           recent history of a large project with a long history, and would want to send in fixes as patches.

       --recursive
           After the clone is created, initialize all submodules within, using their default settings. This is equivalent to running git
           submodule update --init --recursive immediately after the clone is finished. This option is ignored if the cloned repository does
           not have a worktree/checkout (i.e. if any of --no-checkout/-n, --bare, or --mirror is given)

       <repository>
           The (possibly remote) repository to clone from. See the URLS section below for more information on specifying repositories.

       <directory>
           The name of a new directory to clone into. The "humanish" part of the source repository is used if no directory is explicitly
           given (repo for /path/to/repo.git and foo for host.xz:foo/.git). Cloning into an existing directory is only allowed if the
           directory is empty.

== GIT URLS
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

       These two syntaxes are mostly equivalent, except the former implies --local option.

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

== EXAMPLES
       ·   Clone from upstream:

               $ git clone git://git.kernel.org/pub/scm/.../linux-2.6 my2.6
               $ cd my2.6
               $ make

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

== EXAMPLES
       ·   Clone from upstream:

               $ git clone git://git.kernel.org/pub/scm/.../linux-2.6 my2.6
               $ cd my2.6
               $ make

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

== EXAMPLES
       ·   Clone from upstream:

               $ git clone git://git.kernel.org/pub/scm/.../linux-2.6 my2.6
               $ cd my2.6
               $ make
