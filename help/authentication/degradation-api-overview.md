---
title: Visão geral da API de degradação
description: Visão geral da API de degradação
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Visão geral da API de degradação {#degradation-api-overview}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

## Informações gerais {#general_info}

>[!NOTE]
>
>Essa API geralmente não está disponível. Entre em contato com seu representante da Adobe para obter atualizações de disponibilidade.

Esse recurso fornece a qualquer uma das três principais partes em uma integração (Programadores, MVPDs e Adobe) a capacidade de ignorar temporariamente endpoints específicos de Autenticação e Autorização do MVPD. Normalmente, é o Programador que inicia essa ação, mas independentemente de quem aciona um evento de degradação, a ação depende de acordos previamente acordados com os MVPDs afetados.

O principal caso de uso desse recurso ocorre durante esportes ao vivo ou grandes eventos. Em tais cenários de tráfego alto, é possível que a carga em um endpoint de MVPD específico se torne muito alta, resultando em tempos de resposta muito longos para os usuários. Para preservar uma boa experiência do usuário durante esse cenário, o Programador pode decidir acionar uma regra de degradação que pode temporariamente autenticar/autorizar automaticamente os usuários ou desativar um MVPD, removendo-o da lista de MVPDs disponíveis.

Uma regra de degradação é aplicada somente por um período fixo. Embora os principais clientes desse recurso sejam canais de esportes e canais de notícias ao vivo, qualquer Programador pode querer ter acesso a esse recurso, já que os serviços do MVPDs ficam inativos de tempos em tempos.

Notas de degradação:

* Esse recurso foi projetado para ser usado junto com a API de monitoramento de uso, que fornece informações em tempo real sobre o número de autenticações e autorizações por MVPD, a latência média de autorização e outras métricas necessárias para obter uma visão geral completa do serviço.
* Esse recurso não permite ignorar o serviço de autenticação Adobe Primetime. Se a autenticação do Primetime estiver inativa, não há nenhum mecanismo no serviço que possa ser usado para permitir que os usuários vejam o conteúdo. No entanto, os sites ou aplicativos podem rotear para a autenticação do Primetime sozinhos.
* Atualmente, o Adobe não acionará a degradação diretamente, a decisão deve sempre residir com um Programador específico que concordou com essas condições com os MVPDs. No futuro, a autenticação do Primetime poderá ser proativa no acionamento das regras de degradação se os contratos (proteção de SLA) puderem ser alcançados com os MVPDs.

<!--
## Related Information {#related}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->
