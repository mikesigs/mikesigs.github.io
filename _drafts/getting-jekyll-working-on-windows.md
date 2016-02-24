---
title: Getting Jekyll Working on Windows
tags: [jekyll, ruby, windows]
---

### Install Chocolatey

Before we start anything, the first thing we're gonna do is install Chocolatey. If you already use Chocolatey, you can skip this step.

There's two ways to install Chocolatey. 
1. Open *cmd* (wiht Admin) and run:
```@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin```
2. Open *PowerShell* and run:
```iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))```

Close and reopen a new command prompt (with Admin)

### Install Ruby
```cinst ruby -y```

### Install Ruby DevKit (required for rdiscount, redcarpet, and wdm)
``` cinst ruby2.devkit```

Edit *c:\bin\DevKit2*
Add ``` - c:\bin\ruby22\```

```ruby dk.rb install```

### Install Bundler
```gem install bundler```

### Fix the stupid SSL certs with RubyGems
```cd c:\bin\ruby22\lib\ruby\2.2.0\rubygems\ssl_certs\```
```curl -Ok https://curl.haxx.se/ca/cacert.pem```

Set system env var: ```SSL_CERT_FILE=c:\bin\ruby22\lib\ruby\2.2.0\rubygems\ssl_certs\cacert.pem```

### Generate your site
Hmmmm...

### Gemfile should look like this
```
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
```
bundle update
bundle install
```

### Run your site
```bundle exec jekyll serve```

