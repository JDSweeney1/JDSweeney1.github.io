---
layout: post
title:      "Surfs Up! The CLI Gem Project"
date:       2017-12-09 01:07:01 +0000
permalink:  surfs_up_the_cli_gem_project
---



   Wow, what an expeirence. Going through the program, I often worried I was missing some key points or there was a major section I had missed. All of this was due to the fact that I had not yet gone through a project from start to finish, therefore unable to judge how well I knew my stuff. This is where all of that was put to rest. I knew it all... 


   Who am I kidding?? I started this project like a dog who got his head stuck in the bag of chips he wasn't supposed to be eating (`fido = Dog.bad`). I was lost, confused and thought 'well, this is how it ends'.  Seriously, On top of that, I thought that this, of all the lessons available, would be a fantastic time to move from Learn IDE to using the Command prompt and Atom. Go me! 
	 
![Imgur](https://i.imgur.com/Xc98wPKl.jpg)

   However bad this sounds, it was one of my best coding experiences yet. Instead of following some errors due to spec tests and reading up on Stackoverflow, I actually immersed myself in programming. I got to see from the ground up, how awesome, exciting and absolutely powerful coding can be. I feel a much deeper understanding of the entire process and how crucial it is to today's society.  I didn't believe my excitement about programming and what the future holds could get any higher. I was wrong. 
	 
## Getting Started
	 
I was completely new to using the command prompt. I had been using the Learn IDE since the start (Thanks!). However I felt it was time to move on. I knew I was going to have to at some point. I use a windows PC and most of the commands portrayed throughout the course are done using UNIX commands, which is primarily used in Macs, so I had to learn a new set of commands used by the Window's command prompt. It was actually a lot of fun seeing all of the commands possible. Even though the black box looks scary at first, once you get used to it, it is quite simple.  

For those of us lucky enough to use a windows computer (Kidding! Macs are cool too... I guess), here are some helpful CMD commands!

```
cd <File/Folder>            Changes you into the desired file
cd.. or cd ..               Takes you back to the parent folder
chdir <directory>           Changes you into the desired directory
tree                        Shows the current directory or folder structure graphically
mkdir   <dir name>          Makes a new directory or subdirectory
dir                         Shows a list of the folders files or subfolders
```

You can also click [Here](https://commandwindows.com/command3.htm) for more commands!

Here are also a few git commands, crucial for syncing your local repository with the master branch on github.

(Need help figuring out github? Watch [Here](https://www.youtube.com/watch?v=0fKg7e37bQE))

```
git status          Checks the status of of the folder you are currently in and all of its subfolders
git add .           Adds all folders/subfolders/files to the staging area to be commited
git add <File>      Adds the specific file or folder to be staged for commit
git commit -m       Adds the changes in the files to your local repository(not the github or "remote" repository 
                    (-m adds a message to the commit)
git clone "URL"     This clones the remote repository on github to a local repository with the same name
                    (Use the github repository url as the URL)
```

For more git commands, click [Here](http://guides.beanstalkapp.com/version-control/common-git-commands.html).

## Using Bundler

Bundler is an amazing tool that provides ease of access to assigning your dependencies while programming. Another neat feature is that it can help you create your own gem! (Totally awesome in case you didn't know). This way you don't have to go through the hassle of doing all the work yourself. All you have to do is `$ bundle gem <desired name>` and viola! You now have the skeleton of your very own future gem. (Go you!)

Bundler is also great for managing your gem dependencies. All you have to do is create a gemspec file and put in your dependencies such as this example:

##### IN YOUR GEMSPEC FILE OR GEMFILE
```
source 'https://rubygems.org'
require 'nokogiri'
require 'pry'
require 'rspec' 
```

There are too many gems to specifially list them all, however, search around and you will find some neat and extremely helpful gem libraries. Once you have all of your dependencies listed, simply type `$ bundle install` into your terminal. Now all of your dependencies are installed, congratulations! If you want more information on using bundler click [On these blue words](http://bundler.io/) or how to use bundler to create a gem click [On these other blue words](https://bundler.io/v1.16/guides/creating_gem.html).

## daily_surfing time!

Now that I had my framework set up,  It was time to move on to the substance. Seeing as I will be moving  to Miami, FL, once I graduate, I decided I want to learn surfing, a longtime goal of mine. Because of this goal I have, I constantly catch myself checking out the future surf reports for the east coast of Florida and have always thought that it would be nice to be able to pull up the information, without having to go to every page.

It suddenly hit me, it was perfect. Why not use the CLI Gem project as the opportunity to create such a program! I could create a program where I would scrape the websites I constantly rummage through, collect the data and then display it on some interface. So that is exactly what I set out to do. 

To start with, I used bundler as explained above. Initiating the project with  `$ bundle gem daily_surfing`. Now I was ready to get started. 

When it came to the substance of the program, I felt fairly comfortable. The full stack program had up to this point, prepared me well. I had a decent enough understanding of how objects worked with one another how they were each responsible for their own duties. I am not going to go into minute detail about every step I took to code the program, but I will go over some challenges and explain a way to possibly overcome them.


### Challenges

##### Getting started

This can be a very daunting task. You know **what** you want to do, now you have to figure out **how** to do it. I found out that the best way to get started is, well... to start. it may sound reduntant, but I guarentee you its not. It is too easy to stare blankly frozen at an empty project, but once you start to make the first moves, whether they are the right ones or not, it will help get your mind flowing and your confidence growing. 

Secondly, as avi mentions in this [video](https://www.youtube.com/watch?v=_lDExWIhYKI), use fake data or test data to make sure your structure is sound. This way, once you get everything working with the fake data, you know that the real data that you scrape will work! 

##### Creating an environment

This to me is absolutely critical in my opinion(which is a great opinion if I may say so myself). You do not need the hassle of requiring everything on every file. That just becomes frustrating and time consuming. Also, once something breaks, you're in trouble. Make sure you environment contains all the needed requirements from gems to files, then simply require your environment inside the files you use to test and to actually run the program(console.rb and daily_surf.rb in my case). Much easier than going around and requiring everything. 

##### Refactoring

The goal is to make the program work. Once that is complete, it is time to refactor and make the code look pretty. As is frequently mentioned, the best way to start refactoring is to find patterns in the code. If you notice a series of methods whether class or instance, there is a good bet that they can be refactored into a single or few methods that encapsulate the repeating code. Then transmute the code to the disired function by altering it slightly in the code that was just refactored. For example, lets use some code from inside my gem:

This was my original code. (The scraper class had individual scraper methods corresponding to the area since each area was a different web page and required a different url. it is also used to differentiate the report data between regions.):

```
 def self.output_north_florida
   report = Scraper.north_florida
   puts "#{report.name}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts "#{report.date[0]} | Wave height: #{report.wave_height[0]} | Surfing Conditions: #{report.condition[0]} | Weather: #{report.weather[0]} - #{report.weather_temp[0]} |"
   puts ""
   puts "#{report.wind[0]}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts "#{report.date[1]} | Wave height: #{report.wave_height[1]} | Surfing Conditions: #{report.condition[1]} | Weather: #{report.weather[1]} - #{report.weather_temp[1]} |"
   puts ""
   puts "#{report.wind[1]}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts "#{report.date[2]} | Wave height: #{report.wave_height[2]} | Surfing Conditions: #{report.condition[2]} | Weather: #{report.weather[2]} - #{report.weather_temp[2]} |"
   puts ""
   puts "#{report.wind[2]}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts ""
   puts ""
	 end

 def self.output_cental_florida
   report = Scraper.cental_florida
   puts "#{report.name}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts "#{report.date[0]} | Wave height: #{report.wave_height[0]} | Surfing Conditions: #{report.condition[0]} | Weather: #{report.weather[0]} - #{report.weather_temp[0]} |"
   puts ""
   puts "#{report.wind[0]}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts "#{report.date[1]} | Wave height: #{report.wave_height[1]} | Surfing Conditions: #{report.condition[1]} | Weather: #{report.weather[1]} - #{report.weather_temp[1]} |"
   puts ""
   puts "#{report.wind[1]}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts "#{report.date[2]} | Wave height: #{report.wave_height[2]} | Surfing Conditions: #{report.condition[2]} | Weather: #{report.weather[2]} - #{report.weather_temp[2]} |"
   puts ""
   puts "#{report.wind[2]}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts ""
   puts ""
	 end
	 
def self.output_palm_beach
   report = Scraper.palm_beach"
   puts "#{report.name}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts "#{report.date[0]} | Wave height: #{report.wave_height[0]} | Surfing Conditions: #{report.condition[0]} | Weather: #{report.weather[0]} - #{report.weather_temp[0]} |"
   puts ""
   puts "#{report.wind[0]}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts "#{report.date[1]} | Wave height: #{report.wave_height[1]} | Surfing Conditions: #{report.condition[1]} | Weather: #{report.weather[1]} - #{report.weather_temp[1]} |"
   puts ""
   puts "#{report.wind[1]}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts "#{report.date[2]} | Wave height: #{report.wave_height[2]} | Surfing Conditions: #{report.condition[2]} | Weather: #{report.weather[2]} - #{report.weather_temp[2]} |"
   puts ""
   puts "#{report.wind[2]}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts ""
   puts ""
	 end
	 
	 def self.output_broward_miami_dade
   report = Scraper.broward_miami_dade
	    puts "#{report.name}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts "#{report.date[0]} | Wave height: #{report.wave_height[0]} | Surfing Conditions: #{report.condition[0]} | Weather: #{report.weather[0]} - #{report.weather_temp[0]} |"
   puts ""
   puts "#{report.wind[0]}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts "#{report.date[1]} | Wave height: #{report.wave_height[1]} | Surfing Conditions: #{report.condition[1]} | Weather: #{report.weather[1]} - #{report.weather_temp[1]} |"
   puts ""
   puts "#{report.wind[1]}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts "#{report.date[2]} | Wave height: #{report.wave_height[2]} | Surfing Conditions: #{report.condition[2]} | Weather: #{report.weather[2]} - #{report.weather_temp[2]} |"
   puts ""
   puts "#{report.wind[2]}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts ""
   puts ""
	 end
	 ```

It's obvious to see the redundancies. Thus here is the refactored code!

````
 def self.output_broward_miami_dade
   report = Scraper.broward_miami_dade
   self.cli_outline(report)
 end

 def self.output_palm_beach
   report = Scraper.palm_beach
   self.cli_outline(report)
 end

 def self.output_cental_florida
   report = Scraper.cental_florida
   self.cli_outline(report)
 end

 def self.output_north_florida
   report = Scraper.north_florida
   self.cli_outline(report)
 end

 def self.cli_outline(report)
   puts "#{report.name}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts "#{report.date[0]} | Wave height: #{report.wave_height[0]} | Surfing Conditions: #{report.condition[0]} | Weather: #{report.weather[0]} - #{report.weather_temp[0]} |"
   puts ""
   puts "#{report.wind[0]}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts "#{report.date[1]} | Wave height: #{report.wave_height[1]} | Surfing Conditions: #{report.condition[1]} | Weather: #{report.weather[1]} - #{report.weather_temp[1]} |"
   puts ""
   puts "#{report.wind[1]}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts "#{report.date[2]} | Wave height: #{report.wave_height[2]} | Surfing Conditions: #{report.condition[2]} | Weather: #{report.weather[2]} - #{report.weather_temp[2]} |"
   puts ""
   puts "#{report.wind[2]}"
   puts "------------------------------------------------------------------------------------------------------------------"
   puts ""
   puts ""
 end
 ```
 
Ahhh, much better(and shorter, phew!). See the repeating set of code was not needed. All that was needed was for the outline to be encapsulated in the class method cli_outline. As long as it is given the argument of the report generated by the scraper, the outline can individualize the report data while keeping the outline the same. 

After many trials and many, many, many errors, I finally have a working gem!

Now time to publish the gem! It is actually very simple. First, make sure you have a rubygems account or [Sign up](https://rubygems.org/) to get started. Once your account is active (and assuming you set up your gem using the bundler), simply put `$ rake release` into the terminal while in your repository. If it is your first time, it will ask for your rubygems account credentials. There you have it! You have published your gem! Celebrate! 

![Imgur](https://i.imgur.com/KNy9iNP.jpg)

I must reiterate, this has been the single best thing to happen to my programming career. I feel way more confident about coding. This is not solely because throughout this process I have become a better programmer, but because of all of my failures and errors throughout the process, I became much more able and adept to handling those errors. I have grown in these few days from creation to completion in a manner not really describable. It has truly reinforced my desire to continue and really learn programming and technology on general, intellectual and visceral levels.

I attempted to hit the key points where I know i struggled the most or where I feel others might have issues. For me, just getting started from creating the gem using bundler to understanding the command prompt commands was a tough experience. Because of that I learned a lot and thought it would only be right share any bit of help and advice I can. 



