How to use Py4J and the hashing algorithm used in Sakai with Djando and edX

Put global_settings.py into
/edx/app/edxapp/venvs/edxapp/lib/python2.7/site-packages/django/conf

Put hashers.py into
/edx/app/edxapp/venvs/edxapp/lib/python2.7/site-packages/django/contrib/auth

Put java-mail-1.4.4.tar into
/usr/lib/jvm/jdk1.7.0_51/lib/ext

Extract py4j.tar into
/edx/app/edxapp/venvs/edxapp/lib/python2.7/site-packages
cd /edx/app/edxapp/venvs/edxapp/lib/python2.7/site-packages
ln -s py4j-0.8.2.1-py2.7.egg py4j

Extract myproject.tar.gz into
/home/ubuntu

Create /etc/rc.local
#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.

export CLASSPATH=$CLASSPATH:/edx/app/edxapp/venvs/edxapp/lib/python2.7/site-packages/py4j-0.8.2.1-py2.7.egg/share/py4j/py4j0.8.2.1.jar:/usr/lib/jvm/jdk1.7.0_51/
lib/ext/java-mail-1.4.4.jar:/home/ubuntu/myproject

cd /home/ubuntu/myproject
/usr/lib/jvm/java-7-oracle/bin/java PasswordService &

exit 0

Restart /etc/rc.local
sudo bash; sh /etc/rc.local

Restart nginx
sudo service nginx stop
sudo service nginx start

Redémarrer edxapp
sudo /edx/bin/supervisorctl -c /edx/etc/supervisord.conf restart edxapp:
sudo /edx/bin/supervisorctl -c /edx/etc/supervisord.conf restart edxapp_worker:
