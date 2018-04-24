# ansible-cassandra
This is a simple ansible project with only single role to install cassandra in ubuntu.
There are a lot of ansible code in the internet which have already solved cassandra installation.

But most of the code i found out was adding a apt-repository, and gpg keys and stuffs.
Its important to understand why the above activities are done. 

1. We add the apt-repository for the apt to know from where to download the package.
2. We add the apt-key to trust that repository.

But the problem is when you try to download cassandra after adding repo, a new key comes, hence the installation fails.

What i have done is i have used the flag **allow_unauthenticated** flag in ansible. The same flag is used in the apt-get install command.

Lets jump into how to run this project:-

- To run this project, run the command-
````yaml
ansible-playbook -i inventory install_cassandra.yml -v
````
- Before running make sure the inventory has the machine ip where you want to deploy and you have ssh access to it.

To run in your project you can:-

- Add the role **ubuntu-cassandra** to the roles in the playbook which you want to run.
````yaml
  roles:
    - ubuntu-cassandra
````

-  Defaults have values of the dependencies of cassandra and its repo url. Change the url if there is any new version available. Add dependencies if new are required.
````yaml
cassandra_repo: deb http://www.apache.org/dist/cassandra/debian 22x main
cassandra_dependencies:
  - openjdk-7-jdk
  - python-software-properties
````


