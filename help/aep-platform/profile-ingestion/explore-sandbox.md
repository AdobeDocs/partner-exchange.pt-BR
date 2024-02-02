---
title: Acessar e explorar a sandbox da AEP
description: Saiba como acessar e explorar a sandbox Experience Platform.
exl-id: 62c21615-4b03-4900-a1ad-8f809c836491
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 0%

---

# Acessar e explorar a sandbox da AEP

Este artigo abrange o seguinte:

* As diferenças entre uma organização de sandbox de parceiro Adobe Exchange existente e a sandbox AEP compartilhada.
* Solicitação de acesso à sandbox compartilhada da AEP.
* Recebimento de um convite por email para a sandbox compartilhada da AEP.
* Convidar novos usuários na [!DNL Admin Console].
* Navegação na interface do usuário do AEP.

Para obter uma visão geral da tecnologia de sandbox na AEP, consulte esta [artigo](https://docs.adobe.com/content/help/pt-BR/experience-platform/sandbox/home.html).

## A sandbox da AEP compartilhada

Os parceiros do Exchange recebem acesso a vários Adobe [!DNL Experience Cloud] produtos (produtos não-AEP como [!DNL Analytics], [!DNL Target], tags da Platform e assim por diante) por meio de seu próprio Adobe [!DNL Experience Cloud] Org (não compartilhado). Os parceiros recebem direitos de acesso de administrador do sistema a sua própria organização para gerenciar usuários e outras permissões. Adobe [!DNL Experience Platform] (AEP) é tratada de forma diferente das outras sandboxes Adobe. Estas são as principais diferenças:

* O acesso ao AEP NÃO será feito por meio do Adobe principal dos parceiros [!DNL Experience Cloud] sandbox Org.
* O acesso ao AEP é feito por meio de uma organização compartilhada do Adobe Exchange.
* Muitas outras empresas parceiras do Adobe Exchange estão acessando a AEP usando a mesma organização
   * Por meio do recurso Sandbox da AEP, os dados e as atividades nesta organização compartilhada não podem ser vistos ou modificados pelos outros parceiros. Cada parceiro terá acesso a uma sandbox diferente na organização compartilhada.
* Os direitos de administração nesta organização compartilhada são muito limitados.
* Após receber acesso a uma sandbox na AEP, os parceiros verão duas organizações no alternador de organizações na parte superior direita da interface do usuário, enquanto estiverem na página inicial do Admin Console ou do Experience Cloud principal. No entanto, quando conectado à AEP, somente a organização compartilhada deverá estar visível.

## Solicitar acesso à sandbox da AEP compartilhada

Enviar um [solicitação de suporte](https://adobeexchangeec.zendesk.com/hc/pt-br/requests/new) com as seguintes informações:

* Endereço de email
* Assunto: Solicitação de sandbox da AEP
* Produto: Provisionamento geral / Sandbox
* Tipo de tíquete: Suporte do programa - Perguntas sobre programa do Exchange/solicitação de provisionamento
* Descrição: forneça uma breve descrição dos casos de uso de integração que exigem o uso de uma sandbox da AEP
* Forneça também todos os nomes de usuário e emails que devem ser adicionados à sandbox da AEP. É possível que usuários adicionais sejam adicionados após a solicitação ser feita, mas os usuários precisarão ser adicionados por Adobe através de um ticket adicional (veja abaixo).

## Receba o convite por email

O contato principal que solicitou a sandbox da AEP receberá um email automatizado convidando-o para &quot;começar&quot; com o Adobe [!DNL Experience Platform]. O contato principal também terá alguns privilégios de administração que são abordados na próxima seção.

Em vez de clicar no botão &quot;Introdução&quot; no email, navegue diretamente para `https://platform.adobe.com.` Faça logon com a Adobe ID que está associada ao endereço de email no convite ou crie um se não estiver associado a uma Adobe ID.

## Convidar usuários adicionais

Enviar um [solicitação de suporte](https://adobeexchangeec.zendesk.com/hc/pt-br/requests/new) com as seguintes informações:

* Endereço de email do solicitante
* Assunto: Sandbox da AEP - Adicionar administrador/usuário
* Produto: Provisionamento geral / Sandbox
* Tipo de tíquete: Suporte do programa - Perguntas sobre programa do Exchange/solicitação de provisionamento
* Descrição: Lista de usuários a serem adicionados (nomes e emails)

## Navegação na interface do usuário do AEP

Assistir à interface do usuário do AEP [vídeo de introdução](https://docs.adobe.com/content/help/en/platform-learn/tutorials/intro-to-platform/interface-tour.html)

Há 12 áreas principais na interface do usuário do AEP que podem ser navegadas por meio do painel esquerdo. No entanto, as seções mais importantes para esse tipo de integração são Esquemas, Conjuntos de dados e Perfis.

* Página inicial - a tela de aterrissagem

   * Sugere algumas atividades de introdução
   * Fornece alguns links para o conteúdo de aprendizado
   * Fornece uma visualização de painel para alguns dos principais objetos da AEP, como Esquemas, Conjuntos de dados e Perfis

* Fluxos de trabalho - iniciar em fluxos de trabalho comuns para trazer dados para a AEP
* Conexões/Fontes - gerencie fontes de dados que entram na AEP
* Conexões / Destinos - gerencie as conexões para enviar dados a sistemas externos
* Perfis - exiba e gerencie perfis de clientes individuais
* Segmentos - navegar, criar e modificar segmentos de clientes
* Identidades - procure, crie e modifique namespaces de identidade; esses são os tipos de IDs primárias usadas para identificar exclusivamente um cliente
* Modelos (Data Science): participar de atividades de ciência de dados, incluindo o uso de um ambiente Jupyter Notebooks incorporado
* Serviços (Ciência de dados) - publique receitas de ciência de dados como serviços
* Esquemas - procurar, criar e modificar esquemas; essas são as definições de dados detalhadas usadas para manter os dados organizados
* DataSets - procure, crie e gerencie DataSets; um DataSet é definido por um Esquema e é onde os dados residem na AEP
* Consultas - procure, crie, modifique e use um repositório de consultas para obter insights dos dados nos DataSets
* Monitoramento - visualização do status de todos os dados que entram e saem da AEP para Batch e Streaming
