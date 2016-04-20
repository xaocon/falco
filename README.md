# Sysdig website

This repository contains the source code of www.sysdig.org.


### Workflow

The production website is accessible at http://www.sysdig.org.

Changes are first applied to the staging website (http://staging.sysdig.org) and then applied to production.

1. Use the repository [**sysdig-website-staging**](https://github.com/draios/sysdig-website-staging) (branch **gh-pages**) to change staging website
1. Verify changes at http://staging.sysdig.org/
1. Once changes are definitive, merge **sysdig-website-staging#gh-pages** to **draios.github.io#master**

More details to follow.


### Requirements
* Ruby
* Rubygems
* Jekyll

### Testing
Just run ```jekyll serve --watch``` inside the repository. It will start a webserver on 0.0.0.0:4000 and will wait for file changes, no need to re-run when you modify something, just hit refresh.

### Deploy - to staging
Just push the changes back here and they will be live in a second.

### Deploy - from staging to production

In the staging repository:
* Add as a new remote the production repo (you have to do this only the first time):
```
git remote add production git@github.com:draios/draios.github.io.git
```
* Once you've made all the commits, pull the latest changes from the production with ```git pull production master --rebase``` (the ```rebase``` option is to apply all these new commits in the staging repo **on top** of the production history) for a direct merge (you'll have to edit the CNAME file when you're done), or do the same cherry-picking process as below, with staging and production inverted
* At this point, push from the staging repo. (```git push```)

In the production repository:
* Add the staging repo remote:
```
git remote add staging git@github.com:draios/sysdig-website-staging.git
```
* Fetch the new changes from the staging with ```git fetch staging gh-pages```
* Now two choices:
  - ```git merge staging``` if you want an undiscriminated merge (but then you'll have to edit the CNAME file to point to the right domain) - not suggested
  - ```git cherry-pick <first-commit>..<last commit>``` to apply only the chosen commits (of course ```git cherry-pick <commit hash>``` for a single commit)


### Wiki crawler
The wiki subsection is autogenerated by crawling the content of the [wiki](https://github.com/draios/sysdig/wiki). Do ***not*** edit content under the `wiki` folder because it will be replaced by the crawler.

For transfering all the wiki content to the sysdig website just run ```ruby update-wiki.rb``` and push the changes.

##### Requirements
* ruby 1.8 or 1.9
* libxml2
* libxml2-dev
* libxslt
* libxslt-dev
* [nokogiri](http://nokogiri.org/)
