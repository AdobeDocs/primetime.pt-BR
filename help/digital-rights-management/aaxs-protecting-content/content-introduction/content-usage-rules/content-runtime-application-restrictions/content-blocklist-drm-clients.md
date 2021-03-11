---
title: Lista de bloqueios de clientes DRM impedidos de acessar conteúdo protegido
description: Lista de bloqueios de clientes DRM impedidos de acessar conteúdo protegido
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---


# Lista de bloqueios de clientes DRM que impedem o acesso a conteúdo protegido {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

**Adobe Access DRM versões restritas do módulo acesso a conteúdo protegido.**

Especifica o cliente DRM que não pode acessar o conteúdo. Especificado pela versão e plataforma do cliente DRM.

Exemplo de caso de uso: Em caso de violação de segurança, uma versão mais recente do cliente DRM pode ser especificada como a versão mínima necessária para a aquisição de licença e a reprodução de conteúdo. O servidor de licenças verifica se o cliente DRM que faz a solicitação de licença atende aos requisitos de versão antes de emitir uma licença. O cliente DRM também verifica a versão do DRM na licença antes de reproduzir o conteúdo. Essa verificação de cliente é necessária no caso de domínios em que uma licença pode ser transferida para outra máquina.

Uma versão do cliente DRM pode ser identificada pelos atributos especificados na tabela a seguir:

| **Atributo** | **Valores compatíveis** | **Corresponder aos critérios** | **Descrição** |
|---|---|---|---|
| Ambiente | &quot;PC&quot;, &quot;PortingKit&quot; | Correspondência exata | Identifica se o cliente está sendo executado em um desktop ou qualquer outro dispositivo. |
| SO | &quot;Win&quot;, &quot;Mac&quot;, &quot;Linux&quot;, &quot;Android&quot;, &quot;iOS&quot;, &quot;ChromeOS&quot; | Correspondência exata | Plataforma |
| Arquitetura | &quot;32&quot;, &quot;64&quot; | Correspondência exata | 32 bits ou 64 bits |
| Tipo de tela | &quot;PC&quot;, &quot;Mobile&quot;, &quot;TV&quot; | Correspondência exata |  |
| Versão do tempo de execução | Um número de versão válido. Por exemplo, &quot;2.0.0&quot;, &quot;3.0&quot;, &quot;4.0&quot;, &quot;11.0&quot;, etc. | Corresponde se a versão do cliente é menor ou igual à versão especificada. | O número da versão é especificado como uma combinação de números e pontos (&quot;.&quot;) de qualquer comprimento. |
| Versão da biblioteca DRM | Um número de versão válido. Por exemplo, &quot;2.0.0&quot;. | Corresponde se a versão do cliente é menor ou igual à versão especificada. | O número da versão é especificado como uma combinação de números e pontos (&quot;.&quot;) de qualquer comprimento. |
| Fornecedor OEM | Sequência de caracteres do fornecedor OEM | Correspondência exata | Sequência de identificação do fornecedor OEM para o dispositivo que usa o kit portátil. |
| Modelo | Sequência de caracteres do modelo. Por exemplo, &quot;iOS_Mobile&quot;, &quot;Android_Mobile&quot;, &quot;Chrome&quot;, &quot;ChromeOS_ARM&quot;, &quot;WindowsOnARM&quot;, &quot;AVE&quot; | Correspondência exata | Sequência de identificação do modelo de dispositivo para o dispositivo que usa o kit de porta. |

>[!NOTE]
>
>Ao especificar uma entrada na lista de bloqueios, os valores podem ser definidos para um ou mais atributos mencionados no quadro anterior. Qualquer atributo que não seja especificado é tratado como curinga. Se o cliente DRM corresponder a todos os valores especificados em uma entrada de lista de bloqueios, o conteúdo protegido pode não ser acessado por esse cliente.

