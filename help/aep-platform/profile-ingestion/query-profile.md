---
title: Acessar o perfil unificado
description: Use APIs para acessar o Perfil unificado.
exl-id: c9d2fa2d-9ffe-4e66-996f-ad930bee22c6
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Acessar o Perfil unificado usando a API de perfil

O ADOBE [!DNL Experience Platform] puder acessar o perfil do cliente em tempo real; a variável [[!DNL Experience Platform] API do Perfil do cliente em tempo real](https://adobe.ly/2TtDHWr) foi projetado para interagir com isso. Veja isto [tutorial](https://docs.adobe.com/content/help/en/experience-platform/profile/api/getting-started.html) para saber como acessar os dados de perfil do cliente em tempo real usando a API do perfil.

Este artigo fará referência substancial ao tutorial vinculado acima.

A variável [Coleção Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) é referenciado em todo o artigo usando as chamadas associadas por número. Mais detalhes sobre como instalar e usar a coleção do Postman estão disponíveis no GitHub [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) página. Também há exemplos de conjuntos de dados de [fidelização](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) e [perfil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) dados.

Para esta seção, use a pasta do Postman 5: Pesquisa de perfil, 5a: Dados de PERFIL de pesquisa em tempo real OU 5b: Dados de EVENTO de pesquisa em tempo real.

## Uso da API

As seções a seguir ajudam na autenticação para o Experience Platform. Saiba mais sobre o caminho da API, informações de cabeçalho e muito mais.

### Autenticar para [!DNL Platform]

Consulte [este](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html) tutorial de autenticação antes de fazer qualquer uma das chamadas abaixo.

### Caminho da API

O URL do gateway da plataforma necessário para a API do perfil do cliente em tempo real é: `https://platform.adobe.io/`

O caminho base para a API é: `/data/core/ups/access/entities`

Um exemplo de caminho completo é: `https://platform.adobe.io/data/core/ups/access/entities`

### Informações do cabeçalho

O cabeçalho deve incluir:

* Autorização
* x-gw-ims-org-id - obtenha por meio de console.adobe.io
* x-api-key - obtenha por meio de console.adobe.io
* x-sandbox-name - obtido do Adobe Integration Manager
* Tipo de conteúdo: application/json

Mais informações explicadas sobre o cabeçalho podem ser encontradas na [tutorial](https://adobe.ly/2PTHuKv).

## Acessar perfis de clientes em tempo real usando identidades

A API de perfil permite o acesso a Perfis que usam identidades por meio de uma solicitação GET. As seções abaixo seguirão isso [guia](https://docs.adobe.com/content/help/en/experience-platform/profile/api/entities.html).

### Acessar dados do perfil usando a identidade

A API dá acesso às informações do perfil usando a identidade. Isso é feito fazendo uma solicitação GET para /access/entities com a ID da entidade como um dos parâmetros e o namespace da ID da entidade. OBSERVAÇÃO: lembre-se de que qualquer solicitação que retorne 50 registros fornecerá apenas um status HTTP 422 e uma mensagem que lê &quot;muitas identidades relacionadas&quot; e a pesquisa precisará ser limitada com mais parâmetros.

Solicitação:

A solicitação a seguir recupera o email e o nome de um cliente usando uma identidade:

```
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Resposta:

```
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    }
}
```

### Acessar perfis por lista de identidades

A API dá acesso aos perfis que usam uma lista de identidades usando uma solicitação POST para o endpoint /access/entities e fornecendo as identidades na carga. Essas identidades consistem em um valor de ID (entityId) e um namespace de identidade (entityIdNS).

Solicitação: a solicitação a seguir recupera os nomes e endereços de email de vários clientes por uma lista de identidades:

```
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema":{
        "name":"_xdm.context.profile"
    },
    "fields":["identities","person.name","workEmail"],
    "identities":[
        {
            "entityId":"89149270342662559642753730269986316601",
            "entityIdNS":{
                "code":"ECID"
            }
        },
        {
            "entityId":"89149270342662559642753730269986316900",
            "entityIdNS":{
                "code":"ECID"
            }
        },
        {
            "entityId":"89149270342662559642753730269986316602",
            "entityIdNS":{
                "code":"ECID"
            }
        }
    ]
}'
```

Resposta: Uma resposta bem-sucedida retorna os campos solicitados das entidades especificadas no corpo da solicitação.

```
{
    "A29cgveD5y64ezlhxjUXNzcm": {
        "entityId": "A29cgveD5y64ezlhxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "05DD23564EC4607F0A490D44",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316603",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316700",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316701",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    },
    "A29cgveD5y64e2RixjUXNzcm": {
        "entityId": "A29cgveD5y64e2RixjUXNzcm",
        "sources": [
            ""
        ],
        "entity": {},
        "lastModifiedAt": "1970-01-01T00:00:00Z"
    },
    "A29cgveD5y64ezphxjUXNzcm": {
        "entityId": "A29cgveD5y64ezphxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-27T23:25:52Z"
    }
}
```

## Eventos de série temporal

Os parceiros podem acessar eventos de série temporal pela identidade da entidade de perfil associada fazendo uma solicitação GET para o endpoint /access/entities.

### Acessar eventos de série temporal para um perfil por identidade

Os eventos de série temporal são acessados pela identidade de sua entidade de perfil associada fazendo uma solicitação GET para o endpoint /access/entities. Essa identidade consiste em um valor de ID (entityId) e um namespace de identidade (entityIdNS).

Solicitação: a solicitação a seguir encontra uma entidade de perfil por ID e recupera os valores das propriedades endUserIDs, web e canal **para todos** eventos de séries temporais associados à entidade.

```
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Resposta:

Uma resposta bem-sucedida retorna uma lista paginada de eventos de série temporal e campos associados que foram especificados nos parâmetros de solicitação.

```
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236036",
        "count": 1,
        "next": "c8d11988-6b56-4571-a123-b6ce74236037"
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": 1531260476000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:49:02Z"
        }
    ],
    "_links": {
        "next": {
            "href": "/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1"
        }
    }
}
```

### Paginação para eventos de série temporal de um perfil

Os resultados são paginados ao recuperar eventos de série temporal. Se houver páginas subsequentes de resultados, o parâmetro _page.next da resposta conterá uma ID. Além disso, o parâmetro _links.next.href da resposta fornece um URI de solicitação para recuperar a página subsequente.

Solicitação:

A solicitação a seguir recupera a próxima página de resultados usando o URI _links.next.href como o caminho da solicitação.

```
curl -X GET \

  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Resposta:

Uma resposta bem-sucedida retorna a próxima página de resultados. Este exemplo demonstra uma resposta em que não há páginas subsequentes de resultados, conforme indicado pelos valores de sequência de caracteres vazios de _page.next e _links.next.href.

```
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236037",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236037",
            "timestamp": 1531260477000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:50:01Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## Artigos de referência

* [API do Perfil do cliente em tempo real](https://adobe.ly/2TtDHWr)
* [Acessar dados de perfil do cliente em tempo real usando o tutorial da API de perfil](https://docs.adobe.com/content/help/en/experience-platform/profile/api/getting-started.html)
* [[!DNL Experience Platform] Guia de autenticação](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html)
