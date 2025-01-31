# Changelog for TrustedLogin Client

## 1.3.1 (2022-09-21)

- Fixed: PHP 8.1 warning related to performing string actions on `null`

## 1.3 (2022-08-12)

- Changed: Now display the reference ID by default in both the login screen and the Grant Access screen
- Added `trustedlogin/{ns}/template/auth/display_reference` filter to control whether the reference ID is shown in the access form
- Added error handling when `SiteAccess::get_access_key()` fails

## 1.2 (2022-01-25)

- Fixed WordPress Multisite support  ([#84](https://github.com/trustedlogin/client/issues/84))
  - Also run `wpmu_delete_user()` when deleting support users
  - Use `{get|update|delete}_site_option` instead of `{get|update|delete}_option`
  - Add blog ID to hashes for unique keys and email hashes for each blog on a network
- Fixed hashing an empty string when no license was supplied
- Removed unnecessary database call by only registering endpoint when there's a valid TrustedLogin login request ([#75](https://github.com/trustedlogin/client/issues/75))
- Revoke TrustedLogin now always points to the Dashboard
  - Removed second argument from the `SupportUser::get_revoke_url()` method (`$current_url`)
- Added namespace in passed webhook data (under the key `ns`) to allow for more complex webhook functionality ([#83](https://github.com/trustedlogin/client/issues/83))

## 1.1 (2021-12-13)

- Improved admin menu configuration
  - Enhanced logic around whether and how to add a TrustedLogin menu to the sidebar depending on the `menu/slug` setting:
    - If `null`, the a top-level menu will be added.
    - If `false`, a menu item will not be added.
    - If a string, the `menu/slug` setting will be used as the `$parent_slug` argument passed to the [`add_submenu_page()` function](https://developer.wordpress.org/reference/functions/add_submenu_page/)
  - Added `menu/icon_url` setting that is used as the `$icon_url` parameter in [`add_menu_page()` function](https://developer.wordpress.org/reference/functions/add_menu_page/)
- If granting access fails, the reference ID is now passed onto the support URL using the `?ref=` query parameter
- Removed third arguments for `trustedlogin/{ns}/template/auth` and `'trustedlogin/{ns}/template/auth/footer_links` filters, since the namespace is already known
- Improved WordPress backward-compatibility by removing usage of:
  - `wp_date()` (added in WordPress 5.3); used `DateTime` instead
  - `wp_clear_scheduled_hook()` (added in WP 4.9); used `wp_clear_scheduled_hook()` instead
- Fixed filter naming: `trustedlogin/{ns}/public_key` renamed to `trustedlogin/{ns}/vendor_public_key`

## 1.0.2 (2021-10-07)

- Added `SupportUser::is_active()` method to check whether the passed user exists and has an expiration time in the future
- Added `ref` to the to `trustedlogin/{namespace}/access/extended` hook `$data` argument
- Modified some `WP_Error` error codes to be more consistent

## 1.0.1 (2021-09-27)

- Fixed issue where non-support users may see the "Revoke TrustedLogin" admin bar link

## 1.0.0 (2021-09-22)

This is the initial production release of TrustedLogin! Thank you to everyone who has worked on the project, including [Hector Kolonas](https://github.com/inztinkt), [Josh Pollock](https://github.com/Shelob9), and [Shawn Hooper](https://github.com/shawnhooper).

In addition, a deep thanks to our security auditors: James Golovich with [Pritech](https://www.pritect.net) and Ryan Dewhurst with [WPScan](https://wpscan.com).
