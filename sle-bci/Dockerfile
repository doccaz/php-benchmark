FROM registry.suse.com/bci/php:8

ENV my_dependencies="php8-ctype php8-iconv php8-tokenizer wget"
ENV mem_limit="1024M"

RUN set -eux; \
    sed -i s@^memory_limit.*@memory_limit=$mem_limit@g /etc/php8/cli/php.ini; \
    zypper -n in $my_dependencies; \
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
