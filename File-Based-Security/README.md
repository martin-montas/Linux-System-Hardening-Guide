# File Based Security

In this guide we will be exploring some of the most 
common file based security practices.


### 1.0 Using ACLs to Manage File/Directory Permissions
Most Linux systems come with features like ACLs enabled by default. But If you 
want to be sure, run the following:
```bash
tune2fs -l /dev/sdaX | grep 'Default mount options'
```
Replace `/dev/sdaX` with the appropriate device.
if you see `acl` in the output, then you are good to go.

If you don't see anything in the output, then you need to enable ACLs by 
executing the following command:
```bash
mount -o remount,acl /dev/sdaX /
```

### 2.0 Setting ACLs for Files and Directories
The following command will enable ACLs on a specific directory. Remember to 
replace the `/etc` with the correct path and `user1` with the name of the user.
`rx` stands for read and execute permissions enabled for the given user.
```bash
sudo setfacl -m u:user1:rx /etc
```

### 3.0 Setting ACLs for Group
You can also use ACLs for groups. The following sets the ACLs for the 
`admin_group` group for the `/var` directory:
```bash
sudo setfacl -m g:admin_group:rwx /var
```

### 4.0  Viewing ACLs
Once you have set ACLs, you can view them by using the `getfacl` command:
```bash
getfacl /etc
```

