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
