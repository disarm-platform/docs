# Starting a containerized algorithm

Once you've built a container, you need to 'run' it to get it ready to be used. 

1. Navigate to the folder with the relevant `stack.yml` file.
2. Using the `image` name from `stack.yml`, something like `disarm/fn-covariate-extractor:0.0.2`, run this command, substituting the `image` name:

```bash
docker run -it --rm -p 8080:8080 disarm/fn-covariate-extractor:0.0.2
```

* This will get it running locally on port 8080 \(you might need to change the _first_ `8080` if there's a conflict on your machine\).
* Should print a few lines and then wait. You can kill it by pressing `control + C` in this terminal

  ```bash
    ❯ docker run -it -p 8080:8080 disarm/fn-covariate-extractor:0.0.2
    2019/03/04 06:54:53 Version: 0.9.14     SHA: a65df4795bc66147c41161c48bfd4c72f60c7434
    2019/03/04 06:54:53 Read/write timeout: 5s, 5s. Port: 8080
    2019/03/04 06:54:53 Writing lock-file to: /tmp/.lock
  ```

