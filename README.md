collect-users
=========

Collects user information from */etc/passwd*.

By default it uses all users with a home directory under */home* and *root* **if the shell is not *nologin*.**

You can still get specific users or simply all users on a system while providing an exclude list (see role variables). 


Role Variables
--------------

| Variable								| Type								| Default value								| Comments
| :---										|:--- 								| :--- 												|:---
| `users_list_name`     	| string 							| "users_list"              	| A name for the variable name that will be populated with the user objects. This variable can also be set in an inventory and will then be used instead. 
| `exclude_users_list`		| list								| empty												| Users to be excluded from collecting data for.
| `single_users_list`			| list								| empty												| Only users listed here will be processed execpt the users in `exclude_users_list`.
| `only_home_users`				| bool								| true												| If not defined or set to false, all users will be processed except the ones in `exclude_users_list`.

Example Playbook
----------------

```
- hosts: server
  become: yes
  roles:
    - role: collect-users
      exclude_users_list:
        - root

  tasks:
    - name: Print user data.
      debug:
        msg: "{{ users_list }}"

```
### Example output
```
TASK [Print user data.] 
ok: [server] => {
    "msg": [
        {
            "fullname": "Test User",
            "gid": "1002",
            "home": "/home/test",
            "name": "test",
            "shell": "/bin/bash",
            "uid": "1002",
            "userinfo": "Test User,,,"
        }
    ]
}
```

Dependencies
-------
None 

License
-------

MIT

