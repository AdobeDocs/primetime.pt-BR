---
title: Lista de bloqueios de Clientes DRM impedidos de acessar conteúdo protegido
description: Lista de bloqueios de Clientes DRM impedidos de acessar conteúdo protegido
copied-description: true
exl-id: 74ddb5ed-4e68-4570-9cd5-bfc699609972
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# Lista de bloqueios de Clientes DRM impedidos de acessar conteúdo protegido {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

**Adobe Acesse versões do módulo DRM restritas ao acesso a conteúdo protegido.**

Especifica o cliente DRM que não pode acessar o conteúdo. Especificado pela versão e plataforma do cliente DRM.

Exemplo de caso de uso: no caso de uma falha de segurança, uma versão mais recente do cliente DRM pode ser especificada como a versão mínima necessária para a aquisição da licença e a reprodução do conteúdo. O servidor de licenças verifica se o cliente DRM que faz a solicitação de licença atende aos requisitos de versão antes de emitir uma licença. O cliente DRM também verifica a versão do DRM na licença antes de reproduzir o conteúdo. Essa verificação de cliente é necessária no caso de domínios em que uma licença pode ser transferida para outro computador.

Uma versão de cliente DRM pode ser identificada pelos atributos especificados na tabela a seguir:

| **Atributo** | **Valores suportados** | **Corresponder critérios** | **Descrição** |
|---|---|---|---|
| Ambiente | &quot;PC&quot;, &quot;PortingKit&quot; | Correspondência exata | Identifica se o cliente está sendo executado em um desktop ou em qualquer outro dispositivo. |
| SO | &quot;Win&quot;, &quot;Mac&quot;, &quot;Linux&quot;, &quot;Android&quot;, &quot;iOS&quot;, &quot;ChromeOS&quot; | Correspondência exata | Platform |
| Arquitetura | “32”, “64” | Correspondência exata | 32 ou 64 bits |
| Tipo de tela | &quot;PC&quot;, &quot;Dispositivo móvel&quot;, &quot;TV&quot; | Correspondência exata |  |
| Versão de tempo de execução | Um número de versão válido. Por exemplo, &quot;2.0.0&quot;, &quot;3.0&quot;, &quot;4.0&quot;, &quot;11.0&quot; etc. | Corresponde se a versão do cliente é inferior ou igual à versão especificada. | O número da versão é especificado como uma combinação de números e pontos (&quot;.&quot;) de qualquer comprimento. |
| Versão da biblioteca DRM | Um número de versão válido. Por exemplo, &quot;2.0.0&quot;. | Corresponde se a versão do cliente é inferior ou igual à versão especificada. | O número da versão é especificado como uma combinação de números e pontos (&quot;.&quot;) de qualquer comprimento. |
| Fornecedor OEM | Sequência de caracteres do fornecedor OEM | Correspondência exata | String de identificação do fornecedor OEM para o dispositivo que usa o kit de portabilidade. |
| Modelo | Sequência de modelo. Por exemplo, &quot;iOS_Mobile&quot;, &quot;Android_Mobile&quot;, &quot;Chrome&quot;, &quot;ChromeOS_ARM&quot;, &quot;WindowsOnARM&quot;, &quot;AVE&quot; | Correspondência exata | String de identificação do modelo do dispositivo usando o kit de portabilidade. |

>[!NOTE]
>
>Ao especificar uma entrada na lista de bloqueios, os valores podem ser definidos para um ou mais dos atributos mencionados na tabela anterior. Qualquer atributo não especificado é tratado como curinga. Se o cliente DRM corresponder a todos os valores especificados em uma entrada de lista de bloqueios, o conteúdo protegido pode não ser acessado por esse cliente.
