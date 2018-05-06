# Slack Cleaner

Programmatically delete all messages and files in a Slack channel

### Docker run

```shell
$ docker run --rm pam79/slack-cleaner
```

### Append Alias in (.bashrc or .zshrc) config file

```shell
alias slack-cleaner='docker run --rm pam79/slack-cleaner'
```

### Usage

>After the task, a backup file `slack-cleaner.<timestamp>.log` will be created in current directory if `--log` is supplied.


#### Delete all messages from a channel
    slack-cleaner --token <TOKEN> --message --channel general --user "*"

#### Delete all messages from a private group
    slack-cleaner --token <TOKEN> --message --group hr --user "*"

#### Delete all messages from a direct message channel
    slack-cleaner --token <TOKEN> --message --direct sherry --user johndoe

#### Delete all messages from a multiparty direct message channel. Note that the list of usernames must contain yourself
    slack-cleaner --token <TOKEN> --message --mpdirect sherry,james,johndoe --user "*" 

#### Delete all messages from certain user
    slack-cleaner --token <TOKEN> --message --channel gossip --user johndoe

#### Delete all messages from bots (especially flooding CI updates)
    slack-cleaner --token <TOKEN> --message --channel auto-build --bot

#### Delete all messages older than 2015/09/19
    slack-cleaner --token <TOKEN> --message --channel general --user "*" --before 20150919

#### Delete all files
    slack-cleaner --token <TOKEN> --file --user "*"

#### Delete all files from certain user
    slack-cleaner --token <TOKEN> --file --user johndoe

#### Delete all snippets and images
    slack-cleaner --token <TOKEN> --file --types snippets,images

#### Always have a look at help message
    slack-cleaner --help

### Gotchas

If any API problem occurs, try `--rate=<delay-in-seconds>` to reduce the API call rate:

```shell
slack-cleaner ... --rate=1
```

If you see any warning from `urllib3`, consider installing missing packages:

```shell
$ pip install --upgrade requests[security]
```

or just upgrade your Python to 2.7.9.
