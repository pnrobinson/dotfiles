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
   
New Angular project & basics
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a new template and start the application, enter: ::

  angular new hello-world
  cd hello-world
  ng serve

and then open the app at http://localhost:4200/.

Angular architecture
~~~~~~~~~~~~~~~~~~~~
Each Angular appp contains one or more module. Each module contains one or more components and services. Each component contains HTML and a class. Modules can also contain services for the business logic.


Angular components
~~~~~~~~~~~~~~~~~~

To make a new component called test (g=generate, c=component) ::

  ng g c test
   
This creates a subdirectory test with test.component.* files and also modifies the app.module.ts file to import it. The test module has the tag app-test, and we can add this to the main html template as ``<app-test></app-test>``.


Attributes vs Properties
~~~~~~~~~~~~~~~~~~~~~~~~
Attribute is the initial value specified in the HTML file or template. The property can change, e.g., in an HTML form. Attributes cannot change.
