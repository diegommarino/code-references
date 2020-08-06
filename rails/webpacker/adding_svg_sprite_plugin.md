# SVG Sprite Loader Plugin

## Install
```sh
yarn add svg-sprite-loader
```

## Config
`config/webpack/loaders/svg_sprite.js`
```javascript
module.exports = {
  test: /\.svg$/,
  loader: 'svg-sprite-loader',
  options: {
    extract: true,
    spriteFilename: 'media/images/icons.svg',
    runtimeCompat: true
  }
}
```

`config/webpack/environment.js`
```javascript
...
const svg_sprite_loader = require('./loaders/svg_sprite')
const SpriteLoaderPlugin = require('svg-sprite-loader/plugin');
...
environment.plugins.append(
  'SvgSpriteLoader',
  new SpriteLoaderPlugin({
    plainSprite: true
  })
)

environment.loaders.insert('svg_sprite_loader', svg_sprite_loader, { before: 'file' })
const fileLoader = environment.loaders.get('file')
fileLoader.exclude = /\.(svg)$/i
```

Now when you compile your project there'll be a `icons.svg` file inside your `public/media/images` folder that contains 
all your svgs.

## Using it
You need to load your new `icons.svg` in your project.

First create some helper methods to do it.

`app/helpers/application_helper.rb`
```ruby
module ApplicationHelper
  ...
  def svg_sprite
    icons_sprite_filename = "icons.svg"
    file_path = Rails.root.join("public", "packs",  "media", "images", icons_sprite_filename)
    contents = File.read(file_path)
    return contents.html_safe if contents.present?

    "svg sprite not found"
  end

  def svg_icon(id="", classname="")
    svg = "<svg class='svg-icon #{classname}'><use class='svg-icon-inner' xlink:href='##{id}'/></svg>"
    svg.html_safe
  end
  ...
```

Then add it to your layout.

`app/views/layouts/application.haml`
```haml
%html
  ...
  %body
    ...
    -# Render svg sprite
    .svg-sprite
      = svg_sprite
    ...
```
