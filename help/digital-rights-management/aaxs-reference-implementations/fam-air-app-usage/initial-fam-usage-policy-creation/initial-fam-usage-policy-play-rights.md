---
title: Direitos de reprodução
description: Direitos de reprodução
copied-description: true
exl-id: a4fda537-dbcc-496b-8f15-c13b25fe87b0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# Direitos de reprodução {#play-rights}

A tabela a seguir descreve as preferências de direitos de reprodução:

| Preferência | Descrição |
|--- |--- |
| Janela de reprodução | A duração da licença é válida (em minutos) após a primeira vez que o usuário reproduz o conteúdo protegido. |
| Proteção de saída | Controla se a saída para dispositivos de renderização externos deve ser protegida. As saídas analógicas e digitais podem ser especificadas independentemente. |
| Restrições | A lista de bloqueios de versões de clientes não tem permissão para reproduzir conteúdo. Todas as colunas são opcionais. |
| DRM | Especifica uma lista de versões de DRM que não têm permissão para reproduzir conteúdo protegido. |
| Tempo de execução | Especifica uma lista de versões de Tempo de Execução que não têm permissão para reproduzir conteúdo protegido. |
| Nível mínimo de segurança |  |
| DRM | Nível mínimo de segurança DRM necessário para reproduzir conteúdo protegido. |
| Tempo de execução | Nível mínimo de segurança de tempo de execução necessário para reproduzir conteúdo protegido. |
| Aplicativos permitidos | Lista de permissões de aplicativos clientes com permissão para reproduzir conteúdo. Se nenhum aplicativo for especificado, qualquer aplicativo SWF ou AIR será permitido. |
| SWF | Lista de URLs do SWF com permissão para reproduzir conteúdo protegido. |
| AIR | Lista de aplicativos do AIR com permissão para reproduzir conteúdo protegido. A ID do editor é obrigatória. Os campos restantes são opcionais. |

O Gerenciador de Flashes Access é compatível com políticas que contêm vários Direitos de reprodução. Para criar uma política com mais de um direito de reprodução, use o botão &quot;Adicionar direito de reprodução adicional&quot; e preencha os atributos desejados para cada direito de reprodução.

Ao consumir uma licença, o cliente usa o primeiro direito de reprodução para o qual atende a todos os requisitos. Vários direitos de reprodução podem ser usados para especificar restrições diferentes para sistemas operacionais diferentes. Por exemplo, é possível especificar um direito com a Proteção de saída necessária para o Windows (por inclusão de versões DRM em Macintosh e Linux) e especificar um segundo direito com a Proteção de saída &quot;Usar se disponível&quot; em outras plataformas (por inclusão de versões DRM em Windows).
