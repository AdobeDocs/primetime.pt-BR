---
title: Casos de uso
description: Casos de uso no monitoramento de simultaneidade.
source-git-commit: ac0c15b951f305e29bb8fa0bd45aa2c53de6ad15
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---


# Casos de uso {#use-cases}

O principal caso de uso do Serviço de contagem de fluxo é contar o número de fluxos de vídeo simultâneos assistidos por um usuário e fornecer uma decisão sobre o uso simultâneo para a mesma id de conta.

Para monitorar o uso pelo assinante, é necessário um serviço centralizado que possa agregar a atividade do usuário independentemente de ela ocorrer no site ou aplicativo do programador, no portal de conteúdo do MVPD ou em uma propriedade sindicalizada.

Os principais casos de uso compatíveis com esse serviço centralizado devem ser:

1. Assim que um assinante começar a assistir a um vídeo, o aplicativo poderá **inicializar uma sessão de transmissão** e iniciar **atividade de relatórios** dados.
1. No mesmo serviço central, outra instância receberá ***Decisões do CM*** - caso o aplicativo tenha uma ou mais políticas registradas no serviço CM, o serviço responderá com uma decisão de acesso com base na atividade atual.


## Criação de uma sessão {#create-session}

Essa chamada de API permite que o cliente crie uma nova sessão CM quando o usuário pressionar o botão &quot;reproduzir&quot; para assistir algum conteúdo. A resposta do servidor conterá o novo URL de fluxo (contendo a ID de fluxo) para mantê-lo ativo e o tempo em que o fluxo expirará. Espera-se que o aplicativo cliente relate a atividade pelos heartbeats. A chamada de inicialização de sessão deve incluir metadados na forma de pares de chave/valor enviados como dados de formulário (ou parâmetros de sequência de consulta). Além disso, a resposta também incluirá um sinalizador para indicar se a reprodução é &quot;compatível com a política&quot;. Se não estiver, a reprodução não será permitida.

## Atividade de relatórios {#reporting-activity}

Depois que uma sessão é criada, o aplicativo precisa enviar heartbeats regularmente para que esse fluxo permaneça ativo. Além disso, é recomendável que o aplicativo cliente pare o fluxo assim que o usuário interromper a reprodução, para que o fluxo não conte como ativo até o tempo limite.

A resposta da chamada de heartbeat pode permitir que o aplicativo cliente continue a reprodução do vídeo (quando for compatível com a política) ou pode instruí-lo a interromper a reprodução do vídeo. No caso de o fluxo de vídeo não ser compatível, o aplicativo cliente deve interrompê-lo. A resposta fornecerá informações para que o aplicativo cliente exiba uma mensagem de erro e/ou ações disponíveis para o usuário continuar a reprodução.
