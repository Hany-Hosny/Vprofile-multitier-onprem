# VProfile — Multi-Tier Java Web Application Deployment

## Project Overview

This project demonstrates the manual provisioning, configuration, and deployment of a multi-tier Java web application in a local on-premises environment.

The infrastructure consists of five Ubuntu Linux virtual machines managed using Vagrant and VirtualBox.

The focus of this project is hands-on DevOps infrastructure management, networking, application deployment, and troubleshooting.

## Architecture

```text
                   Browser
                      |
                      v
             web01 — Nginx
             192.168.56.16:80
                      |
                 Reverse Proxy
                      |
                      v
             app01 — Tomcat
             192.168.56.15:8080
                      |
          +-----------+-----------+
          |           |           |
          v           v           v
       MariaDB     Memcached    RabbitMQ
        db01         mc01        rmq01
       :3306        :11211       :5672
```

## Technology Stack

- **Virtualization:** VirtualBox
- **Infrastructure Provisioning:** Vagrant
- **Operating System:** Ubuntu 22.04 ARM64
- **Web Server:** Nginx
- **Application Server:** Apache Tomcat 9
- **Build Tool:** Apache Maven
- **Java:** OpenJDK 11
- **Database:** MariaDB
- **Caching:** Memcached
- **Messaging:** RabbitMQ
- **Scripting:** Bash

## Virtual Machine Configuration

| VM | Service | Private IP | RAM |
|---|---|---|---|
| db01 | MariaDB | 192.168.56.12 | 1536 MB |
| mc01 | Memcached | 192.168.56.13 | 1024 MB |
| rmq01 | RabbitMQ | 192.168.56.14 | 1024 MB |
| app01 | Tomcat | 192.168.56.15 | 2048 MB |
| web01 | Nginx | 192.168.56.16 | 768 MB |

## Implementation

1. Defined five virtual machines using Vagrant and YAML-based resource configuration.
2. Configured private networking and hostname resolution.
3. Installed MariaDB and imported the initial application database.
4. Configured Memcached and RabbitMQ services.
5. Installed Java, Maven, and Tomcat.
6. Built the Java application using Maven and deployed the WAR artifact.
7. Configured Nginx as a reverse proxy to Tomcat.
8. Validated application accessibility and the login flow from the host browser.

## Infrastructure Setup

**Prerequisites:** A compatible installation of Vagrant, VirtualBox, and the Vagrant Hostmanager plugin.

Start the virtual machines:

```bash
VAGRANT_DEFAULT_PROVIDER=virtualbox vagrant up
```

Check their status:

```bash
VAGRANT_DEFAULT_PROVIDER=virtualbox vagrant status
```

**Note:** This repository documents a manual service provisioning lab. The Vagrantfile creates the virtual machines, but the database, application, and web services were configured manually. Running `vagrant up` alone does not reproduce the fully configured application.

## Troubleshooting & Lessons Learned

During deployment, I investigated and resolved:

- Virtual machine boot and SSH timeout issues
- Host port forwarding conflicts
- Linux file ownership and permission errors
- Tomcat systemd startup failures
- Hostname resolution issues between virtual machines
- Nginx reverse proxy configuration

These challenges provided practical experience diagnosing problems across multiple infrastructure layers.

## Results

The VProfile application was successfully deployed to Tomcat and accessed through Nginx.

The application login flow and authenticated profile page were verified in the browser.

Functional integration testing for Memcached and RabbitMQ remains a separate validation step.

## Security Notes

This is a local development lab, not a production-ready deployment. Application passwords, private SSH keys, and VM state files are excluded from the repository. HTTP is used within the private lab network.

## Credits

The Java application is based on the original [VProfile Project](https://github.com/hkhcoder/vprofile-project).

My work focused on infrastructure provisioning, service configuration, networking, application deployment, and troubleshooting.

## Next Project

Automating the same multi-tier infrastructure using Vagrant and modular Bash provisioning scripts.
