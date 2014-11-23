# vagrant-nodejs-dev

An ansible-based vagrant environment for kick-starting server-side nodejs application development with MongoDB, Redis and Nginx.

## Usage

```
git clone https://github.com/theasta/vagrant-nodejs-dev.git
cd vagrant-nodejs-dev
ansible-galaxy install DavidWittman.redis
vagrant up
```

This will take some time to complete.
Once it's done, you can ssh inside the vm by running `vagrant ssh`

## Firing nodejs server-side applications

The ansible-nodejs-apps role will help you to fire your nodejs applications as you `vagrant up`.

### Prerequisites

1. A package.json file that should be located at the root of the app repo.
2. A server.js file

Then you have two different ways to get your app(s) running on the virtual machine to choose from.

### I - Put your source code alongside the Vagrantfile and ansible-playbooks

This is the easiest way. You have nothing to do, it will get automatically booted.

If your app is listening to port 3000, you can access it at "http://192.168.50.3:3000".

Note that this port has been defined in the Vagrantfile and you can modify it manually.


### II - Symlink your applications

This configuration has the tremendous advantage of letting you have multiple apps running on a single virtual machine (as long as they are using different ports).

All you have to do is to create a vagrant sync folder for each app you want to include.
Add those lines in the Vagrantfile:

```
  config.vm.synced_folder "/local/path/to/myapp", "/srv/myapp"
  config.vm.synced_folder "/local/path/to/anotherapp", "/srv/anotherapp"
```

Now you need to list the apps you want to enable by listing them in ansible-playbooks/main.yml:

``` 
  - role: ansible-nodejs-apps
    apps:
      enabled:
        - "/srv/myapp/"
        - "/srv/anotherapp/"
```

Then `vagrant reload --provision` and you're all set.