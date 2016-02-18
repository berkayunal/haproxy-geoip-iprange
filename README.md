# IP Ranges for Haproxy based on MaxMind GeoIP Lite

Copy the ipranges folder to /etc/haproxy/ and then configure haproxy.conf for your needs

Here is a sample usage for blocking the country XX 

(XX is the 2 letter code for the country - [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2))

``` 
frontend www
	acl XX src -f /etc/haproxy/ipranges/XX.subnets
	tcp-request content reject if XX
```

Last Update: 2016-02-18

#### Creating your own IP Ranges List

Compile iprange tool

Download /tool folder then run make or download the tool from http://www.haproxy.org/git/?p=haproxy.git;a=tree;f=contrib/iprange 

``` shell
make
gcc -s -O3 -o iprange iprange.c
```

Download GeoIPCountryCSV.zip from the maxmind

Check the csv file

``` shell
$ head GeoIPCountryWhois.csv
```

Cut it for iprange

``` shell
$ cut -d, -f1,2,5 GeoIPCountryWhois.csv | head
$ cut -d, -f1,2,5 GeoIPCountryWhois.csv | head | ./iprange
```

Create subnets files

``` shell
$ cut -d, -f1,2,5 GeoIPCountryWhois.csv | ./iprange | sed 's/"//g' | awk -F' ' '{ print $1 >> $2".subnets" }'
```

##### Thanks to:

@Maxmind for the GeoIP Lite

@[Willy](http://1wt.eu/) for the iprange tool

