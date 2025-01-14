title: CloudStor

You can access CloudStor from [Katana Data Mover](./kdm.md).
RClone is installed on KDM so you can upload data into CloudStor. 

## Configure RClone
1. First, you will need to `set your Sync Password` in the 
`CloudStor settings page`, and keep a copy locally.

!!! warning 
    This can be **confusing**. You need to think of the CloudStor web
    interface and the data store as two different logins. The Sync 
    password is for data transfer only and is different from the web
    login password. 
            
2. Next, login to KDM and run:

``` bash
[z1234567@kdm ~]$ rclone config
```

You will be asked a set of questions. The short answers are:

1. new remote ('n')
2. name ('CloudStor')
3. storage type **webdav** ('25' in current installation)
4. url for http connection (https://cloudstor.aarnet.edu.au/plus/remote.php/webdav/)
5. Name of webdav site: **OwnCloud** ('2' in current installation)
6. user name per your cloudstor settings page (first.last@unsw.edu.au, **not** zID@unsw.edu.au)
7. Password ('Yes')
8. enter password (paste or type in the Sync password from step 1 above)
9. confirm password (paste of type in the Sync password from step 1 above)
10. bearer_token: (blank)

You should then see something like this to which you should answer yes:

``` bash

    Remote config
    --------------------
    [CloudStor]
    type = webdav
    url = https://cloudstor.aarnet.edu.au/plus/remote.php/webdav/
    vendor = owncloud
    user = first.last@unsw.edu.au
    pass = *** ENCRYPTED ***
    --------------------
    y) Yes this is OK
    e) Edit this remote
    d) Delete this remote
    y/e/d> y
```

Then quit and test:

``` bash
[z1234567@kdm ~]$ rclone copy --progress --transfers 8 testdata CloudStor:/
```

If it doesn't work, you can edit the config or make a new one.

The 'name' field you are asked at step two of the config is what the config and 
end point will be known as. If you put in the name `Murgatroyd` then you 
would have to access the instance like this:

``` bash
[z1234567@kdm ~]$ rclone copy --progress --transfers 8 testdata Murgatroyd:/
```

[CloudStor](https://cloudstor.aarnet.edu.au/)

[CloudStor settings page](https://cloudstor.aarnet.edu.au/plus/settings/personal)

[set your Sync Password](https://support.aarnet.edu.au/hc/en-us/articles/236034707-How-do-I-manage-change-my-passwords-)
