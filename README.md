# vagrant-nodejs-dev

An ansible-based vagrant environment to develop server-side nodejs application with MongoDB, Redis and Nginx roles.

## Usage

```
git clone https://github.com/theasta/vagrant-nodejs-dev.git
cd vagrant-nodejs-dev
vagrant up
```

This will take some time to complete.
Once it's done, you can ssh inside the vm by running `vagrant ssh`

## Firing nodejs server-side applications

It comes with an ansible-nodejs-apps role that will help you to fire your nodejs applications as you `vagrant up`.

There are two different ways to get your app(s) running on the virtual machine.

### Prerequisites

1. A package.json file that should be located at the root of the app repo.
2. If ever you are not using server.js as your primary file, you should update the "script" object with the proper information in package.json

```
"scripts": {"start": "node myApp.js"}
```

### I - Put your source code alongside the Vagrantfile and ansible-playbooks

This is the easiest way. You have nothing to do, it will get automatically booted.

If your app is listening to port 3000, you can access it at "http://192.168.50.3:3000".

Note that this port has been defined in the Vagrantfile and you can modify it manually.


### II - Symlink your applications

You can create a vagrant sync folder that links to your local working directory.  This way, any changes you make locally is also on the vm right away.

This configuration has the tremendous advantage of letting you have multiple apps running on a single virtual machine (as long as they are using different ports).

Add this line in the Vagrantfile:

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

Then `vagrant reload --provision` and you're all good.