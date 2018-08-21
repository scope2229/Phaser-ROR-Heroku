
     ______     ______     ______     _____     __    __     _______
    /\  == \   /\  ___\   /\  __ \   /\  __-.  /\ "-./  \   /\  ____\
    \ \  __<   \ \  __\_  \ \  __ \  \ \ \/\ \ \ \ \-./\ \  \ \  __\__
     \ \_\ \_\  \ \_____\  \ \_\ \_\  \ \____-  \ \_\ \ \_\  \ \______\
      \/_/ /_/   \/_____/   \/_/\/_/   \/____/   \/_/  \/_/   \/______/


###########################################################################
###########################################################################
###########################################################################
#####                                                                 #####
#####   Game Engine: Phaser 3, Developed by: Photonstorm              #####
#####   Website: www.phaser.io, Git: https://github.com/photonstorm   #####
#####                                                                 #####
#####   Project: Basic Phaser3 ROR, Heroku, Developed by: scope2229   #####
#####   Date: 22/08/2018, Version: 1.0.0                              #####
#####                                                                 #####
#####   Phaser 3.11                                   	              #####
#####                                                                 #####
###########################################################################
###########################################################################
###########################################################################

Versions
* * * * RVM :: 1.29.4 * * * *  
* * * * RUBY ::
First we need to always use RVM. Why? Not all projects need all the gems you will have installed. Often times, if old & new versions of the same gems are installed this can cause incompatibility issues.

This is why we use RVM. It also means when we are developing, we are able to work on any project. The project could use old/stable versions of gems and/or ruby itself. Being able to manage dependencies efficiently with minimal effort and compatibility issues is a must. 80% of a new developers time is debugging and error handling. For a new user that doesn't fully comprehend how systems work along side our tools can quickly loose motivation from searching their code for errors when really it is the our environment that is causing the issues.

https://rvm.io/

To install simply follow the instructions from rvm's homepage.

Now we should have a basic instalation of RVM installed. Next we want to be able to install different versions of ruby.

https://rvm.io/rubies/installing

This app is going to run using the latest versions of all our dependencies. The most important is ruby for now.

https://www.ruby-lang.org/en/downloads/

We see as we have seen many times that there is a current and stable. For companies will more than often use a stable version. This is because up-time and stability are more important than fancy new features. This isn't always the case. Often times applications will require upgrades due to security issues and you should always be checking your dependencies and applications code for vulnerabilities.

You can also use RVM to check for available packages and versions for instance if you wish to use jruby.

rvm list known

rvm install 2.6

(using just 2.6 will choose the latest package from 2.6 in our case ruby-2.6.0-preview2)

If your machine is missing dependencies you will be informed along with what you need to install. With Ubuntu dists this is done automatically with a prompt for your password.

now rvm use 2.6

I already have docs installed locally but you can view them online also.

another thing to point out is if you are using gnome you will need to change some settings to get rvm to install a ruby version

https://rvm.io/integration/gnome-terminal
you should now be able to use

$ rvm -v && ruby -v

---------------------------------------------------------------------

rvm 1.29.4 (master) by Michal Papis, Piotr Kuczynski, Wayne E. Seguin [https://rvm.io]
ruby 2.6.0preview2 (2018-05-31 trunk 63539) [x86_64-linux]           

---------------------------------------------------------------------

Now we can install the rails framework

search for versions

$ gem search '^rails$' --all

See the installation of ruby as a global installation available for any project you wish to use ruby with. They can be switched and swapped with ease but we want to use the ROR framework. Ruby we have installed but what about rails. Rails is a gem from the ruby gems repository.

Sticking to the convention of independent development environments, for less compatibility issues later and to also help keep our environment clean, we want to create a gemset that will store our local gems keeping everything tidy.

$ rvm gemset create gemsetName

now inside our project folder create two files.

$ touch .ruby-gemset && touch .ruby-version

add the following

.ruby-gemset
gemsetName

.ruby-version
2.6.0-preview2

Now if you cd out and back into our application directory it should access our gemset and ruby version.

Note if you dont create a gemset but you have a .ruby-gemset file it will automatically create the gemset.

now we install rails as of today its 5.2.1

$ gem install rails -v 5.2.1

now we can create our application. Note it isnt needed that you create the project folder first. I do this so that I can store notes project diagrams. Information about the tasks at hand. you could create the .ruby-version and gemset files anywhere cd in and out and you will be able to use ruby and rails. you'd then create the application the same way moving the files into our projects root file.

$ rails new PhaserRails --database-postgres

We set our databse for postgres because thats what heroku likes to use and its the easiest test platform as we used it before with node.
Rails creates a ruby-version with the application but sometimes the versions mismatch. Tbh it is more than likely my own configuration with RVM and ubuntu 18.04. But that is something i can sort out later.
Rails also sets up git for us if installed on our machine.

Goto your github account etc. Create a new repository, no need to initialize anything just create a blank repo.

$ git add .

$ git commit -m "initial commit"

$ git remote add origin git@github.com:USERNAME/REPONAME.git

$ git push --set-upstream origin master

Now we need some environment variables so we can set up our connection for the database. never store passwords, API keys and secrets inside of git. If you do change them immediately. You have just compromised your system.

For now have a look in the gitignore file

you'll see the master.key this is how rails 5.2 handles encryption from now on. for older versions you would have used something like dot-env gem.

https://www.engineyard.com/blog/rails-encrypted-credentials-on-rails-5.2

follow along with the site to create an encrypted username and password field for the database. import using the sites example in your database.yml and save

i used nano text editor like so

$ EDITOR="nano" bin/rails credentials:edit
