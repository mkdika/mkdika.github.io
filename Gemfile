source 'https://rubygems.org'

gem 'jekyll', '~> 3.9.0'

group :jekyll_plugins do
  gem 'github-pages'
end

install_if -> { RUBY_PLATFORM =~ %r!mingw|mswin|java! } do
  gem 'tzinfo', '~> 1.2'
  gem 'tzinfo-data'
end

# Performance-booster for watching directories on Windows
gem 'wdm', '~> 0.1.1', :install_if => Gem.win_platform?
