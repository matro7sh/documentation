# Architecture

SMERSH uses many docker containers in its architecture, it means you have to allow few services, here is the complete list of ports to open. In addition, you will find on this page the schema composing the database.

![test](img/steup.png)

## Ports mapping
| Container | Internal port | External port |
| ------ | ----------- | ---- |
| Vulcain | 443 | 8443 |
| Api | 80 | 8000 |
| Bitwarden | 80 | 8888 |
| Db | 5432 | 5432 |
| Mercure | 443, 80, 2019 | 1337 |
| dev-tls | 80 | 80 |
| php | 9000 | None |
| CodiMD | 3000 | 3000 |
| db-codiMD | 5432 | None |

## Database

Here is the organisation of the tables within the API

![test](img/database.png){ align=left }
