Ansible playbook template
=========================

Steps to follow
---------------

1. You should have an ssh access to the remote host with keys.  
   Most of the time, you will need root access. The remote user should be root, or a sudoer.  
   To use the playbook with less interactions, the sudoer account should be able to use sudo without password.  

2. Modify the user mentionned in group\_vars depending on the remote user (as explained previously).  
   In this folder, you will define some variables that will be passed to specific groups.  
   For example, to use the user `foo` for the hosts group `bar`, create a `bar.yml` file containing this line.  
   ```yaml
   ansible_ssh_user: foo
   ```

3. Modify targets in the `inventory` file.  
   Place your targets into specific groups.  
   As an example, if you have a target `foo` that will be placed in the group `bar`, insert this line  
   ```yaml
   [bar]  
   foo  
   ```

4. In the playbooks folder, you will create a playbook that could refer to other playbooks or use roles.  
   If you do like this, you will need to create a `roles` subfolder containing all referenced roles.  
   `mkdir roles && cd roles && git clone <url_to_the_role_repository>`  
   to execute the role `foo` on the group `bar`, please create a playbook.yml containing those lines  
   ```yaml
   - hosts: bar  
    roles:  
        - role: foo  
   ```

5. to execute the playbook, use the `deploy_host` script:  
   ```bash
       ./deploy_host sample_playbook groups   
   ```
