# Criando um contexto com dados
Para rodar o FIWARE com docker-compose use:
```console
git clone https://github.com/FIWARE/tutorials.Getting-Started.git
cd tutorials.Getting-Started
git checkout NGSI-v2

docker-compose -p fiware up -d
```
## Entidades
Nossas entidades serão SERVIÇOS ou API ou Microserviços `( ex.: payments, accounts, shopping...)`
Para listas as entidades que existem, podemos usar:
```bash 
curl -iX GET 'http://localhost:1026/v2/entities'
```
Nesse momento você nao irá receber nenhuma entidade, ja que ainda nao cadastramos.

Vamos criar o primeiro microsserviço

```console
curl -iX POST \
  'http://localhost:1026/v2/entities' \
  -H 'Content-Type: application/json' \
  -d '
{
    "id": "urn:ngsi-ld:microservice:001",
    "type": "microservice",
    "team": {
        "type": "team",
        "value": {
            "name": "Team Name Accounts",
            "email": "accounts@company.com.br"
        },
        "metadata": {
            "verified": {
                "value": true,
                "type": "Boolean"
            }
        }
    },
 
    "name": {
        "type": "Text",
        "value": "Accounts_Api"
    }
}'
```
Se voce realizar novamente o get na listagem de enteidades, voce ira ver o um elemento.
Vamos cadastrar mais 2, Seguindo esse mesmo padrao.

Payments
```console
curl -iX POST \
  'http://localhost:1026/v2/entities' \
  -H 'Content-Type: application/json' \
  -d '
{
    "id": "urn:ngsi-ld:microservice:002",
    "type": "microservice",
    "team": {
        "type": "team",
        "value": {
            "name": "Team Name Paymets",
            "email": "paymets@company.com.br"
        },
        "metadata": {
            "verified": {
                "value": true,
                "type": "Boolean"
            }
        }
    },
 
    "name": {
        "type": "Text",
        "value": "Paymets_Api"
    }
}'
```
shopping
```console
curl -iX POST \
  'http://localhost:1026/v2/entities' \
  -H 'Content-Type: application/json' \
  -d '
{
    "id": "urn:ngsi-ld:microservice:003",
    "type": "microservice",
    "team": {
        "type": "team",
        "value": {
            "name": "Team Name shopping",
            "email": "shopping@company.com.br"
        },
        "metadata": {
            "verified": {
                "value": true,
                "type": "Boolean"
            }
        }
    },
 
    "name": {
        "type": "Text",
        "value": "shopping_api"
    }
}'
```

Agora se listar as entidades, teremos 3.

# Busca de entidades
Conseguimos ver uma entidede usando o id dela, dessa forma:
```console
curl -G -X GET \
   'http://localhost:1026/v2/entities/urn:ngsi-ld:microservice:001' \
   -d 'options=keyValues'
```

ou usando filtros

```console
curl -G -X GET \
    'http://localhost:1026/v2/entities' \
    -d 'type=microservice' \
    -d 'options=keyValues'
```

Ou ainda com mais subparametros 
```console
curl -G -X GET \
    'http://localhost:1026/v2/entities' \
    -d 'type=microservice' \
    -d 'q=name~=_Api' \
    -d 'options=keyValues'
```

com o `q=name~=_Api` irá aparecer 2, ou o `q=name~=_api` irá aparecer 1. propositalmente, fiz o cadastro dessa forma para mostrar essa forma de filtrar.

Ou seja, existe diferenca entre maisuculo e minúsculo.
