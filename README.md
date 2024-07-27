# php-benchmark
Simple PHP benchmark comparison between official PHP 8.2 image and SUSE's SLE-BCI:PHP8.2.

Using the bench.php script provided at https://github.com/sergix44/php-benchmark-script

## What did I change?
For both images, I set the memory_limit variable in php.ini to 1GB and call the bench.php script with a multipler of 10x (runs the tests 10 times in a row).
For SLE-BCI, I installed the additional packages: php8-ctype php8-iconv php8-tokenizer
For PHP 8.2, I installed the zip extension (required by one of the benchmarks).


## Building the images

```
# docker build official -t ericosuse/phpdemo-official:latest
# docker build sle-bci -t ericosuse/phpdemo-slebci:latest
```

Official PHP 8 image can be found here: https://hub.docker.com/_/php
SLE-BCI image can be found here: https://registry.suse.com/repositories/bci-php


## Running the benchmark

For the official PHP 8.2 image:
```
# docker run -it ericosuse/phpdemo-official
-------------------------------------------------------
|       PHP BENCHMARK SCRIPT v.2.0 by @SergiX44       |
-------------------------------------------------------
PHP............................................. 8.2.21
Platform......................................... Linux
Arch............................................ x86_64
Server.................................... 5fb73a2ea04d
Max memory usage................................. 1024M
OPCache status................................ disabled
OPCache JIT....................... disabled/unavailable
PCRE JIT....................................... enabled
XDebug extension.............................. disabled
Difficulty multiplier.............................. 10x
Started at..................... 27/07/2024 21:12:31.616
-------------------------------------------------------
math.......................................... 1.1428 s
loops......................................... 0.8298 s
ifelse........................................ 1.2633 s
switch........................................ 0.9226 s
string........................................ 2.5610 s
array......................................... 3.8685 s
regex......................................... 1.7500 s
is_{type}..................................... 1.4631 s
hash.......................................... 1.0083 s
json.......................................... 1.6336 s
-----------------Additional Benchmarks-----------------
io::file_read................................. 0.0536 s
io::file_write................................ 0.0940 s
io::file_zip.................................. 0.7055 s
io::file_unzip................................ 0.2174 s
rand::rand.................................... 0.1840 s
rand::mt_rand................................. 0.1819 s
rand::random_int.............................. 2.3839 s
rand::random_bytes............................ 2.4141 s
rand::openssl_random_pseudo_bytes............. 6.8601 s
-------------------------------------------------------
Total time................................... 29.5373 s
Peak memory usage................................ 2 MiB
```


For SLE-BCI with PHP 8.2:
```
# docker run -it ericosuse/phpdemo-slebci
-------------------------------------------------------
|       PHP BENCHMARK SCRIPT v.2.0 by @SergiX44       |
-------------------------------------------------------
PHP............................................. 8.2.20
Platform......................................... Linux
Arch............................................ x86_64
Server.................................... 27f0983ea32e
Max memory usage................................. 1024M
OPCache status................................ disabled
OPCache JIT....................... disabled/unavailable
PCRE JIT....................................... enabled
XDebug extension.............................. disabled
Difficulty multiplier.............................. 10x
Started at..................... 27/07/2024 21:15:32.915
-------------------------------------------------------
math.......................................... 1.1290 s
loops......................................... 0.8232 s
ifelse........................................ 1.2664 s
switch........................................ 0.8814 s
string........................................ 2.5484 s
array......................................... 3.9309 s
regex......................................... 1.7790 s
is_{type}..................................... 1.3936 s
hash.......................................... 0.9934 s
json.......................................... 1.8955 s
-----------------Additional Benchmarks-----------------
io::file_read................................. 0.0270 s
io::file_write................................ 0.0902 s
io::file_zip.................................. 0.6381 s
io::file_unzip................................ 0.2129 s
rand::rand.................................... 0.1697 s
rand::mt_rand................................. 0.1748 s
rand::random_int.............................. 2.3333 s
rand::random_bytes............................ 2.3705 s
rand::openssl_random_pseudo_bytes............. 5.1213 s
-------------------------------------------------------
Total time................................... 27.7784 s
Peak memory usage................................ 2 MiB
```

## Conclusions

Even though the timings are almost the same for both, SLE-BCI offers slightly faster I/O and random number generation, beating the official image by almost 2 seconds.
The size of the images, however, are VERY different:

```
# docker images
REPOSITORY                            TAG               IMAGE ID       CREATED             SIZE
ericosuse/phpdemo-official            latest            4d9465734fd4   31 minutes ago      531MB
ericosuse/phpdemo-slebci              latest            2efe25590966   54 minutes ago      180MB
```

Both images are available at Docker Hub:

* https://hub.docker.com/repository/docker/ericosuse/phpdemo-slebci
* https://hub.docker.com/repository/docker/ericosuse/phpdemo-official

