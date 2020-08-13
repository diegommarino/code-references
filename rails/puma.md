## Restart puma
```sh
bundle exec pumactl -P /home/deploy/.pids/puma.pid restart
```

If you don't know where your puma pid is you can run `ps aux | grep puma` and check the folder in the output.
