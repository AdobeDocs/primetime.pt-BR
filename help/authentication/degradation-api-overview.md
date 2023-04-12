---
title: Visão geral da API de degradação
description: Visão geral da API de degradação
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Visão geral da API de degradação {#degradation-api-overview}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Informações gerais {#general_info}

>[!NOTE]
>
>Essa API não está disponível em geral. Entre em contato com o representante do Adobe para obter atualizações de disponibilidade.

Esse recurso fornece a qualquer uma das três partes principais em uma integração (Programadores, MVPDs e Adobe) a capacidade de ignorar temporariamente pontos de extremidade específicos de autenticação e autorização do MVPD. Geralmente, é o Programador que inicia tal ação, mas independentemente de quem aciona um evento de degradação, a ação depende de acordos previamente acordados com os MVPDs afetados.

O principal caso de uso desse recurso ocorre durante esportes ao vivo ou eventos grandes. Em tais cenários de tráfego alto, é possível que a carga em um terminal MVPD específico se torne muito alta, resultando em tempos de resposta muito longos para os usuários. Para preservar uma boa experiência do usuário durante esse cenário, o Programador pode decidir acionar uma regra de degradação que possa autenticar/autorizar automaticamente usuários temporariamente, ou desativar um MVPD removendo-o da lista de MVPDs disponíveis.

Uma regra de degradação é aplicada somente por um período fixo. Embora os principais clientes desse recurso sejam canais de esportes e canais de notícias ao vivo, qualquer Programador pode querer ter acesso a esse recurso, já que os serviços de MVPDs ficam inativos de tempos em tempos.

Notas de degradação:

* Esse recurso foi projetado para ser usado junto com a API de monitoramento de uso, que fornece informações em tempo real sobre o número de autenticações e autorizações por MVPD, latência média de autorização e outras métricas necessárias para uma visão geral completa do serviço.
* Este recurso não permite ignorar o serviço de autenticação Adobe Primetim. Se a autenticação do Primetime estiver inativa, não há nenhum mecanismo no serviço que possa ser usado para permitir que os usuários vejam o conteúdo. Os sites ou aplicativos podem, no entanto, rotear pela autenticação do Primetime por si mesmos.
* Atualmente, o Adobe não acionará a degradação diretamente - a decisão deve sempre ficar com um programador específico que tenha concordado com essas condições com MVPDs. No futuro, a autenticação do Primetime pode ser pró-ativa no acionamento das regras de degradação se os contratos (proteção de SLA) puderem ser alcançados com MVPDs.

<!--
## Related Information {#related}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->