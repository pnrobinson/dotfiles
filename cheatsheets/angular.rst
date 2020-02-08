#######
Angular
#######


Setup
~~~~~
In ubuntu, first install node./js (https://github.com/nodesource/distributions/blob/master/README.md). 
Also YARM package manager ::

  curl -sL https://deb.nodesource.com/setup_13.x | sudo -E bash -
  sudo apt-get install -y nodejs
  node -v
  curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
  echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
  sudo apt-get update && sudo apt-get install yarn

Node package manager should also have been installed. ::

  node -v
  
Now install angular CLI. ::

   sudo npm install -g @angular/cli
   ng version
