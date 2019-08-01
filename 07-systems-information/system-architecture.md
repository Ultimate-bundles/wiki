<!-- TITLE: System Architecture -->
<!-- SUBTITLE: A quick summary of System Architecture -->

# A full guide to Ultimate Bundles System Architecture

### Routing and Server Management
![Ub Tech Architecture Routing And Server Management](/uploads/ub-tech-architecture-routing-and-server-management.png "Ub Tech Architecture Routing And Server Management")

This image shows an overview of UB's routing and server management. Notes:

1. Orange arrows represent public traffic. Requests to ultimatebundles.com or access.ultimate-bundles.com/wp-admin, for example. Note that this includes any traffic created by admins as well as site visitors and customers. All traffic is identical in the eyes of these systems; Authentication is handled at the application level.
2. Purple arrows represent private encrypted connections, like SSH.
3. Blue clouds represent cloud services. Each is obviously its own entire ecosystem, but for our purposes they can be oversimplified as single entities which communicate perfectly and instantly.
4. Public traffic requests the IP of a domain name like ultimatebundles.com. Route 53 handles these requests, forwarding them to the apropriate IP address. For requests to all servers but the divi application server, these requests go directly to nginx on the apropriate server. For divi, those requests go to Imperva instead, which controls the traffic for security, and forwards allowed traffic onwards as normal.
5. The large black box titled "VPS Rackspace" represents the virtual rackspace provided by Linode and Digital Ocean. Obviously individual requests are only sent to the correct individual server, but representing all of them on this image would be a waste of space.
6. Linode Cloud Manager has a direct connection to each server they provide, similar to plugging a mouse and keyboard into a physical machine directly. However, it is mostly only used for monitoring the hardware resources rather than changing them.
7. Forge and Envoyer work together to provide simpler, safer, easier server management. Forge for server utilities, Envoyer for CI.

### Application Ecosystem
![Ub Tech Architecture Application Ecosystem](/uploads/ub-tech-architecture-application-ecosystem.png "Ub Tech Architecture Application Ecosystem")

This image shows a more granular perspective of the types of traffic hitting our servers, and a list of the servers themselves. Notes:

1. Orange arrows reprsent public traffic from visitors and customers.
2. Red arrows represent public traffic from staff and admins, who authenticate at each application.
3. Purple arrows represent secure integrations between systems, either through authenticated APIs, direct database connections, or other direct secret communications
4. The blue server AccessUltimateBundlesCom is the access site. This is the one server that's actually on a DigitalOcean VPS. It's a wordpress site with it's own integrated DB.
5. The CDN servers work together to serve the bundle content. All the content is public and accessible to anyone, but most people aren't aware of how to get the content except through the access site, which requires authentication to get the URLs. The two servers work together using Route 53's Weighted Routing Policy, which splits all traffic to the domain to the two different servers evenly. The CDN's content is made accessible in it's filesystem in a Dropbox-synced folder. This allows staff to easily load new content by simply putting it into folders in a shared Dropbox account, which after syncing, automatically makes it accessible publicly and generates a URL for it.
6. The UltimateBundlesComApp ecosystem is complex. The main application is depicted in the middle of the 3, with the staging site to its left and the divi content manager to its right. The staging site is a near-exact copy of the main site, except that it pulls the application from the dev branch of the git repository, while the main app uses master.
7. The divi content management works like this: The Divi APP is a WP instance on its own server. It interfaces with a remote DB on its own server. The applications (both staging and production) interface with both the database AND the divi WP site. They can connect directly to the DB for some requests for their content, but also use the ACF REST API provided by the WP plugin on the divi app server. In short, these applications are using both the DB directly and indirectly through an API run by Wordpress. The details of these connections will be explored below.

### UltimateBundlesCom




### Platforms and their roles

Route 53
https://console.aws.amazon.com/route53/home
Route 53 is Amazon's DNS management utility. The destinations of our domains are managed here.

Linode VPS and Cloud Manager
https://cloud.linode.com/linodes
Linode is our VPS provider, and their cloud manager provides monitoring and controls for hardware level issues. 

Forge
https://forge.laravel.com/servers
Forge provides a ton of server configuration automation and management tools. In short, it automates the difficult and finicky parts of setting up and running production servers. It allows us to spin up new servers automatically, manage their databases, applications, and even provides some automated deployment tools through integrations with version control. Some common tasks accomplished in forge include...

* Deploying new servers
* Deploying new nginx sites to existing servers
* Managing server ssh keys
* Manage database users, connections, and permissions
* Scheduling automated maintenance tasks
* Controlling daemons
* Managing private server networks, making it easy to have an application server and separate database server, for example.
* Install/uninstall monitoring software like papertrail.
* Edit application environment variables
* Create and manage job queues
* Manage SSL certs
* Manage Nginx Config and add redirects

Envoyer
https://envoyer.io/dashboard
Envoyer is a zero-downtime deployment tool, providing Continuous Integration or CI. It has a few convenience features we use, but for the most part is used entirely for it's deployment pattern. This pattern follows a few simple steps:

1. Create a new directory with the latest version of the application
2. Change all references to the application to the new folder
3. Delete the old folder

This process ensures there is no downtime when updating an application to the latest version. It is currently only used for the production server of the main UB website.

Imperva
https://www.imperva.com/
Imperva (formerly Incapsula) is a firewall on steroids. For certain domains that use it, it sites in between Route 53 DNS and the application server itself, shielding the application server from unwanted attacks by managing DNS itself. This is currently only used on the divi application server, protecting it's REST data routes using an IP whitelist, which contains only application servers and developer IPs.