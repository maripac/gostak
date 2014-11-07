Readme file for git jekyll site

Readme file for git jekyll site
Build site in master branch as normal. 
When ready to push, I understand there is a remote origin repository in GitHub already added to tracking your master branch with the source files that jekyll uses to build your site.
But since those files cannot be pushed to gh-pages we need to create a separate branch that will capture the current state of our master branch so `git add .` then `git commit -m 'meaningfull label for commit'` to update changes to your local master branch. Now `git branch src` and move to the new branch `git checkout src`. At this point we are ready to `jek deploy`.
Now our local and remote master branches are missing some files, the ones jekyll needs to build the site, but not those that the server needs to run your site. Anyway the missing files are kept in the src branch. The gh-pages branch can be created from the GitHub repository interface, there is no need to keep that one locally. To update changes from the GitHub repository graphic interface I'm not sure... delete and create? 
But maybe from your local master branch is better. `git push -f origin master:gh-pages`