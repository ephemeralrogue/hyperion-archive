To create a systemd service that runs a Docker Compose file, you'll need to follow these steps:

1. Create a new directory for your service and add the `docker-compose.yml` file inside it.
2. Create a new file called `[Service]` in the same directory as the `docker-compose.yml` file. This will contain the systemd service definition.

Example of what this file might look like:
```
[Unit]
Description=My Docker Service
After=docker.service

[Service]
User=<your-username>
ExecStart=/usr/bin/docker-compose -f /path/to/your/docker-compose.yml up -d
Restart=always

[Install]
WantedBy=multi-user.target
```

3. Replace `<your-username>` with the actual username of the user who should run the service, and `/path/to/your/docker-compose.yml` with the path to your `docker-compose.yml` file.
4. Make sure that the directory containing your `docker-compose.yml` file has execute permissions (you can do this with `chmod +x <directory>`)
5. Reload the systemd daemon by running `sudo systemctl daemon-reload`
6. Enable and start the service by running `sudo systemctl enable myservice.service` and then `sudo systemctl start myservice.service`

Note: Make sure to replace `<your-username>` and `/path/to/your/docker-compose.yml` with your actual values.

Also, be aware that you might need to adjust the user and group settings depending on your environment. 

You can also use the `ExecStartPre` directive to run a command before starting the Docker Compose service:
```
[Service]
ExecStartPre=/usr/bin/docker-compose -f /path/to/your/docker-compose.yml config
```
This way you can configure your Docker services programmatically.

You can also use `docker-compose up -d` instead of `/usr/bin/docker-compose -f /path/to/your/docker-compose.yml up -d`

You should always check the official documentation for a service, as each one may have different requirements.