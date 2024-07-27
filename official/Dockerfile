FROM php:8.2-cli
ADD --chmod=0755 https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/


ENV my_dependencies="wget"
ENV mem_limit="1024M"

RUN set -eux; \
    sed -e s@^memory_limit.*@memory_limit=$mem_limit@g /usr/local/etc/php/php.ini-production > /usr/local/etc/php/php.ini; \
    apt-get update && apt-get install $my_dependencies; \
    install-php-extensions zip; \
    # additional setup steps \
    wget https://raw.githubusercontent.com/SergiX44/php-benchmark-script/master/bench.php; \
    # rand: random number generation 
    wget https://raw.githubusercontent.com/SergiX44/php-benchmark-script/master/rand.bench.php; \
    # io: file read/write/zip/unzip 
    wget https://raw.githubusercontent.com/SergiX44/php-benchmark-script/master/io.bench.php; 
    # mysql: selects, updates, deletes, transactions, ....  
    # you need to pass the args --mysql_user=xxx --mysql_password=xxx --mysql_host=xxx 
    #wget https://raw.githubusercontent.com/SergiX44/php-benchmark-script/master/mysql.bench.php    
    
CMD ["php", "bench.php", "--multiplier=10"]
