# Webpacker Deploy Issues

I faced some problems when I deployed my rails app that was using webpacker. The files were not being compiled correctly 
when I was doing `RAILS_ENV=production NODE_ENV=production bundle exec rails webpacker:compile` in my deploy hooks. Looks 
like in some point the command to compile the assets is being executed, but it's not compiling correctly, so I need to 
remove the compiled assets and compile it again.

Here's my deploy hooks config.
```yml
default: &default
    after_bundle:
      - snippet: cloud66/yarn
        target: rails
        execute: true
    last_thing:
      - command: cd $STACK_PATH && yarn && rm -Rf public/packs RAILS_ENV=production NODE_ENV=production bundle exec rails webpacker:compile && bundle exec rails restart
        target: any
        execute: true

staging:
    <<: *default
    last_thing:
      - command: cd $STACK_PATH && yarn && rm -Rf public/packs && RAILS_ENV=staging NODE_ENV=production bundle exec rails webpacker:compile && bundle exec rails restart
        target: any
        execute: true

production:
    <<: *default
```
