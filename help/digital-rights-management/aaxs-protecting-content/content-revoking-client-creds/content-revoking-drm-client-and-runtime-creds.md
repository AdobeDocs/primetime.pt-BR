---
seo-title: Revogação de credenciais de cliente e tempo de execução do DRM
title: Revogação de credenciais de cliente e tempo de execução do DRM
uuid: 774b8ac7-51bb-42fc-a05d-cfa718e24a81
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Revogação de credenciais de cliente e tempo de execução do DRM{#revoking-drm-client-and-runtime-credentials}

As versões de DRM/tempo de execução são identificadas pelo nível de segurança, número de versão e outros atributos, incluindo SO e tempo de execução. Para restringir as versões de DRM/Tempo de execução permitidas, defina as restrições do módulo em uma política ou em uma `HandlerConfiguration`. As restrições do módulo podem incluir um nível mínimo de segurança e uma lista de versões do módulo que não podem receber uma licença. Consulte Lista [preta de clientes DRM que não acessam conteúdo](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-blacklist-drm-clients.md) protegido para obter detalhes sobre os atributos usados para identificar um módulo DRM/Runtime.

Se o nível mínimo de segurança for definido, a versão no cliente (especificada no token do computador) deverá ser maior ou igual ao valor especificado.

Se uma lista de versões excluídas for especificada e a versão do cliente corresponder a qualquer um dos identificadores de versão na lista, o cliente não poderá usar um direito que contenha essa instância de ModuleRequirements. Para que um módulo corresponda às informações da versão, todos os parâmetros especificados nas informações da versão, exceto a versão de lançamento, devem corresponder exatamente aos valores dos módulos. A versão corresponde se o valor do módulo cliente for menor ou igual ao valor nas informações da versão.

Caso uma violação seja relatada com um cliente DRM específico ou uma versão de tempo de execução, o proprietário do conteúdo e o distribuidor de conteúdo (que executa o servidor de licenças) podem configurar o servidor para recusar a emissão de licenças durante um período no qual a Adobe não tenha uma correção disponível. Isso pode ser configurado por meio do `HandlerConfiguration` descrito acima, ou fazendo alterações em todas as políticas. Neste último caso, você pode manter uma lista de atualização de política e usá-la para verificar se uma política foi atualizada ou revogada.

Se você precisar de uma versão mais recente do Adobe® Flash® Player/Adobe® AIR® Runtime ou da biblioteca do Adobe Content Protection (módulo DRM), atualize suas políticas conforme mostrado em [Atualização de uma política usando a API](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md) Java e crie uma lista de atualização de política, ou defina restrições `HandlerConfiguration` chamando `HandlerConfiguration.setRuntimeModuleRequirements()` ou `HandlerConfiguration.setDRMModuleRequirements()`. Quando um usuário solicita uma nova licença com essas listas negras ativadas, os tempos de execução e as bibliotecas mais recentes devem ser instalados antes que uma licença possa ser emitida. Para obter um exemplo sobre a lista negra de versões de DRM e tempo de execução, consulte o código de amostra em [Atualização de uma política usando a API](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md)Java.
