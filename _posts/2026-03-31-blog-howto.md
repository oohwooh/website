---
date: 2026-03-31T21:05
updated: 2026-04-03T19:31
layout: post
title: How To Set Up Your Own Blog (for free, in under an hour)
permalink: /blog-howto/
---
# Introduction and Overview
If you're reading this you (probably) want to make your own blog, but don't know where to start because coding is intimidating and you don't know how to do it. Great news, you don't need to have any experience to read and follow along! 

If you _do_ have a ton of technical experience, this blog post probably isn't for you. I'm not sharing any novel blogging techniques, just the basics explained in the most beginner-friendly way possible.
# Step 0 - Setting up GitHub
(I'm letting you in on a little programmer inside joke here by starting with "Step 0". Computers start counting at 0, not 1, so often when programmers talk to eachother we will start our counting at 0 to pretend we are computers)

You might have heard of GitHub before, it's the worlds most popular place to store and share code. It's kind of like Google Drive, but for developers. One of the many cool features of GitHub is that they'll host a website for you, for free! (As long as the website is simple enough, which is great because we don't want to make a complicated website anyways.)

- Head to [github.com](https://github.com) and make an account. 
- Once you've made your account, click the plus button in the top right corner and select "New Repository" from the dropdown:

![](/images/20260331232013-github-newrepo.png)

A **repository** is fancy GitHub-speak for a big folder. Right now, you're creating the repository that will store all the code and content for your website. You can call this whatever you want, but I'm going to call mine "blog"

- You can leave every other field alone and click "Create Repository"

# Step 1 - Installing Prerequisites
Next, we need to install a couple pieces of software.
## Ruby
The first thing we're installing is called **Ruby**. Ruby is a programming language (like Python or JavaScript, if you've heard of those) and we need it because it's what was used to develop **Jekyll**, the next thing we're installing.
- To install Ruby, select and follow the install instructions for your operating system [here](https://jekyllrb.com/docs/installation/#guides)

Note that these instructions will expect you to use your computers terminal. You can open this by searching "terminal" on your computer (on Windows, it is called "command prompt" but will still show up when you search for terminal)

> Some of the commands you'll be asked to run are kind of long, and some things are spelled strangely - don't forget you can copy-paste!

## Jekyll
Next, we need to install **Jekyll**. Jekyll is a "static site generator" which basically means it will turn a text file we write in plain English into all the code needed for it to show up as a website. 

- Now you have Ruby installed, run the following command:
- `gem install jekyll bundler`

(you might need to reopen your terminal for this to work)

🎉 You now have Jekyll installed! That was easy, wasn't it?

## Git
We're almost done, the last thing we need to install is **Git**. Git is something called "version control software." Version control is exactly what it sounds like, it makes it easier to keep track of the different versions of a project, and what changed between those versions.

If you've ever worked on a group project, and had to send all kinds of files back and forth, all named silly things like `Untitled Document_final_revision-3_final_final(6).docx` and it was impossible to keep track of and really frustrating and stressful? Git was invented to solve this problem.

Git has a lot of advanced features, but we don't need to use them to run a blog, so I won't be teaching you them. The important part is it's what we need to use to put our blog's files on GitHub. (Now you know what Git is, the name "GitHub" might make a little more sense - it's a hub for storing projects organized using Git)

### Windows
- Run the following command in your terminal:
- `winget install --id Git.Git -e --source winget`

If this doesn't work (likely because you are on a version of windows older than Windows 10) you will need to follow the directions [here](https://git-scm.com/install/windows) - I recommend using the "Standalone Installer"

### MacOS
Most versions of MacOS come with Git preinstalled, so you likely don't need to do anything! You can check this by running `git --version` in your terminal. If you see some output like "git version (a bunch of random numbers)" you're good to go!

If Git didn't come preinstalled, first install [homebrew](https://brew.sh/), then run:
- `brew install git`

### Linux
You can install Git through your distribution's package manager. Follow the instructions for your distribution [here](https://git-scm.com/install/linux)

Not sure your distribution? It's probably "Debian/Ubuntu" and you can install Git using `apt`.

# Step 2 - Setting Up Your Blog
🎉 Great work getting through all that installation!

Now you have everything you need, we can get started on the fun part!

First, you will need to `clone` your repository from GitHub. "Cloning" is a fancy Git word for "downloading" - this is how we get your (currently empty, we're about to fix that) project from GitHub's servers onto your computer. 

- In your terminal, run `git clone https://github.com/[your username]/blog`

(if you called your repository something other than `blog`, replace it with that. You can also copy-paste the URL from your browser. For the purposes of this tutorial I'm going to assume you named it `blog` in subsequent steps)

This will create a new folder, called `blog`. Navigate your terminal inside that folder with the following command: 
- `cd blog`

`cd` is an acronym for "Change Directory" and is how you move through folders using the terminal. Running `cd` is the same thing as double-clicking a folder to open it in your file explorer!

Now you're inside the `blog` folder, run the following command:
- `jekyll new .`

(don't forget the period at the end, it's important!)

After that, run 
- `bundle exec jekyll serve`

After a second or two, you should see the following:
```
Server address: http://127.0.0.1:4000/
Server running... press ctrl-c to stop.
```

**🥳You just made your own website!!!🥳**

Head to [http://localhost:4000](http://localhost:4000) to check it out. If it looks familiar, that's because this is the exact same way I set up my site.

Note that the URL for your website is `localhost` - this means it's running just on your computer, and nobody else can see your website yet. This is fine for now, and it's helpful to have this version to tweak and test things before posting them publicly.
# Step 3 - Making Simple Changes 
Running that `jekyll new .` command created a bunch of files. You can change those files to customize every aspect of your site.

If you want to open your files in something that isn't the terminal, you can run the following command to open it in your operating system's file explorer:
- **Windows:** `explorer .`
- **MacOS**: `open .`
- **Linux** `xdg-open .`

Just like with the `jekyll` command earlier, note the `.` at the end. In the terminal, `.` is shorthand for the current folder. Each of these commands are you asking your computer "Open the current folder, please!"

In the folder that just opened, look for a file called `_config.yml`. You can open this in any text editor. I recommend [Visual Studio Code](https://code.visualstudio.com/) but anything works, really!

`_config.yml` is the main configuration file for Jekyll. Helpfully, Jekyll's developers have added comments explaining what most of the different settings mean. There are a lot more than just these available, if you really want to you can read about all the options [here](https://jekyllrb.com/docs/configuration/).

You can also remove options, if you don't want to set something (for example removing the `email` line if you don't want your email shown)

If you're curious, you can see the `_config.yml` for my website [here](https://github.com/oohwooh/website/blob/main/_config.yml).

- Change the values of `title` and `description`, then save the file

You'll need to restart Jekyll to see your changes (this is only true when changing `_config.yml` making other changes will auto-update)
- Go back to your terminal, and press `ctrl+C` to stop the server. (MacOS: `⌘+C`)  

(Depending on your OS, you might need to press  twice.)
`ctrl-c` is the "stop" command for the terminal. It's like clicking the red x on an application 
# Step 4 - Your First Post

# Step 5 - Making Your Blog Public
# Optional Software
I covered the bare minimum you need to get started. These are some extra pieces that make my life easier, and will probably make yours easier too.
## Obsidian
I use [Obsidian](https://obsidian.md) to write posts. It's a very nice markdown editor and has some quite handy features. Once installed, click "Open folder as vault" and select the folder that contains your blog. (If you followed these instructions to the letter, this will be a folder called `blog`)
### Configuration
I would recommend changing the following settings:
![](/images/20260331214405-obsidian-settings.png)
**Options** -> **Files and Links** -> **Default location for new notes** = "In the folder specified below"
**Options** -> **Files and Links** -> **Folder to create new notes in** = "\_drafts" 
 - Setting these are rather self-explanatory, but it means when you make a new "note" (aka a markdown file, meaning a new blog post) it will automatically show up in your drafts folder. You can work on it there and move it to `_posts` when it's ready
 
 **Options** -> **Files and Links** -> **Default location for new attachments** = "In the folder specified below"
**Options** -> **Files and Links** -> **Attachment folder path** = "images" 
- This will keep all your attachments (which are most of the time images) in one folder, to help keep things organized.
 
 - Note that if you are hosting image-heavy content or otherwise want to host large files on your blog, you might get in trouble with GitHub. You can read more about the limits of GitHub Pages [on their website](https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits), but the TLDR is as long as all your blog files are less than 1GB in total, you are probably fine. It's possible to configure external sites to host your images, and use GitHub Pages just for the text content, but that's out of scope for this article. The term to look up is "CDN" if you want to learn more.

 
**Options** -> **Files and Links** -> **New Link Format** = "Path From Vault Folder"
-  If you don't set this, Obsidian will auto-generate internal links (for instance, to an embedded image, or link to a different post) that will be in the wrong format. Unfortunately, even with this setting the format will still be wrong, just slightly less wrong. For images you will need to add a `/` to the start (i.e. `![](images/whatever.png)` -> `![](/images/whatever.png)`) Correcting links to other posts is more involved, and looks like the following: `[example](_posts/2026-03-31-blog-howto.md)` -> `[example](/2026/03/31/blog-howto.md)`
- I haven't figured out a good, simple, solution to this. Granted, I haven't looked very hard, but if any smart people want to give it a shot and figure it out im sure it's not too hard to make a Jekyll plugin to correct these link patterns during generation.

**Options** -> **Files and Links** -> **Use \[\[Wikilinks\]\]** = off
- Obsidian uses different link syntax, that isn't supported by Jekyll. Turning this off makes Obsidian output links in a format Jekyll understands.

### Community plugins
I also recommend installing the following community plugins 

**Git** - This adds a little sidebar so you can commit and push to GitHub without needing to use the command line. There shouldn't be any setup required as long as your git is configured correctly and you selected the right folder for your vault.

**Update time on edit** - This will automatically add fields to the frontmatter for when a file is created, and edited. I have "Front matter updated name" set to `updated` and "Front matter created name" set to `date`. By default, the minima theme will only display the date created but it's straightforward to customize it to make it display the updated date, if that's something you want.

## Visual Studio Code
If you plan on customizing your theme, or making lots of non-markdown changes, I'd recommend an IDE like [Visual Studio Code](https://code.visualstudio.com/). It's hard to give specific installation or usage instructions since what you want to do will likely be unique and creative, but VS Code is really popular and it should be easy to find someone else's blog post teaching you how to use it. Or you can figure it out and write one of your own, now you have a personal blog!