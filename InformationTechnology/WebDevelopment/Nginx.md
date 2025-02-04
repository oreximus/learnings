## Nginx Notes

### What is NGINX?

- **NGINX** (pronounced "engine-x") is an open-source, high-performance web server software that can also function as a
  reverse proxy, load balancer, HTTP cache, and mail proxy server. It was created by Igor Sysoev and first released in 2004.
  NGINX is known for its ability to handle a large number concurrent connections efficiency, making it a popular choice for
  busy websites and applications.

#### Key Features of NGINX:

- **Web Server**: NGINX is primarily used for serving static web content and can handle thousands of simultaneous
  connections with a low memory footprint.

- **Reverse Proxy**: Acts as an intermediary between clients and servers, enhancing security and performance by caching
  content and distributing traffic.

- **Load Balancer**: Distributes incoming traffic across multiple servers to improve reliability and reduce server
  overload.

- **Caching**: Caches frequently accessed content to improve response times.

- **Mail Proxy**: Supports SMTP, POP3, and IMAP protocols for email services.

- **Architecture**: Uses an asynchronous event-driven architecture, which allows it to handle high concurrency without
  creating a new process for each request.

#### Use Cases:

- **High-Traffic Websites**: Used by sites like Netflix, Dropbox, and Google for its performance and scalability.

- **Content Delivery**: Often used as a content cache and reverse proxy to reduce load on application servers.

- **Enterprise Solutions**: NGINX Plus offers additional features for enterprise environments, including advanced load
  balanced and performance monitoring.

### Useful Terminologies:

- **reverse proxy**: A **reverse proxy** is a server that acts as an intermediatary between clients ( such as web browsers)
  and one or more backend servers. It is positioned in front of web servers and intercepts incoming requests from clients,
  forwarding them the appropriate server. - perplexity.ai

#### Key functions of a Reverse Proxy:

- **Security**: Reverse proxies can filter traffic, blocking malicious requests and hiding the IP addresses of the
  backend servers, making them less vulnerable to direct attacks.

- **Performance**: They can improve performance by caching frequently accessed content, compressing data, and distributing
  incoming requests across multiple servers (load balancing).

- **Reliability**: By distributing traffic, reverse proxies help prevent any single server from becoming overloaded
  ensuring a more stable and reliable service.

#### Comparison with Forward Proxy:

- **Forward Proxy**: Sits in front of clients, protecting them by filtering outgoing requests to the internet.
- **Reverse Proxy**: Sits in front of servers, protecting them by filtering incoming requests from the internet.

Reverse proxies are essential tools for enhancing the security, performance and scalability of
web applications and are commonly used by large websites and organizations.
