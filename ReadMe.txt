Набор правил для .htaccess

# использование кеша браузеров (нужен включенный mod_expires на сервере - по умолчанию выкл)
<IfModule mod_expires.c>
  ExpiresActive on

# Задаем значение по умолчанию (для всех файлов)
  ExpiresDefault                          "access plus 1 month"

# cache.appcache нельзя кэшировать в FF 3.6 (спасибо Remy ~Introducing HTML5)
  ExpiresByType text/cache-manifest       "access plus 0 seconds"

# Ваш html документ
  <FilesMatch \.(html|xhtml|xml|shtml|phtml|php|txt)$>
    ExpiresDefault "access plus 0 seconds"
  </FilesMatch>
  ExpiresByType text/html                 "access plus 0 seconds"

# Данные
  ExpiresByType text/xml                  "access plus 0 seconds"
  ExpiresByType application/xml           "access plus 0 seconds"
  ExpiresByType application/json          "access plus 0 seconds"

# Рассылка
  ExpiresByType application/rss+xml       "access plus 1 hour"
  ExpiresByType application/atom+xml      "access plus 1 hour"

# Favicon (не может быть переименован)
  <FilesMatch \.(ico)$>
    ExpiresDefault "access plus 1 week"
  </FilesMatch>
  ExpiresByType image/x-icon              "access plus 1 week"

# Медиа: изображения, видео, аудио
  <FilesMatch \.(gif|png|jpg|jpeg|ogg|mp4|mkv|flv|swf|wmv|asf|asx|wma|wax|wmx|wm)$>
    ExpiresDefault "access plus 1 year"
  </FilesMatch>
  ExpiresByType image/gif                 "access plus 1 month"
  ExpiresByType image/png                 "access plus 1 month"
  ExpiresByType image/jpeg                "access plus 1 month"
  ExpiresByType video/ogg                 "access plus 1 month"
  ExpiresByType audio/ogg                 "access plus 1 month"
  ExpiresByType video/mp4                 "access plus 1 month"
  ExpiresByType video/webm                "access plus 1 month"

# HTC файлы (css3pie)
  ExpiresByType text/x-component          "access plus 1 month"

# Веб-шрифты
  <FilesMatch \.(eot|ttf|otf|svg|woff)$>
    ExpiresDefault "access plus 1 year"
  </FilesMatch>
  ExpiresByType application/x-font-ttf    "access plus 1 month"
  ExpiresByType font/opentype             "access plus 1 month"
  ExpiresByType application/x-font-woff   "access plus 1 month"
  ExpiresByType image/svg+xml             "access plus 1 month"
  ExpiresByType application/vnd.ms-fontobject "access plus 1 month"

# CSS и JavaScript
  <FilesMatch \.(css|js)$>
    ExpiresDefault "access plus 1 year"
  </FilesMatch>
  ExpiresByType text/css                  "access plus 1 year"
  ExpiresByType application/javascript    "access plus 1 year"

# Статичные ресурсы
  <FilesMatch \.(swf|pdf|doc|rtf|xls|ppt)$>
    ExpiresDefault "access plus 1 year"
  </FilesMatch>
  ExpiresByType application/x-shockwave-flash "access plus 1 year"
  ExpiresByType application/pdf               "access plus 1 year"
  ExpiresByType application/msword            "access plus 1 year"
  ExpiresByType application/rtf               "access plus 1 year"
  ExpiresByType application/vnd.ms-excel      "access plus 1 year"
  ExpiresByType application/vnd.ms-powerpoint "access plus 1 year"
</IfModule>


# ----------------------------------------------------------------------
# Удаление ETag + Cache-Control
# ----------------------------------------------------------------------
# FileETag None бывает не достаточно (для некоторых серверов).
<IfModule mod_headers.c>
  Header unset ETag
  # Так как мы посылаем expires заголовки с большим сроком,
  # мы не используем ETag для статичного контента.
  #   http://developer.yahoo.com/performance/rules.html#etags
  FileETag None

  ## Браузер должен обновлять документ после заданного в секундах времени, которое задается в Cache-Control.
  <FilesMatch \.(html|xhtml|xml|shtml|phtml|php|txt)$>
    Header set Cache-Control "max-age=0, private, must-revalidate"
  </FilesMatch>
  <FilesMatch \.(ico|gif|png|jpg|jpeg|ogg|mp4|mkv|flv|swf|wmv|asf|asx|wma|wax|wmx|wm)$>
    Header set Cache-Control "max-age=31556926, public"
  </FilesMatch>
  <FilesMatch \.(eot|ttf|otf|svg|woff)$>
    Header set Cache-Control "max-age=31556926, public"
  </FilesMatch>
  <FilesMatch \.(css|js)$>
    Header set Cache-Control "max-age=31556926, public"
  </FilesMatch>
  <FilesMatch \.(swf|pdf|doc|rtf|xls|ppt)$>
    Header set Cache-Control "max-age=31556926, public"
  </FilesMatch>
</IfModule>