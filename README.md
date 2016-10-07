# swift use config

A cloud-config file for a single node swift instance for dev use. The goal is for devs to be able to use the swift api locally. The goal is not for dev on swift. The goal is not for a production usable swift. The goal is not for swift at home. The goal is not for alt swift.

# Why

I wanted to add swift client support to an application and in the course of trying new client APIs I needed a real swift to use. I evaluated my options and they all kind of sucked. I could use devstack, but that runs swift from source. I don't need to hack on the swift source, so devstack seems teh wrong solution. I could use an openstack deploy tool, like juju, but this seems very heavy.

# How

    # change the last line in swift.yaml to import your github or launchpad id.
    lxc launch -e ubuntu:16.04 $(petname) -c user.user-data="$(cat swift.yaml)"
    # wait a bit for it to launch
    lxc list  # get its IP address
    swift --user admin:admin --key admin -A http://$IPHERE:8080/auth/v1.0 upload test swift.yaml
    swift --user admin:admin --key admin -A http://$IPHERE:8080/auth/v1.0 list
    swift --user admin:admin --key admin -A http://$IPHERE:8080/auth/v1.0 list test

