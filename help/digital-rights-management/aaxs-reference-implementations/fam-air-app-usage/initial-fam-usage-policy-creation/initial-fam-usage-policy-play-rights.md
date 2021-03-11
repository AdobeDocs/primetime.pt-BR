---
title: Direitos de reprodução
description: Direitos de reprodução
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# Direitos de reprodução {#play-rights}

A tabela a seguir descreve as preferências de Direitos de reprodução:

| Preferência | Descrição |
|--- |--- |
| Janela de reprodução | A duração de uma licença é válida (em minutos) após a primeira vez que o usuário reproduz o conteúdo protegido. |
| Proteção de saída | Controla se a saída para dispositivos de renderização externos deve ser protegida. Saídas analógicas e digitais podem ser especificadas independentemente. |
| Restrições | Lista de bloqueios de versões de clientes que não têm permissão para reproduzir conteúdo. Todas as colunas são opcionais. |
| DRM | Especifica uma lista de versões de DRM que não têm permissão para reproduzir conteúdo protegido. |
| Tempo de execução | Especifica uma lista de versões de Tempo de execução que não têm permissão para reproduzir conteúdo protegido. |
| Nível mínimo de segurança |  |
| DRM | Nível mínimo de segurança de DRM necessário para reproduzir conteúdo protegido. |
| Tempo de execução | Nível mínimo de segurança de Tempo de execução necessário para reproduzir conteúdo protegido. |
| Aplicativos permitidos | Lista de permissões de aplicativos clientes com permissão para reproduzir conteúdo. Se não forem especificadas aplicações, é permitida qualquer aplicação SWF ou AIR. |
| SWF | Lista de URLs SWF permitidos para reproduzir conteúdo protegido. |
| AR | Lista de aplicações AIR permitidas para reprodução de conteúdo protegido. ID do editor é obrigatório, os campos restantes são opcionais. |

O Flash Access Manager é compatível com políticas que contêm vários Direitos de reprodução. Para criar uma política com mais de um direito de reprodução, use o botão &quot;Adicionar direito de reprodução adicional&quot; e preencha os atributos desejados para cada direito de reprodução.

Ao consumir uma licença, o cliente usa o primeiro direito de reprodução para o qual atende a todos os requisitos. Vários direitos de reprodução podem ser usados para especificar diferentes restrições para diferentes sistemas operacionais. Por exemplo, é possível especificar um direito com a Proteção de Saída necessária para o Windows (ao bloquear a listagem de versões de DRM no Macintosh e Linux) e especificar um segundo direito com a Proteção de Saída &quot;Use if available&quot; em outras plataformas (ao listar as versões de DRM no Windows).
