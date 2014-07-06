jira-git-plugin
===============

Fork of https://github.com/ilgarm/jira-git-plugin.

This fork add a JSON endpoint that can be used to retrieve the list of configured git repositories.
This is useful when automating addition and deletion of configured git repositories using this plugin.

Automated usage might look something like this:

## Adding a configured git repository

 * Clone the target git repository on the JIRA server, and set up git hooks on the  repository server
   (e.g., gitlab or gitorious) to automatically push updates to the clone on the JIRA server. This can
   be done via SSH commands.

 * Check if the repository isn't configured already to avoid creating duplicate entries.

 * Send a HTTP POST request to `[JIRASERVER]/secure/AddGitRepository.jspa` containing an appropriate
   payload.

## Deleting a configured git repository

 * Remove the clone on the JIRA server, and remove the update git hooks.
 
 * Call `[JIRASERVER]/secure/ViewGitRepositoriesJson.jspa` to retrieve a list of all configured git
   repositories, and find JIRA's internal ID for the one you want to delete.
   
 * Send a HTTP GET request to `[JIRASERVER]/secure/DeleteGitRepository.jspa?repoID=[ID]`.
 
Change `[JIRASERVER]` and `[ID]` to the relevant values.
