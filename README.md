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
lock '3.5.0'

set :application, 'test'
# Set your repository url
set :repo_url, 'https://github.com/Syntaxys-dll/Rails-5-auto-deploy-boilerplate.git'
set :branch, 'master'

# Set deploy directory
set :deploy_to, '/home/deploy/applications/test'

set :log_level, :info
set :linked_files, %w{config/secret.yml config/database.yml}
set :linked_dirs, %w{log tmp/pids tmp/cache tmp/sockets vendor/bundle public/uploads}

set :rbenv_type, :user
set :rbenv_ruby, '2.3.1'
set :rbenv_prefix, "RBENV_ROOT=#{fetch(:rbenv_path)} RBENV_VERSION=#{fetch(:rbenv_ruby)} #{fetch(:rbenv_path)}/bin/rbenv exec"
set :rbenv_roles, :all

set :puma_init_active_record, true

desc 'Run rake tasks on server'
task :rake do
  on roles(:app), in: :sequence, wait: 5 do
    within release_path do
      with rails_env: :production do
        execute :rake, ENV['task'], 'RAILS_ENV=production'
      end
    end
  end
end
```
