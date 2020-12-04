---
seo-title: Revogação de credenciais de cliente e tempo de execução do DRM
title: Revogação de credenciais de cliente e tempo de execução do DRM
uuid: 8e36536a-8eed-4d27-8a5f-8d3219817e57
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# Revogando credenciais de cliente e tempo de execução do DRM {#revoking-drm-client-and-runtime-credentials}

As versões de DRM/Tempo de execução são identificadas pelo nível de segurança, número de versão e outros atributos, incluindo o Sistema operacional e o tempo de execução. Para restringir as versões de DRM/Tempo de execução permitidas, defina as restrições do módulo em uma política de DRM ou em `HandlerConfiguration`. As restrições do módulo podem incluir um nível mínimo de segurança e lista de versões do módulo que não podem receber uma licença.

Consulte [Lista de bloqueios de clientes DRM que não têm acesso a conteúdo protegido](../../protecting-content/introduction/usage-rules/runtime-application-restrictions/blocklist-drm-clients.md) para obter detalhes sobre os atributos usados para identificar um módulo DRM/Runtime.

Se o nível mínimo de segurança for definido, a versão no cliente (especificada no token do computador) deverá ser maior ou igual ao valor especificado.

Se uma lista de versões excluídas for especificada e a versão do cliente corresponder a qualquer um dos identificadores de versão na lista, o cliente não terá permissão para usar um direito contendo essa instância de ModuleRequirements. Para que um módulo corresponda às informações da versão, todos os parâmetros especificados nas informações da versão, exceto a versão de lançamento, devem corresponder exatamente aos valores dos módulos. A versão corresponde se o valor do módulo cliente for menor ou igual ao valor nas informações da versão.

No evento, uma violação é relatada com um cliente DRM específico ou uma versão de tempo de execução, o proprietário do conteúdo e o distribuidor de conteúdo (que executa o servidor de licenças) podem configurar o servidor para recusar a emissão de licenças durante um período no qual o Adobe não tem uma correção disponível. Isso pode ser configurado por meio de `HandlerConfiguration`, conforme descrito acima, ou fazendo alterações em todas as políticas de DRM. Neste último caso, você pode manter uma lista de atualização de política de DRM e usá-la para verificar se uma política de DRM foi atualizada ou revogada.

Se você precisar de uma versão mais recente do Flash Player Adobe/Adobe AIR Runtime ou da biblioteca do Adobe Content Protection (módulo DRM), é necessário atualizar suas políticas de DRM.

Consulte [Atualização de uma política usando a API Java](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md).

Em seguida, é necessário criar uma Lista de Atualização de Política de DRM ou definir restrições em `HandlerConfiguration` invocando `HandlerConfiguration.setRuntimeModuleRequirements()` ou `HandlerConfiguration.setDRMModuleRequirements()`. Quando um usuário solicita uma nova licença com as listas de bloqueios especificadas ativadas, é necessário instalar os tempos de execução e as bibliotecas mais recentes para que uma licença possa ser emitida.

Consulte o código de exemplo em [Atualização de uma política usando a API Java Para obter um exemplo sobre a listagem de blocos de versões de DRM e de tempo de execução](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md), consulte um exemplo sobre a listagem de blocos de versões de DRM e de tempo de execução.
