# check_docker_container_status
It's specifically written to monitor the status of the docker
container running.

It uses `docker inspect` to extract the information and represent in nagios
output.

## How to use:

* Clone the repo. (On nagios client)

```
git clone https://github.com/savitojs/check_docker_container_status.git
```

* Copy the plugin to nagios plugin directory (On nagios client) OR Add it plugin to your CM tool if you're using any.

```
cd check_docker_container_status
cp -var check_docker_container_status /usr/lib64/nagios/plugins/
```

* Make changes to nrpe.cfg file. (On nagios client)

```
command[check_docker_container_status]=/usr/bin/sudo /usr/lib64/nagios/plugins/check_docker_container_status
```

* Define in checkcommands.cfg (On nagios server)

```
define command {
   command_name         check_docker_container_status
   command_line         $USER1$/check_nrpe -t 90 -H $HOSTADDRESS$ -c $ARG1$ -a $ARG2$
}
```

* Define in services.cfg (On nagios server)
```
define service {
    use generic-service
    host_name jenkins.example.com 
    service_description check_jenkins_docker_container_status
    check_command check_docker_container_status!jenkins
    contact_groups   devops
}
```
