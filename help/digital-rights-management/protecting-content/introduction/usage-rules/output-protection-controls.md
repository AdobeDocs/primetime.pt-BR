---
seo-title: Controles de proteção de saída
title: Controles de proteção de saída
uuid: a0518392-cd33-4ef0-834c-f90145a9b421
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---


# Controles de proteção de saída{#output-protection-controls}

O parâmetro de controle de proteção de saída controla se a saída para dispositivos de renderização externos está protegida. Você pode especificar restrições para saídas analógicas e digitais independentemente.

Controla se a saída para dispositivos de renderização externos deve ser restrita. Um dispositivo externo é definido como qualquer dispositivo de vídeo ou áudio que não esteja incorporado no computador. As exibições integradas, como em computadores notebook, não são consideradas externas no cenário de controles de proteção de saída.

Por padrão, os tipos de conexão OTA (Over the air) são todos blocos listados, mas podem ser permitidos listados explicitamente, se necessário. As conexões OTA suportadas incluem: Miracast, AirPlay, DLNA e WIDI.

**Proteção de saída baseada em resolução: (Disponível na versão 5.3 em diante.) ** Isso proporciona proteção de saída com base na contagem vertical de pixels do conteúdo, permitindo que uma variedade de requisitos de proteção sejam especificados com base na contagem vertical de pixels.

As seguintes opções/níveis de aplicação estão disponíveis:

| Opção | Suportado em dispositivos analógicos | Suportado em dispositivos digitais |
|---|---|---|
| **Obrigatório** — Proteção de cópia analógica (ACP) ou Sistema de gerenciamento de geração de cópias - a proteção de saída analógica (CGMS-A) deve ser ativada para reproduzir conteúdo em um dispositivo externo. Os clientes DRM do Primetime devem ativar a proteção de saída usando ACP ou CGMS-A. Em dispositivos compatíveis com ambos, os clientes Primetime DRM 3.0 tentam habilitar ambos. No entanto, somente um deve estar habilitado para reproduzir o conteúdo. | SIM | SIM |
| **ACP obrigatório** — A proteção de saída ACP é necessária. A reprodução não é permitida no CGMS-A. Os clientes Primetime DRM 2.0 não suportam essa opção. Se definido, um cliente Primetime DRM 2.0 se comporta como se a opção &quot;Sem reprodução&quot; tivesse sido especificada. | SIM | - |
| **Use se disponível** — Tente ativar a proteção de saída ACP e CGMS-A, se disponível, e permita a reprodução, se não disponível. Os clientes Primetime DRM 3.0 tentam habilitar ACP e CGMS-A, se possível. Os clientes Primetime DRM 2.0 tentam ativar apenas ACP ou CGMS-A. Por exemplo, o cliente DRM Primetime faz uma tentativa de habilitar ACP ou CGMS-A. Se a tentativa for bem-sucedida, a outra opção não poderá ser ativada. Se a tentativa falhar, uma segunda tentativa será feita para habilitar a outra opção. Mesmo se ambas as tentativas falharem, o conteúdo será reproduzido assim mesmo. | SIM | SIM |
| **Usar ACP se disponível** — Tente ativar a proteção de saída ACP, se disponível, mas permita a reprodução, se não disponível. A proteção não está disponível no CGMS-A. Os clientes Primetime DRM 2.0 não suportam essa opção. Se definido, um cliente Primetime DRM 2.0 se comporta como se a opção &quot;Sem proteção&quot; tivesse sido especificada. | SIM | - |
| **Usar CGMS-A se disponível **— Tente ativar a proteção de saída CGMS-A, se disponível, mas permita a reprodução, se não disponível. A proteção não está disponível no ACP. Os clientes Primetime DRM 2.0 não suportam essa opção. Se definido, um cliente Primetime DRM 2.0 se comporta como se a opção &quot;Sem proteção&quot; tivesse sido especificada. | SIM | - |
| **Sem proteção** — Nenhuma ativação de proteção de saída é imposta para saídas analógicas e digitais. | SIM | SIM |
| **Sem reprodução** — Não permita a reprodução em um dispositivo externo para saídas analógicas e digitais. | SIM | SIM |

>[!NOTE]
>
>Embora essas regras sejam aplicadas de forma consistente em todas as plataformas, você só pode ativar com segurança a proteção de saída nas plataformas Windows. Em outras plataformas, como Macintosh e Linux, não há suporte para funções de sistema operacional disponíveis para aplicativos de terceiros.

Exemplo de caso de uso: Alguns conteúdos podem aplicar controles de proteção de saída e, portanto, o distribuidor de conteúdo pode definir o nível de proteção. Se &quot;Obrigatório&quot; for especificado e a reprodução for tentada em um Macintosh, o cliente não reproduzirá conteúdo em dispositivos externos. O conteúdo pode ser reproduzido em monitores internos.

Se &quot;Obrigatório&quot; for especificado e a reprodução for tentada no Linux, o cliente não reproduzirá conteúdo em nenhum dispositivo porque não pode diferenciar entre dispositivos internos e externos.

Se você especificar &quot;Usar se disponível&quot;, a proteção de saída será ativada quando possível. Por exemplo, em sistemas Windows que suportam o Certified Output Protection Protocol (COPP), o conteúdo é transmitido com proteção de saída para uma tela externa. Esse exemplo às vezes é conhecido como *`selectable output control`*.
