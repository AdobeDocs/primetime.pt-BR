---
title: Revogação de credenciais de cliente e tempo de execução DRM
description: Revogação de credenciais de cliente e tempo de execução DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Revogação de credenciais de cliente e tempo de execução DRM {#revoking-drm-client-and-runtime-credentials}

As versões de DRM/Runtime são identificadas pelo nível de segurança, número de versão e outros atributos, incluindo o Sistema Operacional e o runtime. Para restringir as versões de DRM/Tempo de execução permitidas, defina as restrições do módulo em uma política de DRM ou em uma `HandlerConfiguration`. As restrições do módulo podem incluir um nível mínimo de segurança e uma lista de versões do módulo que não têm permissão para receber uma licença.

Consulte [Lista de bloqueios de Clientes DRM impedidos de acessar conteúdo protegido](../../protecting-content/introduction/usage-rules/runtime-application-restrictions/blocklist-drm-clients.md) para obter detalhes sobre os atributos usados para identificar um módulo DRM/Runtime.

Se o nível de segurança mínimo for definido, a versão no cliente (especificada no token do computador) deverá ser maior ou igual ao valor especificado.

Se uma lista de versões excluídas for especificada e a versão do cliente corresponder a qualquer um dos identificadores de versão na lista, o cliente não poderá usar um direito contendo essa instância ModuleRequirements. Para que um módulo corresponda às informações da versão, todos os parâmetros especificados nas informações da versão, exceto a versão de lançamento, devem corresponder exatamente aos valores dos módulos. A versão de lançamento corresponde se o valor do módulo do cliente for menor ou igual ao valor nas informações de versão.

Caso uma violação seja relatada com um cliente DRM específico ou uma versão de tempo de execução, o proprietário do conteúdo e o distribuidor de conteúdo (que executa o servidor de licenças) podem configurar o servidor para recusar a emissão de licenças durante um período em que o Adobe não tenha uma correção disponível. Isso pode ser configurado por meio da variável `HandlerConfiguration` conforme descrito acima, ou fazendo alterações em todas as políticas de DRM. No último caso, é possível manter uma lista de atualização de política DRM e usá-la para verificar se uma política DRM foi atualizada ou revogada.

Se você precisar de uma versão mais recente do Flash Player Adobe/Adobe AIR Runtime ou da biblioteca Adobe Content Protection (módulo DRM), será necessário atualizar suas políticas de DRM.

Consulte [Atualização de uma política usando a API Java](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md).

Em seguida, é necessário criar uma Lista de atualização de política DRM ou definir restrições em `HandlerConfiguration` chamando `HandlerConfiguration.setRuntimeModuleRequirements()` ou `HandlerConfiguration.setDRMModuleRequirements()`. Quando um usuário solicita uma nova licença com as listas de bloqueios especificadas ativadas, é necessário instalar os tempos de execução e as bibliotecas mais recentes para que uma licença possa ser emitida.

Consulte o código de amostra em [Atualizando uma política usando a API Java Para obter um exemplo de listas de bloqueios de versões DRM e de tempo de execução](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md) para obter um exemplo sobre as versões de DRM e tempo de execução da listagem de bloqueios.
