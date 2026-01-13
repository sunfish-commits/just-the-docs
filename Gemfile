source "https://rubygems.org"
gemspec

gem "base64"
gem "csv"

gem "jekyll-github-metadata", ">= 2.15"

gem "jekyll-include-cache", group: :jekyll_plugins
gem "jekyll-sitemap", group: :jekyll_plugins

group :development, :test do
  gem "html-proofer", "~> 5.2"

  # 테스트 인존성
  gem 'rack'
  gem 'rackup'
  gem 'rspec'
  gem 'webrick'

  # 낹 접낱성 테스트
  gem 'axe-core-capybara'
  gem 'axe-core-rspec'
  gem 'capybara'
  gem 'capybara-screenshot'
  gem 'selenium-webdriver'
end
