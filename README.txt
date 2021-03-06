Originally cloned from git://git.drupal.org/project/htpasswdsync.git

Hosted at https://git.faster-it.com/drupal_htpasswdsync
Mirrored at https://github.com/fasterit/drupal_htpasswdsync

This is the Faster IT version of the htpasswdsync module for Drupal 7.
We have applied patches and improved over the module hosted on drupal.org.
This version supports secure (salted) SHA-256-crypt and SHA-512-crypt password
storage.

Please be aware that SHA-512-crypt hashes are larger than the 64 bytes the
original authors of this module specified. So if you are upgrading from a
previous version and not (re-)installing the module, please execute the
following in MySQL:

  use drupal7; # or whatever your Drupal database is
  alter table htpasswdsync_htpasswd modify passwd varchar(128);

For an overview of other changes please review the git log.

-- SUMMARY --

The HTPasswd Sync module let you synchronize a htpasswd and a htgroup file with
the user database.

For a full description of the module, visit the project page:
  http://drupal.org/project/htpasswdsync

To submit bug reports and feature suggestions, or to track changes:
  http://drupal.org/project/issues/htpasswdsync

-- REQUIREMENTS --

The synchronization only happen on password change. Hence, this module shall be 
installed before any user creation.

You need to run the cron.php job on a regular basis to ensure old users are 
properly cleaned up.

-- INSTALLATION --

* Install as usual, see http://drupal.org/node/70151 for further information.


-- CONFIGURATION --

* Configure synchronized files in Administer >> User management >> HTPasswd Sync >>
  
  htpasswdsync module:

  - htpasswd file
    
    The file that will contain users and password, password are crypted, using
    the standard (insecure) crypt function, with a random two characters seed,
    or - specific to this version of the module - with SHA-256 or SHA-512
    salted hashes that are compatible with more modern Linux crypt
    implementations.

  - htgroup file
  
    The file that will synchronize the roles.
    
  - password hashing algorithm
    
    Let you choose how the password is encrypted/hashed. There are four options
    crypt and SHA-1 (insecure), SHA-256-crypt (good) and SHA-512-crypt (secure).
    Crypt works only on Un*x platforms. SHA-1 shall work on both Windows 
    based systems and Un*xes. The SHA-256/512-crypt versions should work on
    any PHP >= v5.5.
    
    WARNING: changing this value only changes the way new or updated passwords
             are hashed.
             You will need to request your users to all change their password
             if you want to migrate from one hash to another.

  - roles
  
    The roles you want to export in the htgroup file.

  - overwrite
  
    Activate if you want to overwrite your htpasswd file. I left inactive
    htpasswdsync will try its best to keep old entries, but will only try.
    
-- CUSTOMIZATION --

None.

-- TROUBLESHOOTING --



-- FAQ --


-- CONTACT --

Current maintainers:
* Marc Furrer (m.fu) - http://drupal.org/user/310415
* Stefan Wilhelm (7.x-xx) - http://drupal.org/user/1344522
* Faster IT GmbH - https://www.faster-it.com
