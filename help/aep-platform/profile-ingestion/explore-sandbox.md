---
title: Acessar e explorar a sandbox da AEP
description: Saiba como acessar e explorar a sandbox da Experience Platform.
exl-id: 62c21615-4b03-4900-a1ad-8f809c836491
TQID: https://experienceleague.adobe.com/A5sl-xNZBPjIKn6HO1iwM78IaQWQs4yBgbw9wwpMrGw
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
feature_v2: id: fdbb8fc9-ffa3-4b86-88fe-aa4c5a3e1bc6
subfeature_v2: id: b75843fa-0a67-4a44-a6b1-cc627b0481dcid: fef08361-6ac5-460c-93fe-d063e40b6a49
topic_v2: id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: eddd9b14-83bd-4ff4-9072-54a4a484abb7id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 6698ae880d1ad13a9387cb1ba66b9ba152d1d407
workflow-type: tm+mt
source-wordcount: 772
ht-degree: 1%

---

# Acessar e explorar a sandbox da AEP

Este artigo abrange o seguinte:

* As diferenças entre uma organização de sandbox de parceiro da Adobe Exchange existente e a sandbox compartilhada da AEP.
* Solicitação de acesso à sandbox compartilhada do AEP.
* Receber um convite por email para a sandbox compartilhada do AEP.
* Convidando novos usuários no [!DNL Admin Console].
* Navegação na interface do AEP.

Para obter uma visão geral da tecnologia de sandbox na AEP, consulte este [artigo](https://docs.adobe.com/content/help/en/experience-platform/sandbox/home.html).

## A sandbox compartilhada do AEP

Os parceiros do Exchange recebem acesso a vários produtos da Adobe [!DNL Experience Cloud] (produtos que não são da AEP, como [!DNL Analytics], [!DNL Target], tags da Platform e assim por diante) por meio de sua própria organização da Adobe [!DNL Experience Cloud] (não compartilhada). Os parceiros recebem direitos de acesso de administrador do sistema a sua própria organização para gerenciar usuários e outras permissões. O Adobe [!DNL Experience Platform] (AEP) é tratado de forma diferente das outras sandboxes da Adobe. Estas são as principais diferenças:

* O acesso ao AEP NÃO será feito por meio da principal organização de sandbox do Adobe [!DNL Experience Cloud] dos parceiros.
* O acesso ao AEP é feito por meio de uma organização compartilhada do Adobe Exchange.
* Muitas outras empresas parceiras da Adobe Exchange estão acessando o AEP usando a mesma organização
   * Por meio do recurso de sandbox da AEP, os dados e as atividades nesta organização compartilhada não podem ser vistos ou modificados pelos outros parceiros. Cada parceiro terá acesso a uma sandbox diferente na organização compartilhada.
* Os direitos de administração nesta organização compartilhada são muito limitados.
* Depois de receber acesso a uma sandbox no AEP, os parceiros verão duas organizações no alternador de organizações na parte superior direita da interface do usuário enquanto estiverem na Admin Console ou na página inicial principal do Experience Cloud. No entanto, quando conectado ao AEP, somente a organização compartilhada deverá estar visível.

## Solicitar acesso à sandbox compartilhada do AEP

Envie uma [solicitação de suporte](https://adobeexchangeec.zendesk.com/hc/pt-br/requests/new) com as seguintes informações:

* Endereço de e-mail
* Assunto: Solicitação de sandbox da AEP
* Produto: Provisionamento geral / Sandbox
* Tipo de tíquete: Suporte do programa - Perguntas sobre programa do Exchange/solicitação de provisionamento
* Descrição: forneça uma breve descrição dos casos de uso de integração que exigem o uso de uma sandbox da AEP
* Forneça também todos os nomes de usuário e emails que devem ser adicionados à sandbox do AEP. É possível que usuários adicionais sejam adicionados após a solicitação ser feita, mas os usuários precisarão ser adicionados pelo Adobe por meio de um tíquete adicional (veja abaixo).

## Receba o convite por email

O contato principal que solicitou a sandbox da AEP receberá um email automatizado convidando-o para &quot;começar&quot; com o Adobe [!DNL Experience Platform]. O contato principal também terá alguns privilégios de administração que são abordados na próxima seção.

Em vez de selecionar o botão &quot;Introdução&quot; no email, navegue diretamente para `https://platform.adobe.com.` Entre com a Adobe ID que está associada ao endereço de email no convite ou crie um se não estiver associado a uma Adobe ID.

## Convidar usuários adicionais

Envie uma [solicitação de suporte](https://adobeexchangeec.zendesk.com/hc/pt-br/requests/new) com as seguintes informações:

* Endereço de email do solicitante
* Assunto: Sandbox AEP - Adicionar administrador/usuário
* Produto: Provisionamento geral / Sandbox
* Tipo de tíquete: Suporte do programa - Perguntas sobre programa do Exchange/solicitação de provisionamento
* Descrição: Lista de usuários a serem adicionados (nomes e emails)

## Navegação na interface do usuário do AEP

Assista ao [vídeo de introdução](https://docs.adobe.com/content/help/en/platform-learn/tutorials/intro-to-platform/interface-tour.html) da interface do usuário do AEP

Há 12 áreas principais na interface do usuário do AEP que podem ser navegadas por meio do painel esquerdo. No entanto, as seções mais importantes para esse tipo de integração são Esquemas, Conjuntos de dados e Perfis.

* Página inicial - a tela de aterrissagem

   * Sugere algumas atividades de introdução
   * Fornece alguns links para o conteúdo de aprendizado
   * Fornece uma visualização de painel para alguns dos principais objetos do AEP, como Esquemas, Conjuntos de dados e Perfis

* Fluxos de trabalho - lançamento em fluxos de trabalho comuns para trazer dados para o AEP
* Conexões / Fontes - gerencie fontes de dados que entram no AEP
* Conexões / Destinos - gerencie as conexões para enviar dados a sistemas externos
* Perfis - exiba e gerencie perfis de clientes individuais
* Segmentos - navegar, criar e modificar segmentos de clientes
* Identidades - procure, crie e modifique namespaces de identidade; esses são os tipos de IDs primárias usadas para identificar exclusivamente um cliente
* Modelos (Data Science): participar de atividades de ciência de dados, incluindo o uso de um ambiente Jupyter Notebooks incorporado
* Serviços (Ciência de dados) - publique receitas de ciência de dados como serviços
* Esquemas - procurar, criar e modificar esquemas; essas são as definições de dados detalhadas usadas para manter os dados organizados
* DataSets - procure, crie e gerencie DataSets; um DataSet é definido por um Esquema e é onde os dados residem no AEP
* Consultas - procure, crie, modifique e use um repositório de consultas para obter insights dos dados nos DataSets
* Monitoramento - visualização do status de todos os dados que entram e saem do AEP para Batch e Streaming
