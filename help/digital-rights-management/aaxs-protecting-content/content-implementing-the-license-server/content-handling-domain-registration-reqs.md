---
title: Lidar com solicitações de registro de domínio
description: Lidar com solicitações de registro de domínio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---


# Lidar com solicitações de registro de domínio{#handling-domain-registration-requests}

Se os metadados de DRM indicarem que o registro de domínio é necessário para reproduzir o conteúdo, o aplicativo cliente deve chamar a API de ActionScript DRMManager.addToDeviceGroup() ou a API do iOS joinLicenseDomain(). Se o cliente ainda não tiver se registrado no servidor de domínio especificado (ou se o aplicativo estiver forçando uma nova associação), uma solicitação de registro de domínio será enviada. O servidor de domínio determina se o cliente tem permissão para ingressar em um domínio e emite uma ou mais credenciais de domínio para o cliente.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* A classe da mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* Se o cliente e o servidor tiverem suporte para a versão 5 do protocolo, o URL da solicitação será &quot;URL do servidor de domínio nos metadados: + &quot;/flashaccess/domain/v4&quot;. Caso contrário, o URL da solicitação será o URL do Servidor de Domínio em metadados&quot; + &quot;/flashaccess/domain/v3&quot;

Ao inicializar o `DomainRegistrationHandler`, o URL do servidor de domínio deve ser especificado. Esse URL será incluído nos tokens de domínio emitidos pelo manipulador para indicar o servidor de domínio que emitiu o token. O URL deve corresponder ao URL do servidor de domínio especificado em qualquer política que exija o registro de domínio com o servidor.

Para determinar se o cliente tem permissão para ingressar no domínio, o servidor pode examinar a máquina e as informações do usuário na solicitação. Consulte [Usando identificadores de máquina](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-using-machine-ids.md) para obter informações sobre como identificar e contar máquinas que estão ingressando no domínio. O servidor também pode determinar em qual domínio o cliente tem permissão para ingressar. Observe que um cliente só pode ser membro de um domínio por URL de servidor de domínio. Se a máquina já tiver um token de domínio para esse URL de servidor de domínio, a solicitação de registro de domínio incluirá o nome de domínio atual ( `getRequestDomainName()`). Para uma solicitação de reassociação, o servidor de domínio deve retornar o conjunto atual de credenciais de domínio para esse domínio ou retornar um erro (o servidor de domínio pode não retornar as credenciais de domínio para um domínio diferente).

Se o servidor de domínio exigir autenticação para ingressar em um domínio, a solicitação deverá conter um token de autenticação. Assim como com uma solicitação de licença, o registro de domínio pode exigir nome de usuário/senha ou autenticação personalizada. Consulte [Autenticação do usuário](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-authentication/content-user-authentication.md) para obter detalhes sobre como lidar com tokens de autenticação.

O servidor de domínio é responsável por armazenar e gerenciar as chaves de domínio associadas a cada domínio. Quando um novo par de chaves precisar ser gerado para um domínio (o primeiro registro de domínio do domínio), chame `generateDomainCredential` `(String, int, Principal, Date)`. Esse método gerará um novo par de chaves de domínio e certificado de domínio. O servidor de domínio deve armazenar a chave privada e o certificado e fornecer esses objetos ao processar solicitações subsequentes para esse domínio. Também é possível gerar um novo par de chaves para um domínio para passar as chaves. Ao passar o mouse sobre as chaves de um domínio específico, incremente a versão da chave em `generateDomainCredential` também.

Sempre que uma máquina se registrar no mesmo domínio, a mesma chave privada de domínio e o mesmo certificado devem ser usados. Chame `addDomainCredential(DomainToken, PrivateKey)` para retornar uma credencial de domínio existente ao cliente. Se houver várias credenciais de domínio para o domínio porque elas foram alteradas, o servidor deverá fornecer credenciais de domínio para a chave de domínio atual e todas as chaves de domínio anteriores, para que o cliente possa consumir licenças vinculadas a chaves de domínio mais antigas. Isso permite que uma licença vinculada a um token de domínio antigo seja movida para uma máquina recentemente registrada e ainda possa ser reproduzida.
