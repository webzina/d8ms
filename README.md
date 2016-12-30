Overview
===============
Drupal 8 multisite platform with composer.

:bell: This tool is under heavy construction, there are no releases at all.

Getting Started
===============
1. Clone this repo
1. Run `composer install`
1. Configure settings files
  * Create the file `drush/aliases.drushrc.local.php` based in `drush/aliases.drushrc.php`
  * Create the file `web/sites/sites.local.php` based in `web/sites/sites.php`
  * Create the file `web/sites/settings.allsites.local.php` based in `web/sites/settings.allsites.php`
1. Setup subsite configuration structure
  * Run `git clone https://github.com/dxvargas/d8ms-subsite subsite/default`
  * Make symlinks for the subsite directories
    * Run `cd config`
    * Run `ln -s ../subsite/default/config default`
1. Install Drupal
    * Run `cd ../web` and `drush @default site-install -vy --account-name=admin --account-pass=admin --config-dir=../config/default/sync`
    * Verify that sites are working: `drush @default status`

Creating a new Subite (e.g. `foo`) with masterpro profile
===============

1. Configure settings files
  * Run `cp -r web/sites/default web/sites/foo && rm -rf web/sites/foo/files/*` and make sure web/sites/foo/settings.php is writable
  * Add entry for `foo` in `drush/aliases.drushrc.local.php`
  * Add entry for `foo` in `web/sites/sites.local.php`
  * Probably you'll need to add a new entry to "trusted_host_patterns" in `settings.allsites.local.php`
1. Setup subsite configuration structure
  * Run `mkdir subsite/foo subsite/foo/config`
  * Make symlinks for the subsite directories
    * Run `cd config`
    * Run `ln -s ../subsite/foo/config foo`
1. Install Drupal
    * Run `cd ../web` and `drush @foo site-install masterpro -vy --account-name=admin --account-pass=admin`
    * Verify that sites are working: `drush @foo status`
1. Configure subsite/foo to have it's own repository
1. Usually you will also want to have custom themes and modules, you can store
them in `subsite/foo` and add symlinks in usual directories

Profiles
===============
If you want to create a profile that enables configurations,
modules and themes, for all your subsites living under the d8ms platform.
The profiles will not be part of this repository nor any subsite repository.
One easy way to do this is to fork the main repository dxvargas/d8ms and set it
as upstream, then in the forked repository you can add some profile(s).

This was done in https://github.com/webzina/d8ms where the masterpro profile was added.
Then to install the first time the command is `drush @foo site-install masterpro -vy --account-name=admin --account-pass=admin`
and then to export the definitions to use this profile the command is `drush @foo cex -y`.

More information in GitHub about forking:
[Fork A Repo](https://help.github.com/articles/fork-a-repo/)

Notes
===============

1. If subsite configuration structure is only for sync files, the repository
can be cloned directly there. If so, you it is not needed to use symlinks;
1. Many of the steps for first install and creating a new subsite will be
automated with a script;
1. Thanks for the inspiration of [multiplesite](https://github.com/weitzman/multiplesite)
project from [Moshe Weitzman](https://github.com/weitzman).
