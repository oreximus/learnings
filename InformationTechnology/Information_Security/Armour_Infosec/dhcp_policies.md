## Configuring Policies in DHCP

### AND and OR Policy:

- Policy to be executed or applied in these two cases:
  1. `AND`: This will meet the application in the case matching all of the things.
  2. `OR`: This will meet the applcation in the case of one of the things.

Vendor Class Options:

DHCP Standard Options - The default RFC-compliant DHCP options that work with all DHCP clients regardless of vendor
Microsoft Windows 2000 Options - Vendor-specific options designed for Windows 2000 clients
Microsoft Windows 98 Options - Vendor-specific options designed for Windows 98 clients

Available Options Checkboxes:

002 Time Offset - Sets the time zone offset from UTC for the client
003 Router - Specifies the default gateway/router IP addresses for the client network
004 Time Server - Provides IP addresses of time servers (like NTP servers) that clients can use for time synchronization

Purpose:
This configuration allows you to create DHCP policies that deliver different sets of options based on the client's vendor class. For example, you might want to provide specific time servers or routers only to certain types of devices or operating systems.
The policy will match clients based on their vendor class identifier and then apply the selected options accordingly. This gives you granular control over which DHCP options are provided to different types of network clients.
