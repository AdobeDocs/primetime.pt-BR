---
title: Revogando credenciais de cliente e tempo de execução do DRM
description: Revogando credenciais de cliente e tempo de execução do DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# Revogando credenciais de cliente e tempo de execução do DRM{#revoking-drm-client-and-runtime-credentials}

As versões de DRM/Tempo de execução são identificadas por nível de segurança, número de versão e outros atributos, incluindo SO e tempo de execução. Para restringir as versões de DRM/Tempo de Execução permitidas, defina as restrições do módulo em uma política ou em um `HandlerConfiguration`. As restrições de módulo podem incluir um nível mínimo de segurança e uma lista de versões de módulo que não podem ser emitidas licenças. Consulte [Lista de bloqueios de clientes DRM restritos ao acesso a conteúdo protegido](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-blocklist-drm-clients.md) para obter detalhes sobre os atributos usados para identificar um módulo DRM/Runtime.

Se o nível mínimo de segurança for definido, a versão no cliente (especificada no token da máquina) deverá ser maior ou igual ao valor especificado.

Se uma lista de versões excluídas for especificada e a versão do cliente corresponder a qualquer um dos identificadores de versão na lista, o cliente não poderá usar um direito contendo essa instância ModuleRequirements. Para que um módulo corresponda às informações da versão, todos os parâmetros especificados nas informações da versão, exceto a versão de lançamento, devem corresponder exatamente aos valores dos módulos. A versão da corresponde se o valor do módulo do cliente for menor ou igual ao valor nas informações da versão.

Caso uma violação seja relatada com um cliente DRM ou versão de tempo de execução específico, o proprietário do conteúdo e o distribuidor de conteúdo (que executa o servidor de licenças) podem configurar o servidor para recusar a emissão de licenças durante um período em que o Adobe não tem uma correção disponível. Isso pode ser configurado por meio do `HandlerConfiguration` conforme descrito acima, ou fazendo alterações em todas as políticas. No último caso, é possível manter uma lista de atualização de política e usá-la para verificar se uma política foi atualizada ou revogada.

Se você precisar de uma versão mais recente do Adobe® Flash® Player/Adobe® AIR® Runtime ou da biblioteca de proteção de conteúdo do Adobe (módulo DRM), atualize suas políticas conforme mostrado em [Atualizando uma política usando a API Java](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md) e crie uma Lista de atualização de política ou defina restrições em `HandlerConfiguration` chamando `HandlerConfiguration.setRuntimeModuleRequirements()` ou `HandlerConfiguration.setDRMModuleRequirements()`. Quando um usuário solicita uma nova licença com essas listas de bloqueios ativadas, os tempos de execução e as bibliotecas mais recentes devem ser instalados antes que uma licença possa ser emitida. Para obter um exemplo sobre a lista de bloqueios de DRM e versões de tempo de execução, consulte o código de amostra em [Atualização de uma política usando a API Java](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md).
