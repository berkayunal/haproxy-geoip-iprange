# IP Ranges for Haproxy based on MaxMind GeoIP Lite

Copy the ipranges folder to /etc/haproxy/ and then configure haproxy.conf for your needs

Here is a sample usage for blocking the country XX 

(XX is the 2 letter code for the country - [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2))

``` 
frontend www
	acl XX src -f /etc/haproxy/ipranges/XX.subnets
	tcp-request content reject if XX
```



##### Thanks to:

@Maxmind for the GeoIP Lite