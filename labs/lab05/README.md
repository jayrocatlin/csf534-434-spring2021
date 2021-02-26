# Lab 05: Network Intrusion Detection with Snort


Create a copy of this google document [lastname_lab05]() (File > Make a Copy) to record all of your assignment answers in.

The table of contents for this lab is found below.

Part 1. Snort Rules: Ep.1 <br>
Part 2. Snort Rules: Ep.2 – DNS <br>
Part 3. Snort Rules: Ep.3 – HTTP <br>
Part 4. Submission <br>

## Snort

Snort is a free open-source network intrusion detection system. Developed and updated by Cisco, Snort has the ability to perform packet logging, protocol analysis, content searching, and pattern matching.

## Part 1 - Snort Rules: Ep.1

The below language is simply pulled from www.immersivelabs.com for your convenience. Please, read the information below and complete the [Snort Rules: Ep.1](https://immersivelabs.online/labs/snort-rules-episode-1/category/defensive/series/snort) lab on immersivelabs.

### IDS rules

For this lab, the scanning engine is Snort version 2.9.7.0 GRE (Build 149).

A standard rule is broken down as follows:

* [action]
* [protocol]
* [ip address] – source
* [port number]  – source
* [direction options]
* [ip address]  – destination
* [port number]  – destination
* [general options]
* [detection options]

Below is an example of the rule syntax:


```snort
alert tcp 10.10.10.0/24 any -> 192.168.0.0/24 443 (msg: “Test Rule”; content: “This is some content”; sid: 5000001; rev: 1;)
```

We will now explain the components of an IDS rule in more depth.

### Actions

The ‘actions’ define which action is taken by the detection engine if a packet matches the rule. There are several options. The most common are as follows:

* `alert` generates an alert and logs the packet
* `log` logs the packet
* `pass` ignores the packet
* `drop` blocks and logs the packet reject blocks the packet, logs it and then sends a TCP Reset or ICMP Port Unreachable

### Protocol

The second component is the protocol. This determines the type of traffic we're looking for, and there are currently four valid options:

* `TCP`
* `UDP`
* `ICMP`
* `IP`

### IP Address

This is the first IP address that must be matched. The engine understands the following syntax for IP addressing:

* any – a wildcard for any IP address
* 10.10.10.23 – any single valid IP address
* 10.10.10.0/24 – CIDR notation for block ranges
* !192.168.0.1/24 – prefixing this field with an exclamation mark means ‘NOT’
*  [192.168.1.1,192.168.1.2,192.168.1.3] – comma-separated lists can use the previous syntax

### Port

This field is a port number. The engine understands the following syntax:

* `any` – a wildcard for any port
* `443` – any single port number
* `1:1024` – port range

### Direction Options

This sets the direction of the match and is important when creating rules. The valid options are as shown:

* `<>` bidirectional
* `->` unidirectional

This is followed by another set of IP addresses and port numbers. Standard notation considers the IP and port on the left-hand side of the direction arrow as the **Source**, and the IP address and port on the direction arrow’s right-hand side as the **Destination**.

### General options

The remainder of the rule falls within a set of parentheses. These options set the metadata element of the rule. They are known as **key:value** pairs and are terminated with a semicolon. There are several options here. The standard fields are as follows:

* `msg` is the message that displays in the log/alert
* `sid` is a unique numerical identifier that identifies the rule and has several reserved ranges
* `rev` annotates the revision of a rule
* `classtype` is used to categorise and group common rules and has many defaults

### Detection options

This is where rules start to get complicated. The previous fields were all used for setting metadata and understanding traffic flow. This set of `key:value` pairs instructs the scanning engine to detect specific data within packets.

### Content

The content keyword forms the core of the rule detection. It can include text, binary data or a mixture of the two. It is important to keep in mind that content keywords are case sensitive.

The following examples are valid content values:

* `content: "This is a string of text";`
* `content: "|68 65 6c 6c 6f|";`
* `content: "Hello |77 6f | rld";`
* `content: !"Not this one";`

The second example uses the hex values enclosed within a pair of pipes `|`.

The third example uses a mix of text and hex characters.

The final option shows the use of ‘!’ to perform a negative match.

Each rule can have multiple content patterns.

The behaviour of the content field is adjustable with the use of modifiers. Each content keyword can have several modifiers, and the modifiers will only alter the previous content option.

There are many modifiers that are observable in the Snort manual: http://manual-snort-org.s3-website-us-east-1.amazonaws.com/node29.html. Some common modifiers include:

`nocase`

This modifier is used for case-insensitive text strings and will not apply to hex values.

`depth`

This modifier defines how far into a packet the match must be located. A depth of six would tell Snort to check the first six bytes of the payload.

`offset`

This modifier determines where to start searching for a pattern. An offset of 20 would tell Snort to check for the content after the first 20 bytes of the payload.

`http_uri`

This modifier will only match the content field if it appears in the NORMALIZED Request URI field.

`http_stat_code`

This modifier restricts the search to the extracted Status Code field from an HTTP server response.

`file_data`

This is a special mode that applies to HTTP and SMTP traffic. The Snort engine will search for the content inside HTTP response bodies and decoded MIME attachments in email streams.

As detailed earlier, several other options can be applied and rules can have multiple content matches with multiple modifiers.

:interrobang: Question 1.  Submit a screenshot of your badge demonstrating the completion of this immersivelab module.

## Snort Rules: Ep.2 – DNS

The below language is simply pulled from www.immersivelabs.com for your convenience. Please, read the information below and complete the [Snort Rules: Ep.2 – DNS](https://immersivelabs.online/labs/snort-rules-episode-2-dns/category/defensive/series/snort) lab on immersivelabs.

Malware operators will use a combination of IP addresses and domain names when creating their C2 infrastructure. These are often shared in intelligence reports and threat feeds or generated by internal IR/SOC Teams. Creating Snort rules to alert on known bad domain names is a good way of detecting threats early in their life cycle.

DNS Overview
The DNS operates primarily on UDP port 53. The client issues a single UDP request to the server, which responds with a single UDP reply.

There are a few exceptions when the DNS will instead use TCP port 53:

If the response is greater than 512 bytes
Tasks like zone transfers
Explicitly set by the DNS operator
When writing rules for DNS entries, it's important to understand how they appear in a packet. As an example, a content match of www.google.com will not work. There are no periods in the DNS; instead, each part of the domain name is prepended by the number of characters within that part (the length).

So a DNS packet for www.google.com would appear as follows:

`0377777706676f6f676c6503636f6d00`

This is an important distinction, as a Snort rule with `content: “www.google.com”;` will not match these DNS requests. However, content: “|03|www|06|google|03|com|00|”; or content: `“|03 77 77 77 06 67 6f 6f 67 6c 65 03 63 6f 6d 00|”;` will produce a match

:interrobang: Question 2.  Submit a screenshot of your badge demonstrating the completion of this immersivelab module.

## Snort Rules: Ep.3 – HTTP

The below language is simply pulled from www.immersivelabs.com for your convenience. Please, read the information below and complete the [Snort Rules: Ep.3 – HTTP](https://immersivelabs.online/labs/snort-rules-episode-3/category/defensive/series/snort) lab on immersivelabs.

HTTP is a well-documented and structured protocol. This means it is relatively easy to write signatures for specific HTTP requests, as we know where in the packet each element will lie.

Snort has a series of pre-processors that will attempt to parse all the elements from an HTTP request to make writing these rules easier. 

These examples will use the following URI as their test case:

GET https://immersivelabs.co.uk/path/to/filename?queryname=thisisthedata HTTP/1.1\r\n

### http_method

The **http_method** modifier specifies that the match must only appear in the ‘method’ portion of the request.

`content: “GET”; http_method;`

### http_uri / http_raw_uri

These modifiers work on the URI of the request. The **http_raw_uri** modifier works on the raw version (the same way it appears in the packet). The **http_uri** modifier attempts to normalize the URI string with techniques like URI decoding. The URI is the identifier that maps to files on a server.

`content:”immersive”; http_raw_uri;`

`content:”immersive”; http_uri;`

### http_header / http_raw_header

The **http_header** keyword is a content modifier that restricts the search to the extracted header fields of an HTTP client request or an HTTP server response.

Snort version 3, which we will cover in a future episode, can match content in a specific header field by name. In Snort 2.x, you need to specify the full header line.

An example of a User-Agent header match is as follows:

`content: “User-Agent: Mozilla/5.0\r\n”; http_header`

### http_client_body

The **http_client_body** keyword is a content modifier that restricts the search to the body of an HTTP client request. For example, this would be useful to detect content in outgoing HTTP POST requests.

### file_data

This specifies that the match must be made against the body of the response object. It will be dechunked and uncompressed if an HTTP stream is detected. This modifier appears before the content match, for example `file_data; content: “immersive”;`.

There are several other modifiers and the Snort manual contains detailed information and examples for each of them.

### Other modifiers

http_cookie limits the search to look for the cookie header value of an HTTP request/response.

**http_raw_cookie** operates similarly to http_cookie but specifically looks for the unnormalised cookie header value of an HTTP request/response.

**http_stat_code** limits the search to the ‘Status Message' value of an HTTP request/response.

**http_encode** limits the search based on the encoding type of the HTTP request/response.

**uricontent** limits the search based on the normalized request URI field.

**urilen** limits the search based on the length (exact length, minimum/maximum length, or range of URI lengths) to match.

These modifiers can also be combined and used alongside standard modifiers like `within`, `depth` etc. The order of content and modifiers must be correct. If the sequence is wrong, the match will not trigger an alert, even if the content is correct.

:interrobang: Question 3.  Submit a screenshot of your badge demonstrating the completion of this immersivelab module.

## Part 4. Submission

Convert your answer document in to a **.PDF** and upload a single `lastname_lab4.pdf` answer document containing all of your answers to the assignment questions to Sakai through the attachment uploads option.
