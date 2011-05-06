# git-post-receive-reviewboard

## Description

A quick and dirty hack to allow post commit reviews of commits to git. We currently use git with a centralized repository which several people pull and push to.
The regular post-review tool did not work very well as it did not work with bare repositories, and did not have a configurable repository path, which would have
given us some problems with doing pre commit reviews with the same repository configuration in reviewboard.

This simple hook just looks at each new ref supplied to git's post-receive hook, attempts to discover who the author is in reviewboard terms, extracts the diff,
creates a new review request with the information at hand, and publishes it. This allows us to use the same code review routines with git as the routines that
are already in place for SVN.

Note that I would be the first to admit that this is not really the ideal workflow, but changes to routines can be hard to advocate...

## Usage

Populate the variables at the top of the script with the correct values for your installation.

1.  @repo_location - should contain the absolute path to the repository you are running the hook in.

2.  @repo_path - should be the path of the repository as configured in reviewboard.

3.  @reviewboard_url - should be the url to your reviewboard instance.

4.  @reviewboard_username - should be the username of a reviewboard user *with rights to submit as other users*.

5.  @reviewboard_password - should be the password for the given user.

6.  @authors - should be a mapping between the git author email and the relevant reviewboard username. Note that if the author cannot be resolved in this hash, the commit is ignored.

## Written By

[Bjørn Øivind Bjørnsen](https://github.com/bjorn-oivind)
