1. install valet
2. cd valet-dir
3. mkdir current
4. yo wordpress
4. git clone git@github.com:INN/umbrella-example.git
5. gsup
6. download the sql file, through phpmyadmin/flywheel's interface
7. wp db reset
8. wp db import database.sql
9. wp search-replace example.org example.test
10. optionally: download images
11. In the repo's child theme, if there's a `package.json`, run `npm install`
