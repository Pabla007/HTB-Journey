
Here is the github link
https://github.com/digininja/DVWA

Let's clone the repo and get our feet's wet with this...... web application
```
git clone https://github.com/digininja/DVWA.git
```
![[Pasted image 20231007120527.png]]


Now will move the DVWA directory to /var/www/html so that we can fire up the apache2 server and run this on it.
```
mv DVWA /var/www/html
```
![[Pasted image 20231007121434.png]]

Now will try to access the localhost
![[Pasted image 20231007121528.png]]
But we got an error as we haven't started the apache2 server so let's fire it up

```
service apache2 start
```

By default the port is set to 80 but still check this if you get any error if it's listening to port 80 or some other port
```
nano /etc/apache2/ports.conf
```


http://localhost/
![[Pasted image 20231007122353.png]]
We got the default page so lets try to run DVWA and note that apache is case-sensitive so take care of that part.


http://localhost/DVWA/
![[Pasted image 20231007122513.png]]
We have to simply copy the dummy file we got to our config file location to get things working
```
cp config/config.inc.php.dist config/config.inc.php
nano config/config.inc.php
```
![[Pasted image 20231007122906.png]]

Now refresh the page and you are good to goooooooooo
![[Pasted image 20231007122949.png]]

Will now peak into http://localhost/DVWA/setup.php to setup the database
![[Pasted image 20231007123059.png]]
Simply click on the create/reset Db

So now inorder to get the Db running we have to fireup the db service
```
service mariadb start
```

Now the Db service is started we could simple create a Db in it
```
$_DVWA[ 'db_server'] = '127.0.0.1';
$_DVWA[ 'db_port'] = '3306';
$_DVWA[ 'db_user' ] = 'dvwa';
$_DVWA[ 'db_password' ] = 'p@ssw0rd';
$_DVWA[ 'db_database' ] = 'dvwa';
```

Start the sql 
```
mysql
create database dvwa;
create user dvwa@localhost identified by 'p@ssw0rd';
grant all on dvwa.* to dvwa@localhost;
flush privileges; 
```

![[Pasted image 20231007124121.png]]

Now let's connect to the mysql with another terminal
```
mysql -u dvwa -pp@ssw0rd
``` 
Simply click on the create/reset button again and you will see the below output if you have configured everything right
![[Pasted image 20231007124744.png]]

After that we have been redirected to login page
![[Pasted image 20231007124905.png]]
```
username: admin
password: password
```

So the basic version of DVWA is being setup

If you get stuck anywhere here is the link for the youtube video
```
https://youtu.be/WkyDxNJkgQ4
```



>[!note] As per the assessment we have to provide 2 SS with data and time stamp

![[Pasted image 20231007163544.png]]
![[Pasted image 20231007163800.png]]


If want to run after a shutdown run the below commands:
```
service apache2 start
service mariadb start

We can skip the last command as we have already created the database
mysql -u dvwa -pp@ssw0rd
```
