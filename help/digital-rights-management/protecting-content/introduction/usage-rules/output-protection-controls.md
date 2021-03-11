---
title: Controles de proteção de saída
description: Controles de proteção de saída
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---


# Controles de proteção de saída{#output-protection-controls}

O parâmetro de controle de proteção de saída controla se a saída para dispositivos de renderização externos está protegida. Você pode especificar restrições para saídas analógicas e digitais independentemente.

Controla se a saída para dispositivos de renderização externos deve ser restrita. Um dispositivo externo é definido como qualquer dispositivo de vídeo ou áudio que não esteja incorporado no computador. Os monitores integrados, como em computadores notebook, não são considerados externos no cenário de controles de proteção de saída.

Por padrão, os tipos de conexão de ar (OTA) são todos bloqueados, mas podem ser explicitamente listados, se necessário. As conexões OTA suportadas incluem: Miracast, AirPlay, DLNA e WIDI.

**Proteção de saída baseada em resolução: (Disponível a partir da versão 5.3.) ** Isso fornece proteção de saída com base na contagem vertical de pixels do conteúdo, permitindo que uma variedade de requisitos de proteção sejam especificados com base na contagem vertical de pixels.

Estão disponíveis as seguintes opções/níveis de execução:

| Opção | Suportado em dispositivos analógicos | Suportado em dispositivos digitais |
|---|---|---|
| **Obrigatório**  — A proteção de saída Analog Copy Protection (ACP) ou Copy Generation Management System - Analog (CGMS-A) deve ser ativada para reproduzir conteúdo em um dispositivo externo. Os clientes de DRM do Primetime devem ativar a proteção de saída usando ACP ou CGMS-A. Em dispositivos que suportam ambos, os clientes do Primetime DRM 3.0 tentam habilitar ambos. No entanto, apenas um deve estar habilitado para reproduzir o conteúdo. | SIM | SIM |
| **ACP Obrigatório**  — É necessária a proteção de saída ACP. A reprodução não é permitida no CGMS-A. Os clientes DRM 2.0 do Primetime não suportam essa opção. Se definido, um cliente DRM 2.0 do Primetime se comporta como se a opção &quot;Sem reprodução&quot; tivesse sido especificada. | SIM | - |
| **Use se disponível**  — Tente ativar a proteção de saída ACP e CGMS-A, se disponível, e permita a reprodução, se não estiver disponível. Os clientes do Primetime DRM 3.0 tentam habilitar o ACP e o CGMS-A, se possível. Os clientes do Primetime DRM 2.0 tentam ativar apenas o ACP ou o CGMS-A. Por exemplo, uma tentativa é feita pelo cliente DRM do Primetime para habilitar ACP ou CGMS-A. Se a tentativa for bem-sucedida, a outra opção não poderá ser habilitada. Se a tentativa falhar, uma segunda tentativa será feita para habilitar a outra opção. Mesmo que ambas as tentativas falhem, o conteúdo é reproduzido de qualquer maneira. | SIM | SIM |
| **Use ACP se disponível**  — Tente ativar a proteção de saída ACP, se disponível, mas permita a reprodução, se não estiver disponível. A proteção não está disponível no CGMS-A. Os clientes DRM 2.0 do Primetime não suportam essa opção. Se definido, um cliente DRM 2.0 do Primetime se comporta como se a opção &quot;Sem proteção&quot; tivesse sido especificada. | SIM | - |
| **Use o CGMS-A, se disponível **— Tente ativar a proteção de saída do CGMS-A, se disponível, mas permita a reprodução, se não estiver disponível. A proteção não está disponível no ACP. Os clientes DRM 2.0 do Primetime não suportam essa opção. Se definido, um cliente DRM 2.0 do Primetime se comporta como se a opção &quot;Sem proteção&quot; tivesse sido especificada. | SIM | - |
| **Sem proteção** — Nenhuma ativação de proteção de saída é imposta para saídas analógicas e digitais. | SIM | SIM |
| **Sem reprodução**  — Não permita reprodução em um dispositivo externo para saídas analógicas e digitais. | SIM | SIM |

>[!NOTE]
>
>Embora essas regras sejam aplicadas de forma consistente em todas as plataformas, você só pode ativar com segurança a proteção de saída nas plataformas Windows. Em outras plataformas, como Macintosh e Linux, não há funções de sistema operacional de suporte disponíveis para aplicativos de terceiros.

Exemplo de caso de uso: Alguns conteúdos podem aplicar controles de proteção de saída e, portanto, o distribuidor de conteúdo pode definir o nível de proteção. Se &quot;Obrigatório&quot; for especificado e a reprodução for tentada em um Macintosh, o cliente não reproduzirá conteúdo em dispositivos externos. O conteúdo pode ser reproduzido em monitores internos.

Se &quot;Obrigatório&quot; for especificado e a reprodução for tentada no Linux, o cliente não reproduzirá conteúdo em nenhum dispositivo porque não pode diferenciar entre dispositivos internos e externos.

Se você especificar &quot;Use if available&quot;, a proteção de saída será ativada, quando possível. Por exemplo, em sistemas Windows que oferecem suporte ao COPP (Certified Output Protection Protocol), o conteúdo é transmitido com proteção de saída para uma exibição externa. Esse exemplo às vezes é conhecido como *`selectable output control`*.
