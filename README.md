# Deploying Web Apps: An Overview
When I first began building websites, I had no idea how to actually get my website on the internet. I could run it on `localhost`, but there was a huge disconnect in my understanding of how a website could run on my computer to running on the world wide web. This guide is meant to explain the basics of how to go from `localhost` to `cool-url.com`.

Note: this is not meant to give you a step-by-step guide on how to deploy your website, but to give a simple, understandable overview of what the different parts of the deployment process are.

## Prerequisite Knowledge
For this guide to be useful, you should be comfortable with at least getting a website up and running on your own computer (i.e. `localhost`). If that seems foreign to you, it's worth finding a tutorial online and following it. Now without further ado, let's begin talking about deployment.

## Vocabulary
Understanding the different terms that are thrown around people is half the battle to understanding how deployment works. These definitions might not be super precise, but it's not worth getting into the nit-picky details of what each one really means.

- **deployment**: putting your website or service onto the internet.
- **server**: a computer that will be serving your website to people who traverse the internet. Nowadays, you don't see the physical hardware that is a server. But they exist somewhere in the cloud.
- the **cloud**: this term gets thrown around a lot, and I, for one, did not really understand it in the beginning. Basically the cloud is just the collection of all the computers that exist somewhere that perform functions (e.g. serving websites to you).
- **web server**: not to be confused with a server. A web server is a program that runs on the server and handles incoming requests (i.e. a person that types in `your-url.com`).

## Getting a server
Where does the code that gives you `github.com` exist? It has to exist somewhere. Specifically, it has to exist on a computer that has the code, i.e. a server. Any computer is a server. You could turn your computer into a server that is used to serve your website. But people don't usually do that. Instead, they usually get another server somewhere else to do the serving of the website. Why is that? Well, if you want your website to always be online, your computer is always going to have to be online and have a good internet connection. If you use a laptop, it's probably obvious why this is an issue. There are many other reasons, but the availability is already a big enough problem that you need a computer specifically dedicated to serving your website.

So how do you get a server? These days, they're everywhere. There are many many companies that provide servers you can purchase. For starters, I'd recommend [DigitalOcean](https://www.digitalocean.com/), which costs $5 per month for the most basic server you can get (which is usually more than enough). If you're a student, you can get some credits through the [GitHub Student Developer Pack](https://education.github.com/pack). There are lots of other options, such as Amazon Web Services, but in my experience, they are a bit more complicated to the first-time deployer.

What kind of computer do you get when you get a server? It depends. You can usually select from multiple choices. The standard choice would be some flavor of Linux, such as Ubuntu. If you haven't heard of Linux, it's like Windows or Mac OS X. I'd choose that to start with. Most companies have Linux servers.

Instead of giving you exact instructions on how exactly to get your server up and running, I defer to the documentation of the service you are using.

## Connecting to a server
Once you have "spun up" a server so that it is running, you now need to connect to the server. Think of it as logging in to the server. To do so, you probably have to use something called `ssh`. Whenever you see `ssh`, think of logging in to a server. 

Not everyone should be able to connect to your server, so there has to be some password-like security mechanism. This mechanism is called an ssh key. No need to understand how exactly that works, but just realize that the server needs to know about your key and you must have a key to be able to get into the server. Perhaps a good analogy is that there is a padlock on your server of which you have a key to.

## Configuring a server
Now that you've logged onto the server through `ssh`, you can start setting up your server to serve your website. At this point, your server is brand new, right out of the box. But it doesn't do anything yet. We need to make sure that the server is set up to be able to serve your website. This means that you need to first get your code onto your server. You can do this a variety of ways. I recommend using `git` to do it. To do this, you need to put your code that you want to serve in a git repository on your personal computer. Then you need to install `git` on your server (the command to do so should be easily found via Google). After that, you can `git clone` your repository on your server. Now your code is on your server!

The next step is to make sure that you have installed everything you need to make your website run. This means installing any libraries such as the web framework you're using (e.g. Flask, Ruby on Rails, Django, etc.). This is called installing all the *dependencies* of your project.

Once you've done that, you should be able to run your website, the same way you do to make it show up on `localhost` on your personal computer. Next, we'll discuss how to make your website public.

### Web Servers
One of the main differences between running your website on `localhost` and on a real website is the use of a web server. It might not seem like it, but most web servers that people use to develop and test their projects are not suited for the demands of being on the internet. On the internet, you need to handle many many connections that come within a few milliseconds of each other, and the web server used in development is not meant to perform well in that scenario. Instead, you need to use something like [nginx](https://www.nginx.com/). This is a piece of software that is built to handle serving websites. It can be a bit tricky to understand how to set it up, but there are many guides online that are good places to get started.

## DNS and Routing
The final step of the equation is getting a URL to show your website. This part was particularly confusing for me when I first learned about it, and it took me quite a while to fully understand how it worked. But it's extremely satisfying to understand what exactly happens when you type in google.com.

So what happens when you type in google.com? Essentially google.com is just a label for a server. It's like the address of your home, a way of identifying a specific place in the world of computers. But how does your browser know where to find your server based on the URL?

This is where DNS comes in. DNS stands for Domain Name System. It's essentially a way to map from URLs to actual servers. You don't really need to understand the internals of how it works. All you need to understand is that the DNS keeps a mapping from domain names (i.e. facebook.com in facebook.com/login.php) to the IP address of your server. The IP address of your server is just a sequence of digits that identify it. Something like `123.456.2.13`. It's basically a serial number that identifies it.

So when you type in something like `google.com`, your browser will consult the DNS and find the IP address of the server associated with the domain name. Based on the IP address, the browser can then be served the contents of the website. And that's it! Now someone else on the other side of the globe can visit your website.

## Some concluding notes
Deployment is something that you will not fully understand until you have tried it out multiple times. It is confusing, with lots of parts that can get complicated. Hopefully this guide gives you the higher-level explanation of how a website goes from your computer to the internet. Good luck with your deploying!
