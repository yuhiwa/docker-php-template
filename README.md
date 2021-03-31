# docker-php-templeate

# prepare directory
```
mkdir -p ~/test-www/html/test/frontend/web
mkdir -p ~/test-www/html/test/backend/web
```

# put something test php file
```
echo '<?php phpinfo();' > ~/test-www/html/test/frontend/web/test.php
echo '<?php phpinfo();' > ~/test-www/html/test/backend/web/test.php
```

# build
```
docker-compose build
```

# up
```
docker-compose up -d
```




