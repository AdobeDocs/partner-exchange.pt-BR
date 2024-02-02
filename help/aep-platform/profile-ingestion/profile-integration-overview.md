---
title: "[!DNL Platform] Visão geral do Guia de integração de acesso e assimilação de perfis"
description: Saiba mais sobre a integração do [!DNL Experience Platform] assimilação e acesso ao perfil.
exl-id: a593511c-dd4c-4437-af73-f44d795cacb8
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Guia de integração: [!DNL Experience Platform] assimilação e acesso ao perfil

Os parceiros devem usar este guia de integração para ajudá-los a desenvolver a funcionalidade de entrada e saída com o Adobe [!DNL Experience Platform] (AEP) (em inglês). Há APIs para assimilação em lote, assimilação por transmissão e acesso ao perfil unificado (saída).

Para ajudar no desenvolvimento, uma [Coleção Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) foi criado pela equipe do Adobe Exchange. Essa coleção do Postman é mencionada em todo o guia de integração.

Mais detalhes sobre como instalar e usar a coleção do Postman estão disponíveis no GitHub [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) página. Também há exemplos de conjuntos de dados de [fidelização](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) e [perfil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) dados.

## Exemplo de caso de uso de integração: sistema de resposta de voz interativa

Para integradores, o [!DNL Experience Platform] As APIs fornecem todos os recursos da plataforma oferecidos na interface do usuário, mas agora com a capacidade de criar workflows de clientes e fluxos de dados automatizados. Como integrador, você verifica periodicamente o status dos conjuntos de dados, configura novos procedimentos de assimilação de dados e integra sua própria solução de ativação de público-alvo ao Perfil unificado.

Considere o mundo dos sistemas de Resposta de Voz Interativa (IVR) e o software de gerenciamento da central de atendimento. O fornecedor pode usar o [!DNL Experience Platform] APIs para assimilar informações históricas da atividade da central de atendimento do cliente no Experience Data Lake. Se os dados forem assimilados no XDM `ExperienceEvent` Esquema (um esquema que expressa as interações do cliente), essas interações podem ser assimiladas sem atrito diretamente no Unified Profile Service. Neste caso, o `callerId` é usado como o identificador do cliente. O serviço de identidade cuidará da resolução de identidades e ajudará o Serviço de perfil unificado a adicionar quaisquer pontos de dados de interações recentes com a central de atendimento ao perfil do cliente.

Na próxima vez que um cliente ligar para a central de atendimento, ele será atendido primeiro pelo IVR. Para personalizar a mensagem e entregar uma oferta personalizada para o chamador, o sistema IVR precisa entender mais sobre o chamador. É aqui que entra a integração da API com o Perfil unificado. O back-end do IVR pode entrar em contato com o Serviço de Perfil Unificado para obter uma pesquisa por ponto. Em seguida, consulte os atributos de perfil que se aplicam apenas às interações da central de atendimento ou o perfil completo do cliente, que também tem atributos para interações em outros pontos de contato. Ao combinar dados de várias fontes de dados, usando a resolução de identidade e o Perfil unificado, a central de atendimento e o provedor de IVR podem fornecer uma experiência do cliente personalizada, com suporte do Adobe [!DNL Experience Platform].&quot;

## Recursos gerais

* AEP [Documentação do produto](https://docs.adobe.com/content/help/en/experience-platform/landing/documentation/overview.html).
* AEP [Extensibilidade](https://www.adobe.com/insights/experience-platform-api-extensibility.html).

## Dúvidas ou feedback?

Envie todas as perguntas e comentários pelo [canal de suporte](https://adobeexchangeec.zendesk.com/hc/pt-br/requests/new)
