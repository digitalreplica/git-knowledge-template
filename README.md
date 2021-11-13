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
