Gitolite Manager
================

Manage [gitolite](https://github.com/sitaramc/gitolite) config and ssh keys.

*Currently in pre-alpha, not polished at all!*


## Installation

    $ sudo pip install gitolite-manager

or alternatively (you really should be using pip though):

    $ sudo easy_install gitolite-manager

From source:

    $ sudo python setup.py install

## Getting Started

### Prepare gitolite

Add the following line to gitolite configuration file (./gitolite-admin/conf/gitolite.conf)

    include "user_repos.conf"

By default, it'll use `./gitolite-admin` as gitolite directory.

### Add/remove repositories

    >>> import gitolite_manager
    >>> gitolite = gitolite_manager.Gitolite()
    >>> gitolite.addRepo('username', 'reponame')
    True
    >>> gitolite.getRepos()
    {'username/reponame': [('RW+', 'username')]}
    >>> gitolite.rmRepo('username', 'reponame')
    True
    >>> gitolite.getRepos()
    {}



### Add/remove ssh keys
This is for new style user keys.  Old style keys are supported, but not encouraged.
(Refer to http://gitolite.com/gitolite/gitolite.html#users)

    >>> import gitolite_manager
    >>> gitolite = gitolite_manager.Gitolite()
    >>> gitolite.addSSHKey('username', 'keyname', 'ssh key content') # Old style user key 
    True
    >>> gitolite.addSSHKey('username', 'ssh key content') # New style user key
    True
    >>> gitolite.getSSHKeys()
    {'username': ['keypath']}
    >>> gitolite.rmSSHKey('username','keypath')
    True
    >>> gitolite.getSSHKeys()
    {}

#### Breaking Change in User/SSHKey API
*`gitolite.*SSHKey()` break compatibility with old code*. In the new code, the keyname is no longer used. Instead full paths of the keys are used.

In the future, this hopefully will be fixed to support both old and new style user management.
