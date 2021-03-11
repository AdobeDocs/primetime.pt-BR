---
title: Revogando credenciais de cliente e tempo de execução do DRM
description: Revogando credenciais de cliente e tempo de execução do DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# Revogando credenciais de cliente e tempo de execução do DRM {#revoking-drm-client-and-runtime-credentials}

As versões de DRM/Tempo de execução são identificadas pelo nível de segurança, número de versão e outros atributos, incluindo Sistema operacional e tempo de execução. Para restringir as versões de DRM/Tempo de Execução permitidas, defina as restrições do módulo em uma política de DRM ou em um `HandlerConfiguration`. As restrições de módulo podem incluir um nível mínimo de segurança e uma lista de versões de módulo que não podem ser emitidas licenças.

Consulte [Lista de bloqueios de clientes DRM restritos ao acesso a conteúdo protegido](../../protecting-content/introduction/usage-rules/runtime-application-restrictions/blocklist-drm-clients.md) para obter detalhes sobre os atributos usados para identificar um módulo DRM/Runtime.

Se o nível mínimo de segurança for definido, a versão no cliente (especificada no token da máquina) deverá ser maior ou igual ao valor especificado.

Se uma lista de versões excluídas for especificada e a versão do cliente corresponder a qualquer um dos identificadores de versão na lista, o cliente não poderá usar um direito contendo essa instância ModuleRequirements. Para que um módulo corresponda às informações da versão, todos os parâmetros especificados nas informações da versão, exceto a versão de lançamento, devem corresponder exatamente aos valores dos módulos. A versão da corresponde se o valor do módulo do cliente for menor ou igual ao valor nas informações da versão.

Caso uma violação seja relatada com um cliente DRM ou versão de tempo de execução específico, o proprietário do conteúdo e o distribuidor de conteúdo (que executa o servidor de licenças) podem configurar o servidor para recusar a emissão de licenças durante um período em que o Adobe não tem uma correção disponível. Isso pode ser configurado por meio do `HandlerConfiguration` conforme descrito acima, ou fazendo alterações em todas as políticas de DRM. No último caso, você pode manter uma lista de atualização da política de DRM e usá-la para verificar se uma política de DRM foi atualizada ou revogada.

Se você precisar de uma versão mais recente do Flash Player Adobe/Adobe AIR Runtime ou da biblioteca de proteção de conteúdo do Adobe (módulo DRM), será necessário atualizar as políticas de DRM.

Consulte [Atualização de uma política usando a API Java](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md).

Em seguida, é necessário criar uma Lista de Atualização de Política de DRM ou definir restrições em `HandlerConfiguration` chamando `HandlerConfiguration.setRuntimeModuleRequirements()` ou `HandlerConfiguration.setDRMModuleRequirements()`. Quando um usuário solicita uma nova licença com as listas de bloqueios especificadas ativadas, é necessário instalar os tempos de execução e bibliotecas mais recentes para que uma licença possa ser emitida.

Consulte o código de exemplo em [Atualizar uma política usando a API Java Para obter um exemplo sobre a listagem de blocos de versões de DRM e de tempo de execução](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md) para obter um exemplo sobre a listagem de blocos de versões de DRM e de tempo de execução.
