[:house_with_garden:](../index.md)

Docker
-
* install docker [:see_no_evil:](https://docs.docker.com/get-docker/)

* install the latest version of docker compose
    ```shell
    COMPOSE_VERSION=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)
    curl -L "https://github.com/docker/compose/releases/download/${COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    chmod +x /usr/local/bin/docker-compose
    ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
    docker-compose --version
    ```

* how to use systemd to run docker compose

    ```shell
    cat > /etc/systemd/system/docker-compose@.service <<EOF
    [Unit]
    Description=%i service with docker compose
    Requires=docker.service
    After=docker.service
    
    [Service]
    Type=oneshot
    RemainAfterExit=true
    WorkingDirectory=/root/appdata/%i
    ExecStart=/usr/local/bin/docker-compose up -d
    ExecStop=/usr/local/bin/docker-compose down
    
    [Install]
    WantedBy=multi-user.target
    EOF
    ```

    ```bash
    cat > /etc/systemd/system/docker-compose-app.service <<EOF
    [Unit]
    Description=Docker Compose Application Service
    Requires=docker.service
    After=docker.service
    
    [Service]
    WorkingDirectory=/root
    ExecStart=/usr/bin/docker-compose up
    ExecStop=/usr/bin/docker-compose down
    TimeoutStartSec=0
    Restart=on-failure
    StartLimitIntervalSec=60
    StartLimitBurst=3
    
    [Install]
    WantedBy=multi-user.target
    EOF
    ```

    ```shell
    sudo systemctl enable docker-compose@<dir-name>
    sudo systemctl create docker-compose@<dir-name>
    ```