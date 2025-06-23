# How to install bootstrap on rails 8

## JS
run:
```
importmap pin "bootstrap"
```
It will add 2 pins to your `config/importmap.rb` file.

Then go to `application.js` and add:
```js
require "popper"
require "bootstrap"
// before require "controllers"
```

## CSS
Gemfile
```ruby
# SCSS to CSS compiler
gem "dartsass-rails"
# Bootstrap SCSS
gem "bootstrap, "~>5.3.3"
```

run
```
bundle install
rails dartsass:install
```
This command `dartsass:install` will rewrite the `bin/dev` file, adding an attempt to install the foreman gem and so it can use afterwards. But there is a good chance that it will not install the foreman gem.

Install foreman gem locally if you need it. **Don't put it on the gem file!**
```
gem install foreman
```

Rename `application.css` to `application.scss`, then add:
```scss
@import "bootstrap";
```

### In development
The sass compiler needs to run every time you change your scss files, so we have to start an watcher. But the `dartsass:install` command already solved this problem by creating a `Procfile.dev` that runs `rails server` and `rails dartsass:watch` at the same time through the `foreman` gem.

So now, in development you just need to run:
```
bin/dev
```
