---
title: Importar dados em lote para a AEP
description: Saiba como importar arquivos em lote para o Experience Platform
exl-id: 50576b67-b3ba-498e-86f6-7e1986b76985
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Importar dados em lote para a AEP

A AEP pode assimilar arquivos em lote que contenham dados de perfil de um arquivo simples (como parquet) ou dados que estejam em conformidade com um esquema conhecido no [!UICONTROL Experience Data Model] Registro do (XDM).

A AEP pode assimilar dados usando arquivos em lote. Os seguintes formatos são aceitos: JSON, Parquet e CSV.

Este artigo abordará o seguinte:

* Pré-requisitos de assimilação em lote
* Práticas recomendadas e limites de assimilação em lote
* Como criar um lote
* Como concluir um lote
* Como verificar o status de um lote

A variável [Coleção Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) é referenciado em todo o artigo usando as chamadas associadas por número. Mais detalhes sobre como instalar e usar a coleção do Postman estão disponíveis no GitHub [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) página. Também há exemplos de conjuntos de dados de [fidelização](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) e [perfil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) dados.

Para todas as chamadas neste tutorial, use as pastas de chamadas do Postman: 4: Importação em lote, 4a: Importação em lote para dados DE PERFIL OU 4b: Importação em lote para dados DE EVENTO.

## Pré-requisitos de assimilação em lote

* Defina um esquema e crie um conjunto de dados.
* Os dados devem ser formatados em JSON, Parquet ou CSV.
* [Autenticar na plataforma](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md).
* Obtenha os valores dos cabeçalhos necessários no tutorial de autenticação vinculado acima.

## Práticas recomendadas e limites de assimilação em lote

* Tamanho máximo do lote: 100 GB
* Número máximo de arquivos por lote: 1500
* Se um arquivo tiver mais de 512 MB, ele precisará ser dividido em partes menores. Mais detalhes podem ser encontrados na [guia do desenvolvedor](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
* Número máximo de propriedades ou campos por linha: 10.000
* Número máximo de lotes por minuto, por usuário: 138

## Criar um lote

Neste tutorial, usaremos JSON como o formato. Mais exemplos de formato podem ser encontrados no [guia do desenvolvedor](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
Crie um lote usando JSON como o formato de entrada (certifique-se de incluir uma ID de conjunto de dados e de que seus dados estejam em conformidade com o esquema XDM vinculado ao conjunto de dados):

```json
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
      }'
```

Resposta:

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

## Fazer upload de arquivos

Agora os arquivos podem ser carregados no lote recém-criado (usando a batch_id da resposta acima).

```json
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

>[!NOTE]
>
>A API é compatível apenas com o upload de parte única, o que significa que cada arquivo/microlote precisará ser carregado com chamadas individuais. Verifique se o tipo de conteúdo é application/octet-stream.

Resposta:

```
200 OK
```

## Concluir um lote

Depois que todos os arquivos forem carregados, essa chamada sinalizará que o lote está pronto para promoção:

```json
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Resposta:

```
200 OK
```

## Verificar o status de um lote

O status do lote pode ser verificado na interface ou por meio da API (consulte a chamada abaixo). Para fazer check-in da interface, navegue até o DataSet para ver o status.

Os vários status de assimilação de lotes podem ser encontrados [aqui](https://adobe.ly/2TMMCmj).


```json
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

Resposta:

```json
{
    "{BATCH_ID}": {
        "imsOrg": "{IMS_ORG}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

## Artigos de referência

* [API de assimilação de dados](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/acpdr/swagger-specs)
* [Visão geral da assimilação em lote](https://docs.adobe.com/content/help/pt-BR/experience-platform/ingestion/home.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/ingest_architectural_overview.md)
* [Guia do desenvolvedor de assimilação em lote](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
* [Guia de solução de problemas de assimilação em lote](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_troubleshooting_guide.md)
* [Coleção Postman de assimilação de dados](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Data%20Ingestion%20API.postman_collection.json)
* [Tutorial de autenticação](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md)
