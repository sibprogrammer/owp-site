server 'owp.softunity.com.ru', :web
set :user, 'deployer'
set :deploy_to, '/var/www/owp/public'

desc 'Build site.'
task :build do
  run_locally 'jekyll --no-auto --no-server'
end

desc 'Sync site with production server.'
task :sync do
  find_servers.each do |server|
    run_locally "rsync -avzr --no-owner --no-group -e ssh --rsync-path='rsync' ./_site/ #{user}@#{server}:#{deploy_to}"
  end
end

desc 'Deploy to production server.'
task :deploy do
  build
  sync
end

def run_locally(cmd)
  logger.trace "executing locally: #{cmd.inspect}" if logger
  system(cmd)
end
