# Git post-receive hook for Discord

(Based on https://github.com/chriseldredge/git-slack-hook)

This is a bash script that posts a message into your [Discord](https://discordapp.com/) channel when changes are pushed.

Hook this script into `post-receive` for your git repositories.

## How to Install

Note: some git repositories may be "bare". You'll know if your repo is bare or not by checking for a `.git` folder where your repo lives.

Download [git-discord-hook](https://raw.githubusercontent.com/taketo1113/git-discord-hook/master/git-discord-hook) onto the server which hosts your git repo.

For bare repos, copy/rename it as `/path/to/your/repo/hooks/post-receive`.

For normal/non-bare repos, copy/rename it as `/path/to/your/repo/.git/hooks/post-receive`.

Finally, `chmod +x post-receive` to allow the script to be executed.

## Configuration

Add an Incoming WebHooks integration in your Discord by going to:

    System Console > Integrations > Custom Integrations

For a normal/non-bare repo, configure the webhook URL

    git config hooks.discord.webhook-url 'https://discordapp.com/api/webhooks/xxx-generatedkey-xxx/yyy-generatedkey-yyy'

For a bare repo:

    git config -f /path/to/your/repo/config hooks.discord.webhook-url 'https://discordapp.com/api/webhooks/xxx-generatedkey-xxx/yyy-generatedkey-yyy'

## Optional
Specify a channel to post in Discord instead of the default:

    git config hooks.discord.channel '#general'

        '#channelname' - post to channel
        '@username' - direct message to user
        'groupname' - post to group

Specify a username to post as. If not specified, the default name `incoming-webhook` will be used:

    git config hooks.discord.username 'git'

Specify an icon to display in Discord instead of the default:

    git config hooks.discord.icon-url 'https://example.com/icon.png'

Specify an emoji icon to display in Discord instead of the default:

    git config hooks.discord.icon-emoji ':twisted_rightwards_arrows:'

Specify a repository nice name that will be shown in messages:

    git config hooks.discord.repo-nice-name 'My Awesome Repository'

Specify whether you want to show only the last commit (or all) when pushing multiple commits:

    git config hooks.discord.show-only-last-commit true

Specify whether you want to show the body of the commit message as well as the title:

    git config hooks.discord.show-full-commit true

Specify if you want to send only certain branches:

    git config hooks.discord.branch-regexp regexp


## Linking to Changesets

When the following parameters are set, revision hashes will be turned into links to a web view of your repository.

    git config hooks.discord.repos-root '/path/to/repos'
    git config hooks.discord.changeset-url-pattern 'http://yourserver/%repo_path%/changeset/%rev_hash%'

For example, if your repository is in `/usr/local/repos/myrepo`, set repos_root to `/usr/local/repos/` and set `changeset_url_pattern` to `http://yourserver/%repo_path%/changeset/%rev_hash%` or whatever.

Links can also be created that summarize a list of commits:

    git config hooks.discord.compare-url-pattern 'http://yourserver/%repo_path%/compare/%old_rev_hash%..%new_rev_hash%'
