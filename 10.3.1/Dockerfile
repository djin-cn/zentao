FROM php:5.6-apache
ADD zentaopms/ /var/www/html/zentao/
COPY wordimage/ /var/www/html/zentao/www/js/ueditor/dialogs/wordimage
RUN cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini \
&& docker-php-ext-install -j$(nproc) pdo_mysql \
&& sed -ri -e 's/;session.save_path/session.save_path/g' /usr/local/etc/php/php.ini \
&& chmod o=rwx -R /var/www/html/zentao/tmp/ \
&& chmod o=rwx -R /var/www/html/zentao/www/data \
&& sed -rie "s/\`content\` text NOT NULL,/\`content\` mediumtext NOT NULL,/g" /var/www/html/zentao/db/zentao.sql \
&& sed -rie "s/'help'/'help', 'wordimage'/g" /var/www/html/zentao/module/common/view/ueditor.html.php \
&& sed -rie "s/die\(json_encode\(array\('state' => 'SUCCESS', 'url' => \\\$url\)\)\);/die(json_encode(array('state' => 'SUCCESS', 'url' => \\\$url, 'original' => \\\$file['title'], 'title' => \\\$file['title'])));/g" /var/www/html/zentao/module/file/control.php \
&& sed -rie "s/inputXssFilter: true/inputXssFilter: false/g" /var/www/html/zentao/www/js/ueditor/ueditor.config.js
#&& sed -rie "s/xssFilterRules: true/xssFilterRules: false/g" /var/www/html/zentao/www/js/ueditor/ueditor.config.js \
#&& sed -rie "s/inputXssFilter: true/inputXssFilter: false/g" /var/www/html/zentao/www/js/ueditor/ueditor.config.js \
#&& sed -rie "s/outputXssFilter: true/outputXssFilter: false/g" /var/www/html/zentao/www/js/ueditor/ueditor.config.js
