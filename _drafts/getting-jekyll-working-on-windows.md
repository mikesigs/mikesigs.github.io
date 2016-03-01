---
title: Getting Jekyll Working on Windows
tags: [jekyll, ruby, windows]
---

It's been almost a year since I started this blog. Sad to say, this is only post #2. Right after I got everything set up and published my first post, wouldn't ya know it... my machine died on me. I recall it being kind of a pain getting Jekyll working on Windows and I just couldn't bring myself to start all over again. Fortunately, a lot has changed in the last 10 months and it is now a cinch to install Jekyll on Windows. Let's get started!

### Install Chocolatey

First of all. If you don't have this magnificent tool installed, now's the time. No really. Now _is_ the time, because you're going to need it to follow the rest of these instructions.

Open **cmd** as Admin and run the following command:

```powershell
C:\> @powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-
object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && 
SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
```

Now, close and reopen **cmd** as Admin. 

Truth be told, **cmd** is ugly and a pain to work with. Do yourself a favor and checkout [cmder](http://cmder.net/). It's not required for any of this to work, but it will make your world a better place since you'll be spending a lot of time in the console with Jekyll. (P.S. You can install it with Chocolatey.)

### Install Ruby
Now that we have Chocolatey installed we can very easily install Ruby like so:

```powershell
C:\> cinst ruby -y
```

This installs Ruby 2.2.4 (at the time of writing) to `C:\Tools\ruby22\`. If for some reason you don't find it there, check the value of your `%ChocolateyBinRoot%` env variable. 

There are a few Gems that rely on the Ruby DevKit to be installed. So let's install that too:

```powershell
C:\> cinst ruby2.devkit
```

To finish setting up the Ruby DevKit we need to tell it where our "Rubies" are. Open the file `C:\Tools\DevKit2\config.yml` in your favorite editor and add " - C:\\Tools\\ruby22\\" to the end of the file (including the leading space, but not the quotes).

Save and close the file and run the next command to complete the DevKit installation.

```powershell
C:\Tools\DevKit2\> ruby dk.rb install
```

### Install Bundler

```powershell
C:\> gem install bundler
```

### Fix the stupid SSL certs with RubyGems
```powershell
C:\Tools\ruby22\lib\ruby\2.2.0\rubygems\ssl_certs\> curl -Ok https://curl.haxx.se/ca/cacert.pem
```

Set system env var: ```SSL_CERT_FILE=c:\bin\ruby22\lib\ruby\2.2.0\rubygems\ssl_certs\cacert.pem```

### Generate your site
Hmmmm...

### Gemfile should look like this
```ruby
source 'https://rubygems.org'
require 'json'
require 'open-uri'

versions = JSON.parse(open('https://pages.github.com/versions.json').read)

gem 'github-pages', versions['github-pages']
gem 'jekyll'
gem 'jekyll-sitemap'
gem 'jekyll-gist'
gem 'octopress', '~> 3.0.0.rc.12'
gem 'wdm', '~> 0.1.0' if Gem.win_platform?
```

### Install Gems
```powershell
bundle update
bundle install
```

### Run your site
```powershell
bundle exec jekyll serve
```


