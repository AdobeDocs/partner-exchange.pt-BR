---
title: Importação em tempo real
description: Saiba como importar dados para o AEP em tempo real.
exl-id: 0b6215a9-1160-49ae-8aa5-302b47357200
TQID: https://experienceleague.adobe.com/GvWcwNPjQdmdKSUkwvJ2EpoCKJHGvf5c1Kn4dwWRVi8
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
source-git-commit: 6698ae880d1ad13a9387cb1ba66b9ba152d1d407
workflow-type: tm+mt
source-wordcount: 642
ht-degree: 4%

---

# Transmitir dados para o AEP

O Adobe [!DNL Experience Platform] permite que os eventos de perfil e experiência sejam transmitidos e disponibilizados em tempo quase real. Todos os dados enviados para o AEP por transmissão são mantidos no data lake. Os dados podem ser transmitidos para conjuntos de dados existentes ou para conjuntos de dados totalmente novos por meio de APIs ou usando o Adobe Launch.

Este artigo abordará o seguinte:

* Transmissão para o perfil individual XDM
* Transmissão para o ExperienceEvent XDM
* Uso da extensão do AEP no Launch para transmissão

A [coleção do Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) é referenciada em todo o artigo usando as chamadas associadas por número. Mais detalhes sobre como instalar e usar a coleção do Postman estão disponíveis na página Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md). Também há exemplos de conjuntos de dados de [fidelidade](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) e [perfil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json).

## Pré-requisitos

* [Autenticar na plataforma](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html).
* Obtenha os valores dos cabeçalhos necessários no tutorial de autenticação vinculado acima.

## Criar uma conexão de streaming

Para transmitir para o AEP, primeiro você deve criar uma conexão de transmissão. As conexões de transmissão contêm atributos como a fonte de dados de transmissão e se você está enviando ou não registros que pertencem aos esquemas [!DNL Experience Data Model] (XDM). Depois de criar uma conexão de transmissão, você recebe um URL exclusivo que usa para transmitir dados para o AEP.

Acesse [aqui](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/create-streaming-connection.html) para obter instruções sobre como criar uma conexão de streaming pela API ou [aqui](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/create-streaming-connection-ui.html) para obter instruções sobre como criar uma conexão de streaming pela interface.

```json
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample name",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }
```

Resposta:

```json
 {
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

Certifique-se de salvar a ID fornecida na resposta acima para futuras chamadas de assimilação de streaming (a coleção do Postman salvará isso para você na variável de ambiente CONNECTION_ID).

## Transmitir dados de perfil para o AEP

Para esta seção, use as pastas de chamadas do Postman: 3: Importação em tempo real, 3a: Importação em tempo real para dados de PERFIL.

Solicitações JSON detalhadas com respostas para dados de perfil de streaming estão documentadas [aqui](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/streaming-record-data.html).

Etapas:

1. Criar um esquema de perfil individual XDM
1. Definir o Descritor de identidade principal do Perfil individual XDM (chave primária)
1. Criar um conjunto de dados para Registros de Perfil individual XDM
1. Chame as APIs de assimilação de fluxo para criar um registro de perfil individual XDM
1. Recuperar o perfil recém-criado

## Transmitir eventos de experiência para o AEP

Para esta seção, use as pastas de chamadas do Postman: 3: Importação em tempo real, 3b: Importação em tempo real para dados de PERFIL.

Solicitações JSON detalhadas com respostas para dados de experiência de streaming estão documentadas [aqui](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/streaming-time-series-data.html).

Etapas:

1. Criar um esquema XDM ExperienceEvent
1. Definir o Descritor de identidade principal para XDM ExperienceEvent (chave primária)
1. Criar um conjunto de dados para XDM ExperienceEvents
1. Chame as APIs de assimilação de fluxo para criar um ExperienceEvent XDM
1. Recuperar o evento recém-criado

## Usar tags do Experience Platform para transmitir para o AEP

A extensão do Adobe [!DNL Experience Platform] Launch fornece uma maneira de transmitir para o AEP por meio do Launch. Para saber mais, consulte [este guia](https://docs.adobe.com/content/help/pt-BR/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html).

## Artigos de referência

* [APIs de assimilação de dados](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/acpdr/swagger-specs)
* [Visão geral da assimilação de fluxo](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/streaming_ingest/streaming_ingest_overview.md)
* [Guia do desenvolvedor de assimilação de streaming](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/streaming_ingest/getting_started_with_platform_streaming_ingestion.md)
* [Uso da extensão Launch para AEP](https://docs.adobe.com/content/help/pt-BR/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)
