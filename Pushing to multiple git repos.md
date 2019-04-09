## Push to multiple repositories. 

### Configure your local repo

Create an alias called origin to your main remote repository for example GitLab

* git remote add origin git@gitlab.com:namespace/repo.git

Then add push URLs for all needs repositories

* git remote set-url --add --push origin git@gitlab.com:namespace/repo.git
* git remote set-url --add --push origin git@bitbucket.org:namespace/repo.git

> These commands will add push URLs for GitLab and BitBucket, although GitLab is already set up as a remote repository.

Or if you prefer, you can make the changes directly in you repo file confuguration "./git/config" 

```
  [remote "origin"]
      url = git@gitlab.com:namespace/repo.git
      fetch = +refs/heads/*:refs/remotes/origin/*
      pushurl = git@gitlab.com:namespace/repo.git
      pushurl = git@bitbucket.org:namespace/repo.git
```

### Pushing & pulling

* git push --all -u
> will push all your local branches and set up tracking.
