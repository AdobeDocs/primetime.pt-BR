---
title: Controles de proteção de saída
description: Controles de proteção de saída
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# Controles de proteção de saída{#output-protection-controls}

O parâmetro de controles de proteção de saída controla se a saída para dispositivos de renderização externos está protegida. É possível especificar restrições para saídas analógicas e digitais independentemente.

Controla se a saída para dispositivos de renderização externos deve ser restrita. Um dispositivo externo é definido como qualquer dispositivo de vídeo ou áudio que não esteja incorporado no computador. Monitores integrados, como em notebooks, não são considerados externos no cenário de controles de proteção de saída.

Os tipos de conexão OTA (Over the air) são todos incluídos na lista de bloqueios por padrão, mas podem ser explicitamente listados, se necessário. As conexões OTA compatíveis incluem: Miracast, AirPlay, DLNA e WIDI.

**Proteção de saída baseada em resolução: (Disponível a partir da versão 5.3.) ** Isso fornece proteção de saída com base na contagem vertical de pixels do conteúdo, permitindo que vários requisitos de proteção sejam especificados com base na contagem vertical de pixels.

As seguintes opções/níveis de imposição estão disponíveis:

| Opção | Compatível com dispositivos analógicos | Compatível com dispositivos digitais |
|---|---|---|
| **Obrigatório** — a proteção de saída Analog Copy Protection (ACP) ou Copy Generation Management System - Analog (CGMS-A) deve estar ativada para reproduzir conteúdo em um dispositivo externo. Os clientes DRM do Primetime devem habilitar a proteção de saída usando ACP ou CGMS-A. Em dispositivos que oferecem suporte a ambos, os clientes Primetime DRM 3.0 tentam ativar ambos. No entanto, apenas um deve estar habilitado para reproduzir o conteúdo. | SIM | SIM |
| **ACP Obrigatório** — É necessária a proteção de saída ACP. A reprodução não é permitida no CGMS-A. Os clientes do Primetime DRM 2.0 não oferecem suporte a essa opção. Se definida, um cliente DRM 2.0 do Primetime se comportará como se a opção &quot;Nenhuma reprodução&quot; tivesse sido especificada. | SIM | - |
| **Usar se disponível** — Tente ativar a proteção de saída ACP e CGMS-A se disponível e permita a reprodução se não estiver disponível. Os clientes do Primetime DRM 3.0 tentam ativar o ACP e o CGMS-A, se possível. Os clientes do Primetime DRM 2.0 só tentam ativar o ACP ou o CGMS-A. Por exemplo, o cliente Primetime DRM tenta habilitar o ACP ou o CGMS-A. Se a tentativa for bem-sucedida, a outra opção não poderá ser ativada. Se a tentativa falhar, uma segunda tentativa será feita para habilitar a outra opção. Mesmo se ambas as tentativas falharem, o conteúdo será reproduzido mesmo assim. | SIM | SIM |
| **Usar ACP, se disponível** — Tentar habilitar a proteção de saída ACP, se disponível, mas permitir reprodução, se não estiver disponível. Proteção não disponível no CGMS-A. Os clientes do Primetime DRM 2.0 não oferecem suporte a essa opção. Se definida, um cliente DRM 2.0 do Primetime se comportará como se a opção &quot;Sem proteção&quot; tivesse sido especificada. | SIM | - |
| **Usar CGMS-A se disponível **— Tente ativar a proteção de saída CGMS-A se disponível, mas permita a reprodução se não estiver disponível. A proteção não está disponível no ACP. Os clientes do Primetime DRM 2.0 não oferecem suporte a essa opção. Se definida, um cliente DRM 2.0 do Primetime se comportará como se a opção &quot;Sem proteção&quot; tivesse sido especificada. | SIM | - |
| **Sem proteção** — Nenhuma ativação de proteção de saída é imposta para saídas analógicas e digitais. | SIM | SIM |
| **Nenhuma reprodução** — Não permita a reprodução para um dispositivo externo para saídas analógicas e digitais. | SIM | SIM |

>[!NOTE]
>
>Embora essas regras sejam aplicadas consistentemente em todas as plataformas, você só pode ativar com segurança a proteção de saída nas plataformas Windows. Em outras plataformas, como Macintosh e Linux, não há funções de suporte do sistema operacional disponíveis para aplicativos de terceiros.

Exemplo de caso de uso: algum conteúdo pode aplicar controles de proteção de saída e, portanto, o distribuidor de conteúdo pode definir o nível de proteção. Se &quot;Obrigatório&quot; for especificado e a reprodução for tentada em um Macintosh, o cliente não reproduzirá o conteúdo em dispositivos externos. O conteúdo pode ser reproduzido em monitores internos.

Se &quot;Obrigatório&quot; for especificado e a reprodução for tentada no Linux, o cliente não reproduzirá o conteúdo em nenhum dispositivo porque não consegue diferenciar entre dispositivos internos e externos.

Se você especificar &quot;Usar se disponível&quot;, a proteção de saída será ativada quando possível. Por exemplo, em sistemas Windows compatíveis com o COPP (Certified Output Protection Protocol), o conteúdo é transmitido com proteção de saída a uma tela externa. Esse exemplo às vezes é conhecido como *`selectable output control`*.
