# Installation

# Overview

We will use Laravel Sail in our development environment; below are the steps to get the `incfile/atomic` repo up and running.

  

## Prerequisites

*   [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
*   [Docker Desktop](https://docs.docker.com/engine/install/)
*   [PHP 7.4](https://www.php.net/downloads.php) or higher & the latest version of [Composer](https://getcomposer.org/download/)
*   [CircleCi](https://app.clickup.com/2403958/v/dc/29bkp-891/29bkp-16365?block=block-99b317e3-1c57-43dc-b42e-488d64e8b11f)
  

## GIT

### Create SSH Keys

Follow [this](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) guide on creating SSH keys and importing them into your GitHub account.

  

### Import SSH Keys to GitHub

-----

  

### Fork the `incfile/atomic` Repo

We use the [Git Forking Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) where developers will work within their fork. When tasks are completed, pull requests should be issued back to the main repo.

  

To begin, fork the [incfile/atomic](https://github.com/incfile/atomic) repository to your personal GitHub account.

  

![](./images/GitFork.png)

###   

### Clone Your Forked Repo

To get your fork out of the `incfile/atomic` repo onto your local machine, you can run the following commands:

```bash
cd [YOUR_PATH]
git clone git@github.com:[USERNAME]/atomic
cd atomic/
```

  

### Add Upstream Repo

Adding the upstream repository to your git remotes lets you easily sync changes from `incfile/atomic` into your fork.

```bash
git remote add upstream git@github.com:incfile/atomic
git fetch -a upstream
```

  

Either the first time or whenever you want to merge in the changes from the `incfile/master` into your feature branch/local, you can run the following command: -a upstream

```bash
git pull upstream master
```

  

## Docker

We need to have the repository running in Docker, to do so we will be using the `laravel/sail` composer package globally. You may install it by running the following command:

```plain
composer global require laravel/sail
```

  

```plain
sh sail/init.sh
```

#### Add sail as an alias. 

As an optional step use Sail as an alias while running your project.

```plain
nano ~/.zshrc // ZSH 
nano ~/.bashrc // Ubuntu Bash 
alias sail='[ -f sail ] && sh sail || sh vendor/bin/sail' 
```

### Setting .env Variables

You may make a copy of the `.env.example` file at the root of your repository and rename it to .env. This will serve as your default configuration for launching your docker containers. You may then modify the variables as you wish.

  

### Bring Up The Machine

To set up the docker containers, you must run the following commands in the root directory of your repo:

```plain
docker-compose up
```

or

sail up

Be patient; this can take some time the first time you do this

  

To access the project routes, we must copy the following host names into our hosts' file (Windows: "C:\\Windows\\System32\\drivers\\etc\\hosts", Mac OS: "/private/etc/hosts")

```plain
127.0.0.1 api.cool
127.0.0.1 atomic.cool
127.0.0.1 db.cool
127.0.0.1 incfile.cool
127.0.0.1 index.cool
127.0.0.1 mailhog.cool
127.0.0.1 maxfilings.cool
127.0.0.1 phpma.cool
127.0.0.1 pro.cool
127.0.0.1 quickcorps.cool
127.0.0.1 usara.cool
127.0.0.1 whitelabel.cool
```

You have to add them Manually.

## Executing Commands in Sail

### Starting Containers

  

*   `sail up`: Allows you to initialize the containers and show logs in real time.
*   `--detach` or `-d` flags: you may also use them to start the containers in the background.
*   `sail start`: Used to resume previously stopped containers, also an alias of `sail up --detach`.

  

### Stopping Containers

*   `sail stop`: Will stop the containers without destroying them.

  

If you initialized sail using the `sail up` command you may also stop the containers using `CTRL/CMD + C`.

  

### Destroying Containers

*   `sail down`: This will stop and remove the containers.

  

## Additional Commands

You may get more context in the official documentation for Laravel Sail: [https://laravel.com/docs/8.x/sail](https://laravel.com/docs/8.x/sail)

  

  

  

  

  

* * *

🏠 [Home](https://example.com/)
