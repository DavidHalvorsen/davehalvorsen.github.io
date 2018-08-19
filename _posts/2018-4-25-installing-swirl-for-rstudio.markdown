---
layout: post
title:  "Installing Swirl for RStudio"
date:   2018-04-25 3:00:40 -0700
categories: R
---
I'm currently taking a class in Data Analysis with R at UCSC. For those that haven't heard, R is a statistical programming language that is commonly used for data analytics. I've been a Windows user my whole life, so it's been tempting to learn R in Windows, *BUT* the majority of the analytics jobs that I'm interested in require Linux experience. That's why I've decided to force myself to learn Linux. I'll probably create a step-by-step post about this later, but for now just know that I've made Linux the default booting operating system for my laptop and desktop computers. My Data Analysis course only requires having R, the programming language, and RStudio, the integrated development environment, installed. Thankfully, I had no trouble installing R and RStudio, *BUT* I've been having trouble installing the RStudio learning platform: [Swirl].

Swirl is a program that teaches you how to program in R *while* you are already running R. You could run it in the terminal, or command prompt, *BUT* it's *so* much easier to work with in RStudio. Swirl comes with a beginner-friendly course titled "R Programming", *BUT* you have the option of installing a variety of classes from the [Swirl GitHub Repository]. Obviously, I'm very interested in completing the Swirl tutorial titled [Mathematical Biostatistics Boot Camp], but I can't even get Swirl to install for RStudio in Linux. I checked with Windows and Swirl installed fine, so it's definitely a Linux issue. [Installing Swirl] is easy. All you have to do is enter 'install.packages("swirl")' as a command in either RStudio *or* R (in the terminal). Here's the error message from my Linux install attempt: 

![Swirl Installation Errors]({{"/assets/swirl_won't_install/swirl_installation_error.png"}})

^That's actually just a snippet of the error messages; in total, it's ~90 lines. Reading closely, you can see that all of the problems seem to be stemming from the absence of 'libcurl' and also 'openssl'. Luckily, this problem was *much* easier to fix that my problem with removing the RSS feed from my website. A Google search for “Configuration failed because libcurl was not found. r studio swirl” yielded this [helpful Stack Overflow] post. User 'steveb' recommended running 'install.packages('swirl', dependencies = TRUE)' in the terminal. This command didn't work for me. I didn't take a screenshot here, but I'm sure you can imagine the readout that said that libcurl was *still* not installed.

I know it didn't work, but I want to talk more about that command. The 'dependencies = TRUE' from the installation command above tells Linux to install Swirl *AND* anything that Swirl might need to run ... maybe I'm being naive, but I can't imagine a circumstance where you'd want to install a program that won't work because it needs other programs ... Why doesn't Linux just install the dependencies automatically? It may have something to do with user control over the operating system. Windows seems to hand-hold you to make sure everything is easy and safe and Linux really pushes you into figuring out *exactly* what you're doing because it isn't beginner-friendly like Windows. It's hard, but I like it.

Now, let's get back to installing Swirl! Going back to that initial Google search string, I found this [helpful Stack Overflow] post. User 'David Maust' suggested to run the command 'apt-get install libcurl4-openssl-dev' as a way of fixing this issue. Luckily, this command installed libcurl, *but* it didn't accomplish the complete dependency install that the first command was aiming at. Sure, I've installed libcurl, but I still need to install openssl. That's next!

![Swirl Install libcurl]({{"/assets/swirl_won't_install/terminal_install_libcurl.png"}})

A new Google search for “Configuration failed because openssl was not found. r studio swirl" found [the solution] that I was looking for. User 'saigoochang' recommended to run the following line in the terminal 'sudo apt-get install libssl-dev'. This installed libssl!

![Swirl Install openssl]({{"/assets/swirl_won't_install/terminal_install_ssl.png"}})

Swirl runs now! I've mostly been programming in python and javascript, so I had *zero* R experience before working with Swirl. It was easy, and enjoyable, to learn!

![Swirl Installed]({{"/assets/swirl_won't_install/swirl_installed_yay.png"}})

It took a couple of hours, but I finished the Swirl introductory R training guide (called 'R Programming'). I can confidently recommend it to anyone that's considering learning R. Now that I've finished the introductory R Swirl class, I want to learn more, *but* there's no automatic way to load Swirl with more classes. It needs to be done manually. The Swirl Documentation gives specific instructions for installing new R Learning Modules. The commands for this part are relatively long, and I don't yet know how to post text in a terminal sort of filter, so you can see the required code I entered in the image below.

![Install Swirl Course]({{"/assets/swirl_won't_install/install_new_class.png"}})

As you can see from the image, I managed to install the 'Open_Intro' class without any issues. Now that I've shown you how I got Swirl installed, I'd like to talk a bit more about it. Each class is broken up into subsections. For example, the introductory R programming class has 15 different sections; I thought the section on functions was the most challenging because you had to code in the terminal, but it was certainly do-able. I *really* like how Swirl guides you step-by-step into learning new commands. Also, it's nice to see a progress bar because it reminds me of how much I've progressed. Here's a representative image of the Swirl learning platform:

![Swirl In Action]({{"/assets/swirl_won't_install/swirl_progress_bar.png"}})



[Swirl]:http://swirlstats.com
[Swirl GitHub Repository]:https://github.com/swirldev/swirl_courses
[Mathematical Biostatistics Boot Camp]:https://github.com/swirldev/swirl_courses/tree/master/Mathematical_Biostatistics_Boot_Camp
[Installing Swirl]:http://swirlstats.com/students.html
[helpful Stack Overflow]:https://stackoverflow.com/questions/35261710/error-when-installing-swirl-in-rstudio-3-1-2
[the solution]:https://github.com/swirldev/swirl/issues/498
[Swirl Documentation]:https://github.com/swirldev/swirl_courses
