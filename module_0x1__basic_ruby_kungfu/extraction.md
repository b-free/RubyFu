# Extraction
String extraction is one of the main tasks that all programmers need. Sometimes it's getting even harder because we don't get an easy string presentation to extract useful data/information. Here some,

## Extracting Network Strings


### Extracting MAC address from string
We need to extract all MAC address from an arbitrary string
```ruby
mac = "ads fs:ad fa:fs:fe: Wind00-0C-29-38-1D-61ows 1100:50:7F:E6:96:20dsfsad fas fa1 3c:77:e6:68:66:e9 f2"
```

**Using Regex**

The regex should supports windows and Linux mac address formats.

`(?:[0-9A-F][0-9A-F][:\-]){5}[0-9A-F][0-9A-F]`

lets to find our mac
```ruby
mac.scan /(?:[0-9A-F][0-9A-F][:\-]){5}[0-9A-F][0-9A-F]/i
```
Returns
```
["00-0C-29-38-1D-61", "00:50:7F:E6:96:20", "3c:77:e6:68:66:e9"]
```

### Extracting IPv4 address from string
We need to extract all IPv4 address from an arbitrary string

```ruby
ip = "ads fs:ad fa:fs:fe: Wind10.0.4.5ows 11192.168.0.15dsfsad fas fa1 20.555.1.700 f2"
```

```
(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)
```
Let's to find our IPs
```ruby
ip.scan /(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)/

```
Returns
```
[["10", "0", "4", "5"], ["192", "168", "0", "15"]]
```

### Extracting IPv6 address from string
https://gist.github.com/cpetschnig/294476

http://snipplr.com/view/43003/regex--match-ipv6-address/

## Extracting Web Strings
### Extracting URLs from file
Assume we have the following string

```ruby
string = "text here http://foo1.example.org/bla1 and http://foo2.example.org/bla2 and here mailto:test@example.com and here also."
```
<br>
**Using Regex**
```ruby
string.scan(/https?:\/\/[\S]+/)
```

**Using standard URI module**
This returns an array of URL's
```ruby
require 'uri'
URI.extract(string, ["http" , "https"])
```

### Extracting URLs from web site
Using above tricks

```ruby
require 'net/http'
URI.extract(Net::HTTP.get(URI.parse("http://rubyfu.net")), ["http", "https"])
```
or using Regex 
```ruby
require 'net/http'
Net::HTTP.get(URI.parse("http://rubyfu.net")).scan(/https?:\/\/[\S]+/)
```


### Extracting Strings from HTML tags 

Assume we have the following HTML contents and we need to get strings only and eliminate all HTML tags.


```ruby

string = "<!DOCTYPE html>
<html>
<head>
<title>Page Title</title>
</head>
<body>

<h1>This is a Heading</h1>
<p>This is another <strong>contents</strong>.</p>

</body>
</html>"


puts string.gsub(/<.*?>/,'').strip

```

Returns
```
Page Title



This is a Heading
This is another contents.
```






