# trellis-disable-xml-rpc

[![GitHub tag](https://img.shields.io/github/tag/ItinerisLtd/trellis-disable-xml-rpc.svg)](https://github.com/ItinerisLtd/trellis-disable-xml-rpc/tags)
[![license](https://img.shields.io/github/license/ItinerisLtd/trellis-disable-xml-rpc.svg)](https://github.com/ItinerisLtd/trellis-disable-xml-rpc/blob/master/LICENSE)


Disable [WordPress XML-RPC](https://codex.wordpress.org/XML-RPC_Support) on [Trellis](https://roots.io/trellis/) sites.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Goal](#goal)
- [Why disable WordPress XML-RPC?](#why-disable-wordpress-xml-rpc)
- [Requirements](#requirements)
- [Installation](#installation)
- [Known Issues](#known-issues)
  - [Incompatible Plugins](#incompatible-plugins)
- [FAQs](#faqs)
  - [Can I use this on managed hosting?](#can-i-use-this-on-managed-hosting)
  - [It looks awesome. Where can I find some more goodies like this?](#it-looks-awesome-where-can-i-find-some-more-goodies-like-this)
  - [This isn't on wp.org. Where can I give a ⭐️⭐️⭐️⭐️⭐️ review?](#this-isnt-on-wporg-where-can-i-give-a-%EF%B8%8F%EF%B8%8F%EF%B8%8F%EF%B8%8F%EF%B8%8F-review)
- [Testing](#testing)
  - [Syntax Check](#syntax-check)
- [Author Information](#author-information)
- [Feedback](#feedback)
- [Change log](#change-log)
- [License](#license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Goal

Deny all requests to [WordPress XML-RPC](https://codex.wordpress.org/XML-RPC_Support) (i.e: `/wp/xmlrpc.php`) by Nginx.

## Why disable WordPress XML-RPC?

- [Kinsta: What is WordPress XML-RPC and How To Stop an Attack](http://bit.ly/kinsta-xml-rpc)
- [WPMU DEV: XML-RPC and Why It’s Time to Remove it for WordPress Security](http://bit.ly/2C8TYtt)
- [Sucuri: New Brute Force Attacks Exploiting XMLRPC in WordPress](http://bit.ly/2NwgQnX)
- [Incapsula: WordPress Default Leaves Millions of Sites Exploitable for DDoS Attacks](http://bit.ly/2wtbpP6)
- [LittleBizzy: How (And Why) To Disable WordPress XML-RPC](http://bit.ly/2LARmUr)

## Requirements

- Trellis [17c26fc](https://github.com/roots/trellis/commit/17c26fc9eb5fe0d427195124e8adc91a73380503) or later
- Ansible v2.6 or later

## Installation

Add this role to `requirements.yml`:

```yaml
# requirements.yml
- src: https://github.com/ItinerisLtd/trellis-disable-xml-rpc
  version: 0.2.0 # Check for latest version!
```

Run the command:

```bash
➜ ansible-galaxy install -r requirements.yml --force
```

Add the role into `dev.yml` and `server.yml`, immediately after `role: wordpress-setup`:

```yaml
roles:
  # Some other Trellis roles ...
  - { role: wordpress-setup, tags: [wordpress, wordpress-setup, letsencrypt] }
  - { role: trellis-disable-xml-rpc, tags: [nginx, wordpress, wordpress-setup] }
  # Some other Trellis roles ...
```

Then, re-provision as usual:

```bash
# https://roots.io/trellis/docs/local-development-setup/
➜ vagrant reload --provision

# https://roots.io/trellis/docs/remote-server-setup/
➜ ansible-playbook server.yml -e env=<environment>
```

## Known Issues

### Incompatible Plugins

Unfortunately, some plugins still relying on [WordPress XML-RPC](https://codex.wordpress.org/XML-RPC_Support):

- [Jetpack](https://jetpack.com/support/getting-started-with-jetpack/troubleshooting-tips/)

## FAQs

### Can I use this on managed hosting?

No, you can't use this on managed hosting such as [Kinsta](http://bit.ly/kinsta-com) or [WP Engine](https://typist.tech/go/wp-engine).

You can disable WordPress XML-RPC by filters:

- [xmlrpc_enabled](https://developer.wordpress.org/reference/hooks/xmlrpc_enabled/) - The name is [misleading](https://developer.wordpress.org/reference/hooks/xmlrpc_enabled/#description)!
- [xmlrpc_methods](https://developer.wordpress.org/reference/hooks/xmlrpc_methods/)
- [xmlrpc_element_limit](https://developer.wordpress.org/reference/hooks/xmlrpc_element_limit/)

Or, just use our plugin - [itineris-disable-xml-rpc](https://github.com/ItinerisLtd/itineris-disable-xml-rpc)

### It looks awesome. Where can I find some more goodies like this?

- Articles on [Itineris' blog](https://www.itineris.co.uk/blog/)
- More projects on [Itineris' GitHub profile](https://github.com/itinerisltd)
- Follow [@itineris_ltd](https://twitter.com/itineris_ltd) and [@TangRufus](https://twitter.com/tangrufus) on Twitter
- Hire [Itineris](https://www.itineris.co.uk/services/) to build your next awesome site

### This isn't on wp.org. Where can I give a ⭐️⭐️⭐️⭐️⭐️ review?

Thanks! Glad you like it. It's important to make my boss know somebody is using this project. Instead of giving reviews on wp.org, consider:

- tweet something good with mentioning [@itineris_ltd](https://twitter.com/itineris_ltd)
- star this Github repo
- watch this Github repo
- write blog posts
- submit pull requests
- [hire Itineris](https://www.itineris.co.uk/services/)

## Testing

### Syntax Check

```bash
➜ ansible-playbook -i 'localhost,' --syntax-check tests/test.yml
```

## Author Information

[trellis-disable-xml-rpc](https://github.com/ItinerisLtd/trellis-disable-xml-rpc) is a [Itineris Limited](https://www.itineris.co.uk/) project created by [Tang Rufus](https://typist.tech).

Special thanks to [the Roots team](https://roots.io/about/) whose [Trellis](https://github.com/roots/trellis) make this project possible.

Full list of contributors can be found [here](https://github.com/ItinerisLtd/trellis-disable-xml-rpc/graphs/contributors).

## Feedback

**Please provide feedback!** We want to make this library useful in as many projects as possible.
Please submit an [issue](https://github.com/ItinerisLtd/trellis-disable-xml-rpc/issues/new) and point out what you do and don't like, or fork the project and make suggestions.
**No issue is too small.**

## Change log

Please see [CHANGELOG](./CHANGELOG.md) for more information on what has changed recently.

## License

[trellis-disable-xml-rpc](https://github.com/ItinerisLtd/trellis-disable-xml-rpc) is released under the [MIT License](https://opensource.org/licenses/MIT).
