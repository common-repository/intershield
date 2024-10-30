=== InterShield ===
Contributors: InterServer.net Web Hosting
Donate link: https://scanner.interserver.net
Tags: security
Requires at least: 4.9
Tested up to: 4.9.7
Requires PHP: 5.5
License: GPLv2 or later
License URI: https://www.gnu.org/licenses/gpl-2.0.html
Stable tag: trunk

Fast malware scanner with a optional firewall to block malicious traffic.

== Description ==

The intershield plugin is a security plugin for wordpress that ultilizes the large amount of data that comes from InterServers secure intershield hosting which includes up to date
listing and reputations of ip addresses, millions of malware scans on wordpress sites and data of the current threats facing wordpress installs.

The main goals are to:

- block ips that are 100% malicious, while ensuring good ips including good bots are not blocked
- quick scans using checksums to find malware, only falling back to full scanning when the checksum is unknown

Default settings
 - Firewall is off but can be enabled in the settings menu. If enabled there are three options
   * Show a 403 forbidden error (default)
   * use your own forbidden url
   * send user to sigs.interserver.net/refurl site where a captcha is shown and a delist can be done. The blocked url is tracked for malicious calls, and the user if the captcha passes
     is sent back to the original site

 - Scanner
  * sha256 checksums are taken of files and using a dns lookup queries a virus database to return results of the file.
    - Files that have never been scanned before are listed as unknown files. Their status as malware is unknown
    - Unknown file scanning is off by default. This can be enabled in the configuration menu. If enabled unknow files can be sent to a remote scanner using wordpress built in curl functions.
      Please review the privacy section for more information.

Privacy
- By default ips that are bad are send to a remote url where a real user can unblock the ip through a captcha. This also logs the ip, the url, and helps improve the waf firewall.
This setting can be changed in the settings section of the plugin to send the user to your own forbidden page.

- Files that have never been scanned before, can be sent to a remote scanning server. This will scan the file and return a result. The entire file is sent over SSL to be scanned.
This feature is off by default. If enabled it permits remote scanning. Files are not saved or stored on the remote scanning server. However sha256checksums are kept logged as well as the scan result.

Full InterShield Support
- There is no premium option for the plugin. The full intershield support only works on InterServer linux shared hosting at https://www.interserver.net/webhosting/ because
the premium features require software that must be installed at the server level outside of wordpress. Feature include:
 - phpmmdrop to drop php privaleges
 - automatic disabling of scripts in the uploads folder
 - disable directcalling of files in the wp-include folders and other folders that should never be called directly
 - WAF firewall
 - Smart firewall

For those with out full InterShield Support please review https://codex.wordpress.org/Hardening_WordPress


== Installation ==
1. Upload the plugin files to the `/wp-content/plugins/wp-intershield` directory, or install the plugin through the WordPress plugins screen directly.
1. Activate the plugin through the 'Plugins' screen in WordPress
1. Access the InterShield menu. Start scanning with the default minimal configuration or go to the settings section to enable firther options

== Upgrade Notice ==
* Bad ip list is no longer a text file but stored in database

== Frequently Asked Questions ==
* PHP max execution time must be high enough to complete the file scan otherwise a time out may occur.
* Litespeed users may need run PHP with out time outs https://www.litespeedtech.com/support/wiki/doku.php/litespeed_wiki:php:run-without-timeouts
* Use Configuration check to scan unknown files
* 403 forbidden VS Forbidden Link - To use a custom forbidden link show 403 forbidden must be turned off an a full url including http(s):// must be include.

== Changelog ==

= 0.6 =
 * Add ability to view file in check unknown files when malware is detected
 * Fixes

= 0.5 =
 * http_api_curl bug fixes
 * Send unknown files fixes

= 0.4 =
 * Ability to preview malware
 * Fixes

= 0.3 =
* Update readme.txt
* Use javascript from wp core
* fix generic function names / includes
* switch to wp http API
* remove headers in index.php
* save bad ip list to database

= 0.2 =
* Add in ability to disable firewall (now the default setting)
* add in index.php / index.html to prevent directory listing

= 0.1 =
* Initial Release

