=====================================================
Opsworks for Chef Automate
=====================================================
`[edit on GitHub] <https://github.com/chef/chef-web-docs/blob/master/chef_master/source/opsworks.rst>`__

`[Opsworks for Chef Automate] <https://aws.amazon.com/opsworks/>`__ is an AWS service which you can use to create a Chef Automate instance. All of the Chef Automate documentation applies to the instances you create via Opsworks.

.. _find-opsworks-instance:

Finding your Opsworks for Chef Automate Instance
=====================================================

All of the Chef Automate instances created via Opsworks are named as `aws-opsworks-cm-YOUR_INSTANCE_NAME`. In order to access your Chef Automate instance you can simply search for `aws-opsworks-cm` in AWS Management console and you can find your Chef Automate Instance.

Configuring Opsworks for Chef Automate with Runners
=====================================================

In order to add runners to you "Opsworks for Chef Automate" instance you need a few things:

#. Make sure you have selected "Use an existing EC2 key pair" in the "Select an SSH key" section while creating your Opsworks for Chef Automate instance. In order to add a runner you need to ssh into your instance and run :ref:`install-runner` command.
#. Your runner instance should be reachable via ssh from your Automate instance. For this you need to make sure its subnet, security groups and ssh key pair are configured correctly. We also recommend you setup a dedicated ssh key pair in AWS and copy the private key to your Chef Automate instance and use it while running :ref:`install-runner` command.
#. You can find FQDN of your "Opsworks for Chef Automate" instance in Opsworks console. You can use `ec2-user` as the username to ssh into your instance. Assuming you have configured the ssh keys correctly, ssh command looks like `ssh ec2-user@<instance-name>-an1leihp6urosoui.gamma.opsworks-cm.io`

Pushing a change through Opsworks for Chef Automate
=====================================================

Existing documentation for pushing a change through Chef Automate is applicable for Opsworks for Chef Automate. The only extra configuration that you will need to do to be able to do this is to make sure you edit the security group of your Opsworks Chef Automate instance to allow inbound Git traffic. This is required so that you can create and approve changes in your Automate instance. Once you :ref:`found your Chef Automate instance <find-opsworks-instance>` can go to the linked security group and add a new inbound rule as following:

```
Protocol: TCP
Port Range: 8989
Source: 0.0.0.0/0
```
