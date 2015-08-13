=== Jumpstarter ===
Contributors: jumpstarter, zeuclas
Tags: jumpstarter, url handling
Requires at least: 4.2
Tested up to: 4.2.5-alpha
Stable tag: 17.0
License: Unlicense
License URI: http://unlicense.org

Jumpstarter WordPress integration plugin for running WordPress in a container environment.

== Description ==

WordPress Jumpstarter integration for the Jumpstarter container environment. The main purpose is to
mitigate the problems encountered when running WordPress in a container environment using nginx behind multiple
http proxy layers.

= Features =

- Sandboxes all users and overrides any user capabilities defined in `/app/code/wp-env.json`.
- Injects a login link to support Jumpstarter [reflected login](https://github.com/jumpstarter-io/help/wiki/App-Portals#reflected-login) on `/wp-login.php`.
- Handles login requests from Jumpstarter by authenticating posts of `jumpstarter-auth-token`. On successful authentication the user is logged in as the admin user.
- Hooks in on `set_url_scheme` and uses the env to determine if the url should use http or https.
- Disables the possibility to delete the theme that's specified in the wp env.
- Rewrites urls passed to `wp_enqueue_script` and `wp_enqueue_style` depending on if SSL is on or not.

== Installation ==

= Installation Procedure =
1. Unzip into `/wp-content/plugins/` directory.
2. Activate the plugin in the WordPress admin panel.

== Frequently Asked Questions ==

= Can this plugin be used outside of the Jumpstarter environment? =

Yes. It is possible to use the plugin in any WordPress installation. However, when not running in
a Jumpstarter container environment the functionality of the plugin is reduced.

Features when not running in a Jumpstarter container:

- Hooks in on `set_url_scheme` and uses the env to determine if the url should use http or https.
- Rewrites urls passed to `wp_enqueue_script` and `wp_enqueue_style` depending on if SSL is on or not.

== Changelog ==

= 17.0 =
* Remove the last restrictions on user plugin management.
* Add help on login page for the event of using a non-secure domain.
* Improve code documentation.
* Add compatibility mode for non Jumpstarter container environments.

= 16.0 =
* Open up the plugin for the new Jumpstarter architecture changes (increase the freedom).
* Auto generate WordPress security salts on install.
* Modify nginx `fastcgi_param HTTPS` on init run.

= 15.0 =
* Refactor token authentication functionality, move out to common library.

= 14.0 =
* jumpstarter: bugfix JS_WP_User::has_cap. call parent function with all arguments.
* Store old siteurl as "js_siteurl_old" in env sync phase if siteurl change.
* js-init: ensure core plugins load order on env sync.

= 13.0 =
* Add "jumpstarter_install" hook in install stage.
* Enable users to deactivate plugins that are specified in both plugins and user_plugins.
* js-init: add `jumpstarter_sync_env` action at end of env sync to allow plugins/themes to run env change dependent code.

= 12.0 =
* Wrap sync of env with WordPress in transaction.
* Use js subclasses of sqlite-integration for multiple statement transactions.

= 11.0 =
* Take care of serialized values in updating of meta and options.

= 10.0 =
* Update post meta and options on change of site url.

= 9.0 =
* Enable user plugins.
* Add support for login_redirect filter on token auth.
* Set user information to defaults on install from state db.

= 8.0 =
* Add support for install hooks that are run while db in memory.
* Add support for installing instance from init state.

= 7.0 =
* Allow reflected login link to work in session expired iframe.

= 6.0 =
* Add support for specifying wp options in env.

= 5.0 =
* Allow plugin activation/deactivation from cli.
* Run hooks when activating plugins.

= 4.0 =
* Fix error when activating jumpstarter plugin from redefining WP_SITEURL.

= 3.0 =
* Break out and optimize js_get_env().

= 2.0 =
* js-init: always use admin username on install.
* Let env define the plugins to activate, hide plugins in admin menu.
* Update readme to reflect 2.0 changes.

= 1.0 =
* Initial version

== Upgrade Notice ==

= 17.0 =
This update adds login help and removes the last plugin restrictions.

= 16.0 =
Addresses some issues when running WordPress on a non HTTPS domain in the container environment.
