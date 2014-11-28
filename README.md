## alban.andrieu.jenkins-slave

[![Travis CI](http://img.shields.io/travis/AlbanAndrieu/ansible-jenkins-slave.svg?style=flat)](http://travis-ci.org/AlbanAndrieu/ansible-jenkins-slave) [![Branch](http://img.shields.io/github/tag/AlbanAndrieu/ansible-jenkins-slave.svg?style=flat-square)](https://github.com/AlbanAndrieu/ansible-jenkins-slave/tree/master) [![Donate](https://img.shields.io/gratipay/AlbanAndrieu.svg?style=flat)](https://www.gratipay.com/AlbanAndrieu)  [![Ansible Galaxy](http://img.shields.io/badge/galaxy-alban.andrieu.jenkinsslave-blue.svg?style=flat)](https://galaxy.ansible.com/list#/roles/1998) [![Platforms](http://img.shields.io/badge/platforms-ubuntu-lightgrey.svg?style=flat)](#)

Ensures that the basic requirements are properly installed (using `apt`) and configured for a jenkins slave to build, test package and deploy your project

### Installation

This role requires at least Ansible `v1.6.3`. 

To install it, run:

    ansible-galaxy install alban.andrieu.jenkins-slave



### Role variables

List of default variables available in the inventory:

```yaml
        ---
    
    jenkins_name: jenkins
    jenkins_user: jenkins
    # python -c 'import crypt; print crypt.crypt("This is my Password", "jenkins")'
    # python -c "from passlib.hash import sha512_crypt; import getpass; print sha512_crypt.encrypt(getpass.getpass())"
    #http://docs.ansible.com/faq.html#how-do-i-generate-crypted-passwords-for-the-user-module
    jenkins_password: "$6$rounds=40000$OvRtT6osJP89GLee$/cizemUXDAH.mW1ILNK1NGk64/TYLgfbHPo3LnFZEZaLsXTOXQV/0f9.bghBsCycJ32rC.meBaujNQI7KgRPQ."
    jenkins_group: jenkins
    #jenkins_shell: "/bin/false"
    jenkins_shell: "/bin/bash"
    #NIS issue jenkins_home: /home/jenkins
    #jenkins_home: "/var/lib/jenkins"
    jenkins_home: "/home/jenkins"
    jenkins_slave_home: "{{ jenkins_home }}"
    jenkins_slave_directory: "{{ jenkins_slave_home }}/jenkins-slave"
    jenkins_jdk7_enable: yes
    jenkins_jdk8_enable: yes
    
    jenkins_ssh_key_file: ""                    # Set private ssh key for Jenkins user (path to local file)
    jenkins_ssh_fingerprints:                   # Set known hosts for ssh
      - "bitbucket.org,131.103.20.167 ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAubiN81eDcafrgMeLzaFPsw2kNvEcqTKl/VqLat/MaB33pZy0y3rJZtnqwR2qOOvbwKZYKiEO1O6VqNEBxKvJJelCq0dTXWT5pbO2gDXC6h6QDXCaHo6pOHGPUy+YBaGQRGuSusMEASYiWunYN0vCAI8QaXnWMXNMdFP3jHAJH0eDsoiGnLPBlBp4TNm6rYI74nMzgz3B9IikW4WVK+dc8KZJZWYjAuORU3jc1c/NPskD2ASinf8v3xnfXeukU0sJ5N6m5E8VLjObPEO+mN2t/FZTMZLiFqPWc/ALSqnMnnhwrNi2rbfg/rd/IpL8Le3pSBne8+seeFVBoGqzHM9yXw=="
      - "github.com,204.232.175.90 ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAq2A7hRGmdnm9tUDbO9IDSwBK6TbQa+PXYPCPy6rbTrTtw7PHkccKrpp0yVhp5HdEIcKr6pLlVDBfOLX9QUsyCOV0wzfjIJNlGEYsdlLJizHhbn2mUjvSAHQqZETYP81eFzLQNnPHt4EVVUh7VfDESU84KezmD5QlWpXLmvU31/yMf+Se8xhHTvKSCZIFImWwoG6mbUoWf9nzpIoaSjB+weqqUUmpaaasXVal72J+UX2B+2RPW3RcT0eOzQgqlJL3RKrTJvdsjE3JEAvGq3lGHSZXy28G3skua2SmVi/w4yCE6gbODqnTWlg7+wC604ydGXA8VJiS5ap43JXiUFFAaQ=="
    jenkins_ssh_authorized_keys_fingerprints:   # Set known authorized keys for ssh
    # Alban Andrieu
      - "ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAIEAio3SOQ9yeK6QfKqSFNKyTasuzjStxWevG1Vz1wgJIxPF+KB0XoMAPD081J+Bzj2LCDRSWisNv2L4xv2jbFxW/Pl7NEakoX47eNx3U+Dxaf+szeWBTryYcDUGkduLV7G8Qncm0luIFd+HDIe/Qir1E2f56Qu2uuBNE6Tz5TFt1vc= Alban"
    
    jdk_dir_tmp: "/tmp" # or override with "{{ tempdir.stdout }} in order to have be sure to download the file"
    jdk_owner: "root"
    jdk_group: "{{ jdk_owner }}"
    
    nexus_url: http://home.nabla.mobi:8081
    
    shell_git_machine: "127.0.0.1"
    shell_git_login: jenkins
    shell_git_name: "{{ shell_git_login }}"
    shell_git_password: jenkins
    shell_git_email: "root@localhost"
    shell_git_path: "/usr/bin"
    shell_git_ssl: false
    
    docker_files_generated_directory: "./"
    docker_files_enable: no
    docker_volume_directory: "{{ jenkins_home }}"
    docker_working_directory: "/tmp/ansible"
    #docker_working_directory: "{{ docker_volume_directory }}"
    docker_image_name: "nabla/ansible-jenkins-slave"
```


### Detailed usage guide

Describe how to use in more detail...


### Authors and license

`alban.andrieu.jenkins-slave` role was written by:
- [Alban Andrieu](fr.linkedin.com/in/nabla/) | [e-mail](mailto:alban.andrieu@free.fr) | [Twitter](https://twitter.com/AlbanAndrieu) | [GitHub](https://github.com/AlbanAndrieu)
- License: [GPLv3](https://tldrlegal.com/license/gnu-general-public-license-v3-%28gpl-3%29)

### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/AlbanAndrieu/ansible-jenkins-slave/issues)!

***

README generated by [Ansigenome](https://github.com/nickjj/ansigenome/).
