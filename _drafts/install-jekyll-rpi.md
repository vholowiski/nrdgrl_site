Installing Jekyll on your raspberry pi

	with credit from https://jekyllrb.com/docs/installation/

log in as user
First we need to install ruby and it's dependencies
sudo apt-get update && sudo apt-get install ruby ruby-dev build-essential -y
This took about a minute on my 3b+

Avoid installing gems as root user
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME=$HOME/gems' >> ~/.bashrc
echo 'export PATH=$HOME/gems/bin:$PATH' >> ~/.bashrc
source ~/.bashrc

Install Jekyll
gem install jekyll bundler
This took 8 mins 16 secondx on my 3b+

