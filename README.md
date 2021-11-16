# Git Knowledge Template

Use this template to create a git-knowledge repository.

## Create repos.txt file
1) Create a file called "repos.txt"
2) Put one notes repository per line in the format ```owner/repo_name```. For example, a simple file might be:

```
digitalreplica/test-notes
```

## Running GitHub actions workflow
The template has a GitHub actions workflow that:
* Iterates through all repos in the repos.txt file, and
  * Extracts tags
  * Extracts note information
  * Saves to knowledge.json file
* Downloads the digitalreplica/git-knowledge-app repo
* Publishes the git-knowledge-app and knowledge.json file into the ```gh-pages``` branch

## Configuring GitHub Pages
Once the app is published for the first time, GitHub Pages can be configured for the repository. By default, it assumes a base_href path with the same name as the repo.

1) In the repo, click ```Settings``` and then ```Pages```.
2) Under ```Source```, select the ```gh-pages``` branch.
3) Click the ```Save``` button.

The URL should be displayed at the top of the page.

## Additional workflows
There are additional GitHub Action workflows to help manage knowledge repos

### get-notes-repos.yml
This workflow lists notes repos that can be saved into the repos.txt file. By default, it looks for:
* Public repos
* With the ```notes``` topic
* For the owner of the current repo

Change the REPO_OWNER variable to look for a different user or organization

### get-notes-markdown-links.yml
This workflow makes a list of markdown links for note repos. By default, it looks for:
* Public repos
* With the ```notes``` topic
* For the owner of the current repo

It formats the repos as a list, with a markdown link to each repo and the repo description. Change the REPO_OWNER variable to look for a different user or organization

# Git-knowledge for private notes
Git-knowledge can also be used to search private notes, but takes a few extra steps to prevent the application from becoming public. This method uses Github Actions to generate the site, but doesn't publish it to GitHub Pages. You can then checkout the branch on a local computer, and open the html file for the application.

1) Use this template to create a new repo, but set the repo to private.
2) Create a [Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token). Give it ```repo``` access, so it can access private repositories.
3) Add the token as a [repository encrypted secret](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository). Note the name to use later.
4) Edit .github/workflows/deploy-github-pages.yml
5) Change ```GH_PAGES_BRANCH``` from ```gh-pages``` to anything else, like ```knowledge``` or ```deploy```. This prevents creating the GitHub Pages site. 
6) Change ```APP_BASE_HREF``` to ```./``` so the application works locally.
7) Under the ```Create knowledge.json file``` step, change ```repo-token``` to ```'${{ secrets.YOUR_SECRET_NAME }}'```, changing YOUR_SECRET_NAME to the name of your secret.
8) Commit the file.
9) Under the ```Actions``` tab, make sure the ```Deploy to GitHub Pages``` action completes successfully.
10) Add private repos into the ```repos.txt``` file. Check actions again to make sure it completes sucessfully.
11) Clone the repo to your local workstation. Check out the GH_PAGES_BRANCH branch.
12) Open ```index.html``` in a browser.

If you have the GitHub CLI installed, here's a command to find all notes repositories (public and private). It assumes you've given your notes repo the topic ```notes```. Change ```GITHUB_USERNAME``` to your GitHub username.

```gh repo list GITHUB_USERNAME --topic notes --json nameWithOwner --jq '.[]|.nameWithOwner' | sort```

# Known Issues
* When using this repo as a template, there's no easy way to incorporate changes into the new repo
