---
title: Lidar com solicitações de Registro de domínio
description: Lidar com solicitações de Registro de domínio
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# Lidar com solicitações de Registro de domínio{#handling-domain-registration-requests}

Se os metadados de DRM indicarem que o registro de domínio é necessário para reproduzir o conteúdo, o aplicativo cliente deverá chamar a API do ActionScript DRMManager.addToDeviceGroup() ou a API do iOS joinLicenseDomain(). Se o cliente ainda não tiver se registrado no servidor de domínio especificado (ou se o aplicativo estiver forçando uma reassociação), uma solicitação de registro de domínio será enviada. O servidor de domínio determina se o cliente tem permissão para ingressar em um domínio e emite uma ou mais credenciais de domínio para o cliente.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* Se tanto o cliente quanto o servidor suportam o protocolo versão 5, o URL da solicitação é &quot;Domain Server URL in metadata: + &quot;/flashaccess/domain/v4&quot;. Caso contrário, o URL da solicitação será o URL do servidor do domínio nos metadados&quot; + &quot;/flashaccess/domain/v3&quot;

Ao inicializar o `DomainRegistrationHandler`, a URL do servidor de domínio deve ser especificada. Esse URL será incluído nos tokens de domínio emitidos pelo manipulador para indicar o servidor de domínio que emitiu o token. A URL deve corresponder à URL do servidor de domínio especificada em qualquer política que exija o registro do domínio no servidor.

Para determinar se o cliente tem permissão para ingressar no domínio, o servidor pode examinar as informações do computador e do usuário na solicitação. Consulte [Utilização de identificadores de máquina](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-using-machine-ids.md) para obter informações sobre como identificar e contar computadores que ingressam no domínio. O servidor também pode determinar em qual domínio o cliente tem permissão para ingressar. Observe que um cliente só pode ser membro de um domínio por URL de servidor de domínio. Se o computador já tiver um token de domínio para este URL do servidor de domínio, a solicitação de registro de domínio incluirá o nome de domínio atual ( `getRequestDomainName()`). Para uma solicitação de reingresso, o servidor de domínio deve retornar o conjunto atual de credenciais de domínio para este domínio ou retornar um erro (o servidor de domínio pode não retornar as credenciais de domínio para um domínio diferente).

Se o servidor de domínio exigir autenticação para ingressar em um domínio, a solicitação deverá conter um token de autenticação. Assim como em uma solicitação de licença, o registro de domínio pode exigir nome de usuário/senha ou autenticação personalizada. Consulte [Autenticação do usuário](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-authentication/content-user-authentication.md) para obter detalhes sobre como manipular tokens de autenticação.

O servidor de domínio é responsável por armazenar e gerenciar as chaves de domínio associadas a cada domínio. Quando um novo par de chaves precisar ser gerado para um domínio (o primeiro registro de domínio do domínio), chame `generateDomainCredential` `(String, int, Principal, Date)`. Este método gerará um novo par de chaves de domínio e um novo certificado de domínio. O servidor de domínio deve armazenar a chave privada e o certificado e fornecer esses objetos ao processar solicitações subsequentes para esse domínio. Também é possível gerar um novo par de chaves para um domínio para substituir as chaves. Ao rolar sobre as chaves de um domínio específico, certifique-se de incrementar a versão da chave em `generateDomainCredential` também.

Cada vez que uma máquina se registra no mesmo domínio, a mesma chave privada e o mesmo certificado de domínio devem ser usados. Chamar `addDomainCredential(DomainToken, PrivateKey)` para retornar uma credencial de domínio existente ao cliente. Se houver várias credenciais de domínio para o domínio porque as chaves de domínio foram alteradas, o servidor deverá fornecer credenciais de domínio para a chave de domínio atual e todas as chaves de domínio anteriores para que o cliente possa consumir licenças vinculadas a chaves de domínio mais antigas. Isso permite que uma licença associada a um token de domínio antigo seja movida para uma máquina recém-registrada e ainda possa ser reproduzida.
