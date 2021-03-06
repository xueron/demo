NAME
       git-remote - manage set of tracked repositories

       git-remote - 管理远程仓库

SYNOPSIS
       git remote [-v | --verbose]

       列出所有的远程仓库，关联过的


       git remote add [-t <branch>] [-m <master>] [-f] [--mirror] <name> <url>

       增加一个关联的远程仓库，name是一个别名，后面git push, git pull 的时候会用到


       git remote rename <old> <new>

       更名一个远程仓库


       git remote rm <name>

       删除一个远程仓库别名


       git remote set-head <name> (-a | -d | <branch>)

       git remote set-url [--push] <name> <newurl> [<oldurl>]
       git remote set-url --add [--push] <name> <newurl>
       git remote set-url --delete [--push] <name> <url>
       git remote [-v | --verbose] show [-n] <name>
       git remote prune [-n | --dry-run] <name>
       git remote [-v | --verbose] update [-p | --prune] [group | remote]...

DESCRIPTION
       Manage the set of repositories ("remotes") whose branches you track.

OPTIONS
       -v, --verbose
           Be a little more verbose and show remote url after name. NOTE: This must be placed between remote and subcommand.

COMMANDS
       With no arguments, shows a list of existing remotes. Several subcommands are available to perform operations on the remotes.

       add
           Adds a remote named <name> for the repository at <url>. The command git fetch <name> can then be used to create and update
           remote-tracking branches <name>/<branch>.

           With -f option, git fetch <name> is run immediately after the remote information is set up.

           With -t <branch> option, instead of the default glob refspec for the remote to track all branches under $GIT_DIR/remotes/<name>/,
           a refspec to track only <branch> is created. You can give more than one -t <branch> to track multiple branches without grabbing
           all branches.

           With -m <master> option, $GIT_DIR/remotes/<name>/HEAD is set up to point at remote’s <master> branch. See also the set-head
           command.

           In mirror mode, enabled with --mirror, the refs will not be stored in the refs/remotes/ namespace, but in refs/heads/. This
           option only makes sense in bare repositories. If a remote uses mirror mode, furthermore, git push will always behave as if
           --mirror was passed.

       rename
           Rename the remote named <old> to <new>. All remote tracking branches and configuration settings for the remote are updated.

           In case <old> and <new> are the same, and <old> is a file under $GIT_DIR/remotes or $GIT_DIR/branches, the remote is converted to
           the configuration file format.

       rm
           Remove the remote named <name>. All remote tracking branches and configuration settings for the remote are removed.

       set-head
           Sets or deletes the default branch ($GIT_DIR/remotes/<name>/HEAD) for the named remote. Having a default branch for a remote is
           not required, but allows the name of the remote to be specified in lieu of a specific branch. For example, if the default branch
           for origin is set to master, then origin may be specified wherever you would normally specify origin/master.

           With -d, $GIT_DIR/remotes/<name>/HEAD is deleted.

           With -a, the remote is queried to determine its HEAD, then $GIT_DIR/remotes/<name>/HEAD is set to the same branch. e.g., if the
           remote HEAD is pointed at next, "git remote set-head origin -a" will set $GIT_DIR/refs/remotes/origin/HEAD to
           refs/remotes/origin/next. This will only work if refs/remotes/origin/next already exists; if not it must be fetched first.

           Use <branch> to set $GIT_DIR/remotes/<name>/HEAD explicitly. e.g., "git remote set-head origin master" will set
           $GIT_DIR/refs/remotes/origin/HEAD to refs/remotes/origin/master. This will only work if refs/remotes/origin/master already
           exists; if not it must be fetched first.

       set-url
           Changes URL remote points to. Sets first URL remote points to matching regex <oldurl> (first URL if no <oldurl> is given) to
           <newurl>. If <oldurl> doesn’t match any URL, error occurs and nothing is changed.

           With --push, push URLs are manipulated instead of fetch URLs.

           With --add, instead of changing some URL, new URL is added.

           With --delete, instead of changing some URL, all URLs matching regex <url> are deleted. Trying to delete all non-push URLs is an
           error.

       show
           Gives some information about the remote <name>.

           With -n option, the remote heads are not queried first with git ls-remote <name>; cached information is used instead.

       prune
           Deletes all stale tracking branches under <name>. These stale branches have already been removed from the remote repository
           referenced by <name>, but are still locally available in "remotes/<name>".

           With --dry-run option, report what branches will be pruned, but do not actually prune them.

       update
           Fetch updates for a named set of remotes in the repository as defined by remotes.<group>. If a named group is not specified on
           the command line, the configuration parameter remotes.default will be used; if remotes.default is not defined, all remotes which
           do not have the configuration parameter remote.<name>.skipDefaultUpdate set to true will be updated. (See git-config(1)).

           With --prune option, prune all the remotes that are updated.

DISCUSSION
       The remote configuration is achieved using the remote.origin.url and remote.origin.fetch configuration variables. (See git-
       config(1)).

EXAMPLES
       ·   Add a new remote, fetch, and check out a branch from it

               $ git remote
               origin
               $ git branch -r
               origin/master
               $ git remote add linux-nfs git://linux-nfs.org/pub/linux/nfs-2.6.git
               $ git remote
               linux-nfs
               origin
               $ git fetch
               * refs/remotes/linux-nfs/master: storing branch ´master´ ...
                 commit: bf81b46
               $ git branch -r
               origin/master
               linux-nfs/master
               $ git checkout -b nfs linux-nfs/master
               ...

       ·   Imitate git clone but track only selected branches

               $ mkdir project.git
               $ cd project.git
               $ git init
               $ git remote add -f -t master -m master origin git://example.com/git.git/
               $ git merge origin
