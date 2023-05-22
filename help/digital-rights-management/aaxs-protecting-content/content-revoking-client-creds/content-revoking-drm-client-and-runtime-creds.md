---
title: Revogação de credenciais de cliente e tempo de execução DRM
description: Revogação de credenciais de cliente e tempo de execução DRM
copied-description: true
exl-id: f39d6523-9215-49ec-bb3b-e60fe6690dca
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Revogação de credenciais de cliente e tempo de execução DRM{#revoking-drm-client-and-runtime-credentials}

As versões de DRM/Runtime são identificadas pelo nível de segurança, número de versão e outros atributos, incluindo o sistema operacional e o runtime. Para restringir as versões de DRM/Runtime permitidas, defina as restrições do módulo em uma política ou em uma `HandlerConfiguration`. As restrições do módulo podem incluir um nível mínimo de segurança e uma lista de versões do módulo que não têm permissão para receber uma licença. Consulte [Lista de bloqueios de Clientes DRM impedidos de acessar conteúdo protegido](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-blocklist-drm-clients.md) para obter detalhes sobre os atributos usados para identificar um módulo DRM/Runtime.

Se o nível de segurança mínimo for definido, a versão no cliente (especificada no token do computador) deverá ser maior ou igual ao valor especificado.

Se uma lista de versões excluídas for especificada e a versão do cliente corresponder a qualquer um dos identificadores de versão na lista, o cliente não poderá usar um direito contendo essa instância ModuleRequirements. Para que um módulo corresponda às informações da versão, todos os parâmetros especificados nas informações da versão, exceto a versão de lançamento, devem corresponder exatamente aos valores dos módulos. A versão de lançamento corresponde se o valor do módulo do cliente for menor ou igual ao valor nas informações de versão.

Caso uma violação seja relatada com um cliente DRM específico ou uma versão de tempo de execução, o proprietário do conteúdo e o distribuidor de conteúdo (que executa o servidor de licenças) podem configurar o servidor para recusar a emissão de licenças durante um período em que o Adobe não tenha uma correção disponível. Isso pode ser configurado por meio da variável `HandlerConfiguration` conforme descrito acima, ou fazendo alterações em todas as políticas. Nesse último caso, você pode manter uma lista de atualização de política e usá-la para verificar se uma política foi atualizada ou revogada.

Se você precisar de uma versão mais recente do Adobe® Flash® Player/Adobe® AIR® Runtime ou da biblioteca Adobe Content Protection (módulo DRM), atualize suas políticas conforme mostrado na [Atualização de uma política usando a API Java](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md) e criar uma Lista de atualização de política ou definir restrições em `HandlerConfiguration` chamando `HandlerConfiguration.setRuntimeModuleRequirements()` ou `HandlerConfiguration.setDRMModuleRequirements()`. Quando um usuário solicita uma nova licença com essas listas de bloqueios ativadas, os tempos de execução e as bibliotecas mais recentes devem ser instalados antes que uma licença possa ser emitida. Para obter um exemplo de versões de DRM e tempo de execução da listagem de blocos, consulte o código de exemplo em [Atualização de uma política usando a API Java](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md).
