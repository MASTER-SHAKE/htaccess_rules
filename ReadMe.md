Набор правил для .htaccess

# использование кеша браузеров
FileETag MTime Size
<ifmodule mod_expires.c>
<filesmatch “.(jpg|jpeg|gif|png|ico|css|js)$”>
ExpiresActive on
ExpiresDefault “access plus 1 year”
</filesmatch>
</ifmodule>