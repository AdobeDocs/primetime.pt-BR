---
description: nulo
seo-description: nulo
seo-title: Lista de bloqueios de clientes DRM impedidos de acessar conteúdo protegido
title: Lista de bloqueios de clientes DRM impedidos de acessar conteúdo protegido
uuid: 38bc024e-0c5b-4c1c-8d4b-94b9e0fec67e
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Lista de bloqueios de clientes DRM impedidos de acessar conteúdo protegido {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

Esta lista de bloqueios especifica os clientes DRM Primetime que não podem acessar conteúdo protegido. Você lista de bloqueios clientes pela versão e plataforma do cliente.

Exemplo de caso de uso: No evento de uma violação de segurança, uma versão mais recente do cliente Primetime DRM pode ser especificada como a versão mínima exigida para aquisição de licença e reprodução de conteúdo. O servidor de licenças verifica se o cliente Primetime DRM que faz a solicitação de licença atende aos requisitos de versão antes de emitir uma licença. O cliente DRM Primetime também verifica a versão na licença antes de reproduzir o conteúdo. Essa verificação do cliente é necessária no caso de domínios nos quais uma licença pode ser transferida para outra máquina.

Uma versão do cliente DRM Primetime pode ser identificada pelos atributos especificados na tabela a seguir:

| **Atributo** | **Valores suportados** | **Critérios de correspondência** | **Descrição** |
|---|---|---|---|
| Ambiente | `“PC”, “PortingKit”` | Correspondência exata | Identifica se o cliente está sendo executado em uma área de trabalho ou em qualquer outro dispositivo. |
| SO | `“Win”, “Mac”, “Linux”, “Android”, “iOS”, "ChromeOS"` | Correspondência exata | Plataforma |
| Arquitetura | `“32”, “64”` | Correspondência exata | 32 bits ou 64 bits |
| Tipo de tela | `“PC”, “Mobile”, “TV”` | Correspondência exata |  |
| Versão do tempo de execução | Um número de versão válido. Por exemplo, `“2.0.0”, "3.0", "4.0", "11.0"`, etc. | Corresponde se a versão do cliente é menor ou igual à versão especificada. | O número da versão é especificado como uma combinação de números e pontos (&quot;.&quot;) de qualquer comprimento. |
| Versão da biblioteca DRM Primetime | Um número de versão válido. Por exemplo, `“2.0.0”`. | Corresponde se a versão do cliente é menor ou igual à versão especificada. | O número da versão é especificado como uma combinação de números e pontos (&quot;.&quot;) de qualquer comprimento. |
| Fornecedor OEM | Sequência de caracteres do fornecedor OEM que pode ser localizada no Certificado de tempo de execução emitido para um cliente que exportou o DRM Primetime para um dispositivo. | Correspondência exata | Sequência de caracteres de identificação do fornecedor OEM para o dispositivo usando o kit de porta. |
| Modelo | Sequência de caracteres do modelo que pode ser localizada no Certificado de tempo de execução emitido para um cliente que importou o DRM Primetime para um dispositivo. Por exemplo, `"iOS_Mobile", "Android_Mobile", "Chrome", "ChromeOS_ARM", "WindowsOnARM", "AVE"` | Correspondência exata | Sequência de identificação do modelo de dispositivo para o dispositivo usando o kit de porta. |

>[!NOTE]
>
>Ao especificar uma entrada na lista de bloqueios, é possível definir valores para um ou mais dos atributos mencionados na tabela anterior. Qualquer atributo não especificado é tratado como curinga. Se o cliente DRM Primetime corresponder a todos os valores especificados em uma entrada de lista de bloqueios, o conteúdo protegido pode não ser acessado por esse cliente.

