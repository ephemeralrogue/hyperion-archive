To create a systemd service that runs a Docker Compose file, you'll need to 
follow these steps:

1. fill in the details in the provided `hyperion.service` file.

    - set `WorkingDirectory` with the path to your `compose.yaml`.
    - set `ExecStart` with the path to your compose binary if running 
    docker-compose in standalone mode, followed by `docker-compose up -d`, 
    or leave as is if using the compose plugin.
    - set `ExecStop` similarly, adding `docker-compose down` if using the 
    standalone binary.
    - you may also use the `ExecStartPre` directive to run a command before starting the docker compose service, to configure docker services programmatically:
    ```
    [Service]
    ExecStartPre=/usr/bin/docker-compose -f /path/to/your/docker-compose.yml config
    ```

2. place the service file in the directory applicable to how you will run the 
    systemd service. if you intend to run the service system-wide, via `root`, 
    place the service file in the `/etc/systemd/system` directory. if you 
    intend to run the service under a specific user, place it in 
    `~/.config/systemd/user`. you may need to create the user directory:

    ```sh
    mkdir -p ~/.config/systemd/user
    ```

3. reload the systemd daemon by running `sudo systemctl daemon-reload` if 
    running the service under root, or `systemctl --user daemon-reload` if running the service under a user.

4. start the service:
    ```sh
    sudo systemctl start hyperion
    ```
    if running the service as root, or 
    ```sh
    systemctl --user start hyperion
    ```
    if running the service as a user.

5. if you choose to run the containers persistently, enable the service:
    ```sh
    sudo systemctl enable hyperion
    ```
    if running the service as root, or
    ```sh
    systemctl --user enable hyperion
    ```
    if running the service as a user.

