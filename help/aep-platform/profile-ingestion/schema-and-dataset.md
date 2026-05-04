---
title: Criar esquemas e conjuntos de dados do AEP
description: Crie esquemas e conjuntos de dados na Experience Platform.
exl-id: a2773551-20a3-4a5b-ab53-60fa67e38ec0
TQID: https://experienceleague.adobe.com/uQtIQwCgsjOd5pR5w4LF634-Whvjl0jmF5WywVWlkZQ
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 6698ae880d1ad13a9387cb1ba66b9ba152d1d407
workflow-type: tm+mt
source-wordcount: 617
ht-degree: 17%

---

# Criar esquemas e conjuntos de dados

A [coleção do Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) é referenciada em todo o artigo usando as chamadas associadas por número. Mais detalhes sobre como instalar e usar a coleção do Postman estão disponíveis na página Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md). Também há exemplos de conjuntos de dados de [fidelidade](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) e [perfil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json).

## Esquemas

Um esquema é um conjunto de regras que representam e validam a estrutura e o formato dos dados. Em um alto nível, os esquemas fornecem uma definição abstrata de um objeto do mundo real (como uma pessoa) e destacam quais dados devem ser incluídos em cada instância desse objeto (como nome, sobrenome, aniversário e assim por diante). Os esquemas podem ser criados na interface ou usando as APIs [!DNL Experience Platform].

Consulte [esta documentação](https://www.adobe.io/apis/experienceplatform/home/xdm/xdmservices.html#!api-specification/markdown/narrative/technical_overview/schema_registry/schema_composition/schema_composition.md) para obter mais detalhes.

### Criar um esquema

Os parceiros podem criar um esquema usando a interface seguindo este [tutorial](https://docs.adobe.com/content/help/en/experience-platform/xdm/tutorials/create-schema-ui.html). Este exemplo usa o esquema de perfil do programa de fidelidade. Embora o exemplo seja um schema de perfil, schemas baseados em eventos podem ser usados usando um processo semelhante.

Para usar as APIs, os parceiros devem ter uma integração do Adobe I/O existente com permissões [!DNL Experience Platform] habilitadas. Consulte este manual para [criar uma integração de E/S](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md).

Em seguida, visite [este link](https://docs.adobe.com/content/help/en/experience-platform/xdm/tutorials/create-schema-api.html) para saber como criar esquemas usando a API.

Para criar um esquema por meio do Postman, use as chamadas contidas nas pastas 1: Criar esquema, 1a: Criar esquema para dados de PERFIL OU 1b: Criar esquema para dados DE EVENTO.

## Conjuntos de dados

Todos os dados trazidos para o Adobe [!DNL Experience Platform] estão contidos em conjuntos de dados. Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas) e campos (linhas). Os conjuntos de dados também contêm metadados que descrevem vários aspectos dos dados armazenados.

O Serviço de Catálogo é o sistema de registro para localização e linhagem de dados no [!DNL Experience Platform], e é usado para criar e gerenciar conjuntos de dados. O catálogo rastreia os metadados de cada conjunto de dados, o que inclui uma referência ao esquema do Experience Data Model (XDM) com o qual o conjunto de dados está em conformidade (explicado na próxima seção) e o número de registros assimilados nesse conjunto de dados.

Acesse [aqui](https://docs.adobe.com/content/help/en/experience-platform/catalog/datasets/overview.html) para obter uma visão geral detalhada do conjunto de dados.

### Criar um conjunto de dados

![Criando Gif Animado Do Conjunto De Dados](images/creating_a_dataset.gif)

<!-- 
We don't yet support hover text in images (and we render it poorly when included). I removed "Creating a Dataset" from the above image link. We can add it back when we support it (Summer 2020?) -Bob
-->

Criar um conjunto de dados por meio da interface do usuário:

1. Clique em **[!UICONTROL Criar Conjunto de Dados]**.

1. Clique em **[!UICONTROL Criar do esquema]**.

1. Clique em **[!UICONTROL Concluir]**.

Obtenha [aqui](https://docs.adobe.com/content/help/en/experience-platform/catalog/datasets/user-guide.html) um guia do usuário do conjunto de dados.

[Criar um conjunto de dados usando as APIs](https://docs.adobe.com/content/help/en/experience-platform/catalog/datasets/create.html).

Para criar um conjunto de dados por meio do Postman, use as pastas 2: Criar conjunto de dados, 2a: Criar conjunto de dados para dados do PERFIL OU 2b: Criar conjunto de dados para dados do EVENTO.

## Práticas recomendadas de esquema e conjunto de dados para parceiros

* Os dados do parceiro devem usar um esquema de perfil separado em vez de criar um mix-in para o esquema de perfil e o esquema de experiência existentes de um cliente.
* Os parceiros devem usar aulas e mixins do Adobe sempre que possível.
* Os parceiros devem fazer upload de seus dados usando um conjunto de dados separado, em vez de tentar combinar seus dados em um conjunto de dados existente.
* Os parceiros não podem fazer upload de seus esquemas para o registro global por enquanto.
