# Rails 5 deploy with ansible, capistrano, postgresql.

### Step 1

Setup SSH keys [(manual)](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2)

### Step 2

Download this repo and unzip.

### Step 3

Change in files:

**/config/deploy/production.rb**

`ip = 'enter_your_server_ip'`

**config/deploy.rb**

```

# Set your repository url
set :repo_url, 'https://github.com/Syntaxys-dll/Rails-5-auto-deploy-boilerplate.git'

# Set deploy directory
set :deploy_to, '/home/deploy/applications/test'

```

### Step 4

Run:

`cap production deploy`
