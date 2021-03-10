---
title: Gerenciar solicitações de registro de domínio
description: Gerenciar solicitações de registro de domínio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---


# Gerenciar solicitações de registro de domínio {#handle-domain-registration-requests}

Se os metadados de DRM indicarem que o registro de domínio é necessário para reproduzir o conteúdo, o aplicativo cliente deverá chamar a API do ActionScript `DRMManager.addToDeviceGroup()` ou a API do iOS `joinLicenseDomain()`. Se o cliente ainda não tiver se registrado no servidor de domínio especificado (ou se o aplicativo estiver forçando uma nova associação), uma solicitação de registro de domínio será enviada. O servidor de domínio determina se o cliente tem permissão para ingressar em um domínio e emite uma ou mais credenciais de domínio para o cliente.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* A classe da mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* Se o cliente e o servidor tiverem suporte para a versão 5 do protocolo, o URL da solicitação será &quot;URL do servidor de domínio nos metadados: + &quot; [!DNL /flashaccess/domain/v4]&quot;. Caso contrário, o URL da solicitação será o URL do servidor de domínio nos metadados&quot; + &quot; [!DNL /flashaccess/domain/v3]&quot;

Ao inicializar o `DomainRegistrationHandler`, você deve especificar o URL do servidor de domínio. Esse URL é incluído nos tokens de domínio emitidos pelo manipulador para indicar ao servidor de domínio que o token foi emitido. O URL deve corresponder ao URL do servidor de domínio especificado em qualquer política de DRM que exija o registro do domínio com o servidor.

Para determinar se o cliente tem permissão para ingressar no domínio, o servidor pode examinar a máquina e as informações do usuário na solicitação. O servidor também pode determinar em qual domínio o cliente tem permissão para ingressar.

>[!NOTE]
>
>Um cliente só pode ser membro de um domínio por URL de servidor de domínio. Se a máquina já tiver um token de domínio para esse URL de servidor de domínio, a solicitação de registro de domínio incluirá o nome de domínio atual ( `getRequestDomainName()`).

Para uma solicitação de reassociação, o servidor de domínio deve retornar o conjunto atual de credenciais de domínio para esse domínio ou retornar um erro. O servidor de domínio pode não retornar as credenciais de domínio para um domínio diferente.

Consulte [Usando identificadores de máquina](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#use-machine-identifiers) para obter informações sobre como identificar e contar máquinas que estão ingressando no domínio.

Se o servidor de domínio exigir autenticação para ingressar em um domínio, a solicitação deverá conter um token de autenticação. Assim como com uma solicitação de licença, o registro de domínio pode exigir nome de usuário/senha ou autenticação personalizada.

Consulte [Autenticação do usuário](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#user-authentication) para obter detalhes sobre como gerenciar tokens de autenticação.

O servidor de domínio é responsável por armazenar e gerenciar as chaves de domínio associadas a cada domínio. Quando um novo par de chaves precisa ser gerado para um domínio (o primeiro registro de domínio do domínio), você precisa chamar `generateDomainCredential(String, int, Principal, Date)`. Esse método gera um novo par de chaves de domínio e certificado de domínio. O servidor de domínio deve armazenar a chave privada e o certificado e fornecer esses objetos ao processar solicitações subsequentes para esse domínio. Também é possível gerar um novo par de chaves para um domínio para passar as chaves. Ao passar o mouse sobre as chaves de um domínio específico, incremente a versão da chave em `generateDomainCredential`.

Sempre que uma máquina se registrar no mesmo domínio, a mesma chave privada de domínio e o mesmo certificado devem ser usados. Chame `addDomainCredential(DomainToken, PrivateKey)` para retornar uma credencial de domínio existente ao cliente. Se houver várias credenciais de domínio para o domínio porque elas foram alteradas, o servidor deverá fornecer credenciais de domínio para a chave de domínio atual e todas as chaves de domínio anteriores, para que o cliente possa consumir licenças vinculadas a chaves de domínio mais antigas. Isso permite que uma licença vinculada a um token de domínio antigo seja movida para uma máquina recentemente registrada e ainda possa ser reproduzida.
