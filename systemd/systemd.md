To create a systemd service that runs a Docker Compose file, you'll need to 
follow these steps:

1. create a new directory for your service and add the `compose.yaml` file 
inside it.
2. fill in the details in the provided `hyperion.service` file.

    - set `User` and `Group` with the details of the user who should run the 
    service. you may need to adjust the user and group settings depending on 
    your environment.
    - set `WorkingDirectory` with the path to your `compose.yaml`.
    - set `ExecStart` with the path to your compose binary, follow by 
    `docker-compose up -d`.
    - set `ExecStop` with the path to your compose binary, follow by 
    `docker-compose down`.
    - set the directory containing your `compose.yaml` file with execute permissions:
    `chmod +x <directory>`.
    - you may also use the `ExecStartPre` directive to run a command before starting the docker compose service, to configure docker services programmatically:
```
[Service]
ExecStartPre=/usr/bin/docker-compose -f /path/to/your/docker-compose.yml config
```


3. place the service file in the directory applicable to how you will run the 
systemd service. if you intend to run the service system-wide, via `root`, 
place the service file in the `/etc/systemd/system` directory. if you intend 
to run the service under a specific user, place it in 
`~/.config/systemd/user`. you may need to create the user directory:

```
mkdir -p ~/.config/systemd/user
```

5. reload the systemd daemon by running `sudo systemctl daemon-reload` if 
running the service under root, or `systemctl --user daemon-reload` if running 
the service under a user.
6. Enable and start the service by running 
`sudo systemctl enable hyperion.service` and then 
`sudo systemctl start hyperion.service`, or 
`systemctl --user enable hyperion.service` and then 
`systemctl --user start hyperion.service`.


You can also use `docker-compose up -d` instead of `/usr/bin/docker-compose -f /path/to/your/docker-compose.yml up -d`
