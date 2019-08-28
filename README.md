# Asynchronous concurrent crawler

## 1 Introduction

A multi-process asynchronous concurrent crawler, performance is not bad <br>
Current implementation:<br>
Epoll-based event module, high performance red black tree timer<br>
Asynchronous dns resolver with cache, based on redis Bloom filter<br>
Multi-process asynchronous concurrency, take full advantage of multi-core advantages, configure the number of processes, bind CPU<br>
Redis-based task queue, hashing addresses by murmur hash to achieve load balancing <br>
Asynchronous http client, supports https, currently only supports get operations, does not support cookies (planned improvements)<br>

## 2.Dependence

[http-parser](https://github.com/nodejs/http-parser) Powerful to parse url<br>
[gumbo-parser](https://github.com/google/gumbo-parser) Google's html analysis library for parsing crawled pages<br>

## 3. Compile and run

```
Git clone https://github.com/DevJasper/web-crawler.git
Cd crawler
Make
./crawlerss
```

In CentOS7, if the installation path of the dependent library is /usr/local/lib, the runtime will prompt to find the library<br>
You can set the environment variable LD_LIBRARY_PATH first, then run:<br>

```
LD_LIBRARY_PATH=/usr/local/lib ./crawler
```

You can also add /usr/local/lib directly to the default library path:<br>

```
Echo "/usr/local/lib" > /etc/ld.so.conf.d/usrlocallib.conf
Ldconfig
```

## 4.Configuration

Settings.lua is the configuration file, following the lua syntax format, field description:<br>
Work_processes is the number of processes, it is recommended to set the number of cpu cores<br>
Seed is a list of seed addresses, you can configure multiple, separated by commas<br>
