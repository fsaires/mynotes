## WORDPRESS

- Atualizar URLs para rodar wordpress local

```
UPDATE wp_options SET option_value = 'http://{localhost_url}/' WHERE option_name IN ('home', 'siteurl');
```
