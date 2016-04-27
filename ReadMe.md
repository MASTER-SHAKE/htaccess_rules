Ќаборы правил дл€ .htaccess

# использование кеша браузеров
FileETag MTime Size
<ifmodule mod_expires.c>
<filesmatch У.(jpg|jpeg|gif|png|ico|css|js)$Ф>
ExpiresActive on
ExpiresDefault Уaccess plus 1 yearФ
</filesmatch>
</ifmodule>