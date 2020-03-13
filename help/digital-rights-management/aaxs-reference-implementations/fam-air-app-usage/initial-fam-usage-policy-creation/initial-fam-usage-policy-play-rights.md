---
seo-title: Direitos de reprodução
title: Direitos de reprodução
uuid: 90f2a7a6-6637-4d10-9afe-6d2e77fc4185
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c

---


# Direitos de reprodução {#play-rights}

A tabela a seguir descreve as preferências de Direitos de reprodução:

| Preferência | Descrição |
|--- |--- |
| Janela de reprodução | A duração de uma licença é válida (em minutos) após a primeira vez que o usuário reproduz o conteúdo protegido. |
| Proteção de saída | Controla se a saída para dispositivos de renderização externos deve ser protegida. Saídas analógicas e digitais podem ser especificadas independentemente. |
| Restrições | Lista negra de versões de clientes que não têm permissão para reproduzir conteúdo. Todas as colunas são opcionais. |
| DRM | Especifica uma lista de versões DRM que não têm permissão para reproduzir conteúdo protegido. |
| Tempo de execução | Especifica uma lista de versões em tempo de execução que não têm permissão para reproduzir conteúdo protegido. |
| Nível mínimo de segurança |  |
| DRM | Nível mínimo de segurança de DRM necessário para reproduzir conteúdo protegido. |
| Tempo de execução | Nível mínimo de segurança de tempo de execução necessário para reproduzir conteúdo protegido. |
| Aplicativos permitidos | Lista de permissões dos aplicativos clientes autorizados a reproduzir conteúdo. Se não houver aplicativos especificados, qualquer aplicativo SWF ou AIR será permitido. |
| SWF | Lista de URLs SWF permitidos para reproduzir conteúdo protegido. |
| AIR | Lista de aplicativos AIR permitidos para reproduzir conteúdo protegido. A ID do editor é obrigatória, os campos restantes são opcionais. |

O Flash Access Manager oferece suporte a políticas que contêm vários Direitos de Reprodução. Para criar uma política com mais de um direito de reprodução, use o botão &quot;Adicionar direito de reprodução adicional&quot; e preencha os atributos desejados para cada direito de reprodução.

Ao consumir uma licença, o cliente usa o primeiro direito de reprodução para o qual atende a todos os requisitos. Vários direitos de reprodução podem ser usados para especificar restrições diferentes para diferentes sistemas operacionais. Por exemplo, é possível especificar um direito com a Proteção de saída exigida para o Windows (ao adicionar versões DRM à lista negra no Macintosh e no Linux) e especificar um segundo direito com a Proteção de saída &quot;Usar se disponível&quot; em outras plataformas (ao adicionar versões DRM à lista negra no Windows).
