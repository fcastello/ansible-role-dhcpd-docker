# Test playbook

Playbook that allows to test against a host.


# Requirements

- automake (to run make)
- python  virtualenv (to run ansible in a confined space)
- Setup ssh key authentication and sudo for the destination host


# Run playbook

Make sure you adapt the inventory to your needs. This invetory expects you have setup passwordless authentication with pub and priv keys.

```
make

source .env/bin/activate

ansible-playbook playbook.yml
```