# أسلوب البناء

تم إنشاء تطبيقنا كخدمة مستقلة صغيرة ، وهنا القائمة

![test1](../img/steup.png)

## Ports mapping

| Container | Default DNS          |
| --------- | -------------------- |
| Api       | `api.{DOMAIN}`       |
| Bitwarden | `bitwarden.{DOMAIN}` |
| Client    | `{DOMAIN}`           |
| Db        | NOT EXPOSED          |
| php       | NOT EXPOSED          |
| CodiMD    | `codimd.{DOMAIN}`    |
| db-codiMD | NOT EXPOSED          |


## قاعدة البيانات

أدناه لدينا صورة توضح قاعدة البيانات

![test2](../img/database.png){ align=left }
