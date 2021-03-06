# Evmongoose([中文](https://github.com/zhaojh329/evmongoose/blob/master/README_ZH.md))

![](https://img.shields.io/badge/license-GPLV3-brightgreen.svg?style=plastic "License")

Evmongoose is an asynchronous, event based Embedded Web Server Library - It's more than an embedded webserver Library,
it is a multi-protocol embedded networking library with functions including TCP, HTTP client and server, WebSocket 
client and server, MQTT client and broker and much more. It is based on [mongoose](https://github.com/cesanta/mongoose)
and [libev](https://github.com/kindy/libev) implementation.

Evmongoose supports highly customized to extend your application. Before I started this project, I had never found a HTTP server
library that was satisfied with the event based framework, and those HTTP server libraries could only loop it'sown objects and 
could not add my own objects. For example, I want to monitor a signal or a file through the event.

# Features
* New from evmongoose
    - Using libev programming 
	- Highly customized to extend your application based on libev
	- Lua(In development)

* Inherited from mongoose
	- plain TCP, plain UDP, SSL/TLS (over TCP, one-way or two-way)
	- Alternative openssl and mbedtls
	- HTTP client, HTTP server
	- Proxy
	- WebSocket client, WebSocket server
	- MQTT client, MQTT broker
	- CoAP client, CoAP server
	- DNS client, DNS server, async DNS resolver
	- Url Rewrite

# [Example](https://github.com/zhaojh329/evmongoose/blob/master/example)
* [simplest web](https://github.com/zhaojh329/evmongoose/blob/master/example/simplest_web.c)
* [simplest web on ssl](https://github.com/zhaojh329/evmongoose/blob/master/example/simplest_web_ssl.c)
* [http client](https://github.com/zhaojh329/evmongoose/blob/master/example/http_client.c)
* [async DNS resolver](https://github.com/zhaojh329/evmongoose/blob/master/example/async_dns_resolver.c)

# How To Compile
## For Ubuntu
### Install dependency Libraries
    sudo apt install libev-dev libssl-dev
    
### Install Evmongoose(HTTPS Support Default)
    git clone https://github.com/zhaojh329/evmongoose.git
    cd evmongoose
    mkdir build
    cd build
    cmake ..
    make

### Install Evmongoose(Disable HTTPS Support)
    git clone https://github.com/zhaojh329/evmongoose.git
    cd evmongoose
    mkdir build
    cd build
    cmake .. -DHTTPS_SUPPORT=OFF
    make

## For OpenWRT/LEDE
	git clone https://github.com/zhaojh329/evmongoose.git
	cp evmongoose/openwrt/ openwrt_dir/package/evmongoose -r
	cd openwrt_dir
	make menuconfig
	Libraries  --->
	    Networking  --->
	        <*> evmongoose
	            Configuration  --->
	                SSl (mbedtls)  --->
	
	make package/evmongoose/compile V=s
	
# API reference manual
Evmongoose dose not change the usage of API in mongoose and libev, 
so please refer to the API Manual of [mongoose](https://docs.cesanta.com/mongoose/master) and libev.
Only one thing to notice is that mg_mgr_poll is no longer invoked when using evmongoose.

In addition, evmongoose added a new API: mg_mgr_set_loop, which is used to set libev's loop for Mgr.
If the function is not called, the Mgr will use the default loop:EV_DEFAULT.

# How To Contribute
Feel free to create issues or pull-requests if you have any problems.

**Please read [contributing.md](https://github.com/zhaojh329/evmongoose/blob/master/contributing.md)
before pushing any changes.**

# Thanks for the following project
* [mongoose](https://github.com/cesanta/mongoose)
* [libev](https://github.com/kindy/libev)

# If the project is helpful to you, please do not hesitate to star. Thank you!
