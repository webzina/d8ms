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

Creating a new Subite (e.g. `foo`)
===============

Basically, do the same that you previously did for default.

1. Configure settings files
  * Run `cp -r web/sites/default web/sites/foo && rm -rf web/sites/foo/files/*`
  * Add entry for `foo` in `drush/aliases.drushrc.local.php`
  * Add entry for `foo` in `web/sites/sites.local.php`
  * Probably you'll need to add a new entry to "trusted_host_patterns" in `settings.allsites.local.php`
1. Setup subsite configuration structure
  * Run `git clone https://github.com/dxvargas/d8ms-subsite subsite/foo`
  * Make symlinks for the subsite directories
    * Run `cd config`
    * Run `ln -s ../subsite/foo/config foo
1. Install Drupal
    * Run `cd ../web` and `drush @foo site-install -vy --account-name=admin --account-pass=admin --config-dir=../config/foo/sync`
    * Verify that sites are working: `drush @foo status`
1. Configure subsite/foo to have it's own repository
1. Usually you will also want to have custom themes and modules, you can store them in `subsite/foo` and add symlinks in usual directories

Notes
===============

1. If subsite configuration structure is only for sync files, the repository
can be cloned directly there. If so, you it is not needed to use symlinks;
1. Many of the steps for first install and creating a new subsite will be
automated with a script;
1. Thanks for the inspiration of [multiplesite](https://github.com/weitzman/multiplesite)
project from [Moshe Weitzman](https://github.com/weitzman).
