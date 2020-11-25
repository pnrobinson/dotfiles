FHIR-IG setup
#############

Prereq's
^^^^^^^^

Jekyll: ::

  sudo apt-get install ruby-full build-essential zlib1g-dev
  # Avoid installing RubyGems packages (called gems) as the root user. 
  echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
  echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
  echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
  source ~/.bashrc
  gem install jekyll bundler
