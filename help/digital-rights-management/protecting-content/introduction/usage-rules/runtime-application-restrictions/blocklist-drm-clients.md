---
title: Lista de bloqueios de Clientes DRM impedidos de acessar conteúdo protegido
description: Lista de bloqueios de Clientes DRM impedidos de acessar conteúdo protegido
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Lista de bloqueios de Clientes DRM impedidos de acessar conteúdo protegido {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

Essa lista de bloqueios especifica os clientes DRM do Primetime que não podem acessar o conteúdo protegido. Você faz a lista de bloqueios de clientes por versão e plataforma do cliente.

Exemplo de caso de uso: no caso de uma falha de segurança, uma versão mais recente do cliente DRM do Primetime pode ser especificada como a versão mínima necessária para a aquisição da licença e a reprodução do conteúdo. O servidor de licenças verifica se o cliente Primetime DRM que faz a solicitação de licença atende aos requisitos de versão antes de emitir uma licença. O cliente DRM do Primetime também verifica a versão na licença antes de reproduzir o conteúdo. Essa verificação de cliente é necessária no caso de domínios em que uma licença pode ser transferida para outro computador.

Uma versão de cliente DRM do Primetime pode ser identificada pelos atributos especificados na tabela a seguir:

| **Atributo** | **Valores suportados** | **Corresponder critérios** | **Descrição** |
|---|---|---|---|
| Ambiente | `“PC”, “PortingKit”` | Correspondência exata | Identifica se o cliente está sendo executado em um desktop ou em qualquer outro dispositivo. |
| SO | `“Win”, “Mac”, “Linux”, “Android”, “iOS”, "ChromeOS"` | Correspondência exata | Platform |
| Arquitetura | `“32”, “64”` | Correspondência exata | 32 ou 64 bits |
| Tipo de tela | `“PC”, “Mobile”, “TV”` | Correspondência exata | |
| Versão de tempo de execução | Um número de versão válido. Por exemplo, `“2.0.0”, "3.0", "4.0", "11.0"`, etc. | Corresponde se a versão do cliente é inferior ou igual à versão especificada. | O número da versão é especificado como uma combinação de números e pontos (&quot;.&quot;) de qualquer comprimento. |
| Versão da biblioteca DRM do Primetime | Um número de versão válido. Por exemplo, `“2.0.0”`. | Corresponde se a versão do cliente é inferior ou igual à versão especificada. | O número da versão é especificado como uma combinação de números e pontos (&quot;.&quot;) de qualquer comprimento. |
| Fornecedor OEM | Sequência de caracteres do fornecedor OEM que pode ser localizada no Certificado de tempo de execução emitido para um cliente que transferiu o DRM do Primetime para um dispositivo. | Correspondência exata | String de identificação do fornecedor OEM para o dispositivo que usa o kit de portabilidade. |
| Modelo | Sequência de modelo que pode ser localizada no Certificado de tempo de execução emitido para um cliente que transferiu o DRM do Primetime para um dispositivo. Por exemplo, `"iOS_Mobile", "Android_Mobile", "Chrome", "ChromeOS_ARM", "WindowsOnARM", "AVE"` | Correspondência exata | String de identificação do modelo do dispositivo usando o kit de portabilidade. |

>[!NOTE]
>
>Ao especificar uma entrada na lista de bloqueios, você pode definir valores para um ou mais dos atributos mencionados na tabela anterior. Qualquer atributo não especificado é tratado como curinga. Se o cliente DRM do Primetime corresponder a todos os valores especificados em uma entrada de lista de bloqueios, o conteúdo protegido pode não ser acessado por esse cliente.
