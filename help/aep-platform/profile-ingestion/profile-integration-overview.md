---
title: Visão geral do Guia de integração de acesso e assimilação de perfis do [!DNL Platform]
description: Saiba mais sobre a integração para  [!DNL Experience Platform] assimilação e acesso de perfil.
exl-id: a593511c-dd4c-4437-af73-f44d795cacb8
TQID: https://experienceleague.adobe.com/whnqurJyM4QXl5ikRvez7hpKWRDuU4onzROsUk-WeSI
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 6698ae880d1ad13a9387cb1ba66b9ba152d1d407
workflow-type: tm+mt
source-wordcount: 492
ht-degree: 1%

---

# Guia de integração: assimilação e acesso ao perfil do [!DNL Experience Platform]

Os parceiros devem usar este guia de integração para ajudá-los a criar a funcionalidade de entrada e saída com o Adobe [!DNL Experience Platform] (AEP). Há APIs para assimilação em lote, assimilação por transmissão e acesso ao perfil unificado (saída).

Para auxiliar no desenvolvimento, uma [coleção do Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) foi criada pela equipe do Adobe Exchange. Essa coleção do Postman é mencionada em todo o guia de integração.

Mais detalhes sobre como instalar e usar a coleção do Postman estão disponíveis na página Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md). Também há exemplos de conjuntos de dados de [fidelidade](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) e [perfil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json).

## Exemplo de caso de uso de integração: sistema de resposta de voz interativa

Para os integradores, as APIs do [!DNL Experience Platform] fornecem todos os recursos da plataforma oferecidos na interface do usuário, mas agora com a capacidade de criar fluxos de trabalho do cliente e fluxos de dados automatizados. Como integrador, você verifica periodicamente o status dos conjuntos de dados, configura novos procedimentos de assimilação de dados e integra sua própria solução de ativação de público-alvo ao Perfil unificado.

Considere o mundo dos sistemas de Resposta de Voz Interativa (IVR) e o software de gerenciamento da central de atendimento. O fornecedor pode usar as APIs [!DNL Experience Platform] para assimilar informações históricas da atividade da central de atendimento do cliente no Experience Data Lake. Se os dados forem assimilados no esquema XDM `ExperienceEvent` (um esquema que expressa as interações do cliente), essas interações poderão ser assimiladas sem atrito diretamente no Serviço de Perfil Unificado. Nesse caso, o `callerId` é usado como o identificador do cliente. O serviço de identidade cuidará da resolução de identidades e ajudará o Serviço de perfil unificado a adicionar quaisquer pontos de dados de interações recentes com a central de atendimento ao perfil do cliente.

Na próxima vez que um cliente ligar para a central de atendimento, ele será atendido primeiro pelo IVR. Para personalizar a mensagem e entregar uma oferta personalizada para o chamador, o sistema IVR precisa entender mais sobre o chamador. É aqui que entra a integração da API com o Perfil unificado. O back-end do IVR pode entrar em contato com o Serviço de Perfil Unificado para obter uma pesquisa por ponto. Em seguida, consulte os atributos de perfil que se aplicam apenas às interações da central de atendimento ou o perfil completo do cliente, que também tem atributos para interações em outros pontos de contato. Ao combinar dados de várias fontes de dados, usando a resolução de identidade e o Perfil Unificado, a central de atendimento e o provedor IVR podem fornecer uma experiência personalizada para o cliente, com suporte do Adobe [!DNL Experience Platform].&quot;

## Recursos gerais

* [Documentação do produto](https://docs.adobe.com/content/help/en/experience-platform/landing/documentation/overview.html) do AEP.
* [Extensibilidade](https://www.adobe.com/insights/experience-platform-api-extensibility.html) do AEP.

## Dúvidas ou feedback?

Envie todas as perguntas e comentários através do [canal de suporte](https://adobeexchangeec.zendesk.com/hc/pt-br/requests/new)
