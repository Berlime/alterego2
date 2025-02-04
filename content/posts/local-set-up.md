---
title: "Local Set Up"
# description: ""
date: 2025-02-04
# image: ""
lastmod: 2025-02-04
showTableOfContents: false
tags: ["wordpress",]
type: "post"
---

Local WordPress development environments like Local by WP Engine are typically slower than live hosting for several reasons:

1. Resource Limitations: Local runs a full server stack (PHP, MySQL, web server) directly on your computer, sharing resources with your operating system and other applications. In contrast, dedicated hosting environments have optimized server resources.

2. Virtualization Overhead: Local uses virtualization technology to create isolated environments, which adds a layer of processing overhead compared to bare metal servers.

3. Development Features: Local includes additional development tools and features (like live reload and debug logging) that can impact performance but aren't present in production environments.

4. Hardware Differences: Most hosting providers use enterprise-grade SSDs, processors, and networking equipment optimized for web serving. Your local machine, while powerful, isn't specifically optimized for running web servers.

5. Caching Differences: Production environments typically have more sophisticated caching setups (like Varnish, Redis, or CDNs) that aren't configured in local environments.

To improve Local's performance, you could:
- Increase the PHP memory limit in Local's settings
- Disable unused services
- Close other resource-intensive applications while developing
- Use the "Preferred" option instead of "Classic" in Local's settings
- Consider using an SSD for your Local sites

Keep in mind that slower local performance is generally acceptable during development since the focus is on functionality rather than speed optimization.

Copy and paste this code

```php 
//Copy this code, go to wp-config.php file
//and paste it right below define( 'WP_ENVIRONMENT_TYPE', 'local' );
define( 'WP_ENVIRONMENT_TYPE', 'local' ); //configured by Local.
define('WP_MEMORY_LIMIT', '512M');
define('WP_MAX_MEMORY_LIMIT', '512M');
define('MAX_EXECUTION_TIME', '300');
define('UPLOAD_MAX_FILESIZE', '64M');
define('POST_MAX_SIZE', '128M');
define('MAX_INPUT_VARS', '3000');
```


> - *Post Changelogs*
>   - *Nothing Yet*
