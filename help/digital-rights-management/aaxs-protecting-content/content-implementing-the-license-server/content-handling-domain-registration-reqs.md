---
seo-title: Tratamento de solicitações de registro de domínio
title: Tratamento de solicitações de registro de domínio
uuid: e0cef9c4-b2d1-4bec-8dce-50452bc826fb
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---


# Tratamento de solicitações de registro de domínio{#handling-domain-registration-requests}

Se os metadados do DRM indicarem que o registro de domínio é necessário para reproduzir o conteúdo, o aplicativo cliente deve chamar a API do ActionScript DRMManager.addToDeviceGroup() ou a API do iOS joinLicenseDomain(). Se o cliente ainda não se registrou no servidor de domínio especificado (ou se o aplicativo está forçando uma nova adesão), uma solicitação de registro de domínio é enviada. O servidor de domínio determina se o cliente tem permissão para ingressar em um domínio e emite uma ou mais credenciais de domínio para o cliente.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* Se o protocolo de suporte do cliente e do servidor versão 5, o URL da solicitação será &quot;URL do servidor de domínio nos metadados: + &quot;/flashaccess/domain/v4&quot;. Caso contrário, o URL da solicitação será o URL do Servidor de Domínio nos metadados&quot; + &quot;/flashaccess/domain/v3&quot;

Ao inicializar o `DomainRegistrationHandler`, o URL do servidor de domínio deve ser especificado. Esse URL será incluído nos tokens de domínio emitidos pelo manipulador para indicar o servidor de domínio que emitiu o token. O URL deve corresponder ao URL do servidor de domínio especificado em qualquer política que exija o registro de domínio com o servidor.

Para determinar se o cliente tem permissão para ingressar no domínio, o servidor pode examinar as informações do computador e do usuário na solicitação. Consulte [Usando identificadores de máquina](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-using-machine-ids.md) para obter informações sobre como identificar e contar máquinas que ingressam no domínio. O servidor também pode determinar que domínio o cliente tem permissão para ingressar. Observe que um cliente só pode ser membro de um domínio por URL do servidor de domínio. Se o computador já tiver um token de domínio para este URL do servidor de domínio, a solicitação de registro de domínio incluirá o nome de domínio atual ( `getRequestDomainName()`). Para uma solicitação de nova adesão, o servidor de domínio deve retornar o conjunto atual de credenciais de domínio para este domínio ou retornar um erro (o servidor de domínio pode não retornar as credenciais de domínio para um domínio diferente).

Se o servidor de domínio exigir autenticação para ingressar em um domínio, a solicitação deverá conter um token de autenticação. Assim como com uma solicitação de licença, o registro de domínio pode exigir nome de usuário/senha ou autenticação personalizada. Consulte [Autenticação do usuário](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-authentication/content-user-authentication.md) para obter detalhes sobre como manipular tokens de autenticação.

O servidor de domínio é responsável por armazenar e gerenciar as chaves de domínio associadas a cada domínio. Quando for necessário gerar um novo par de chaves para um domínio (o primeiro registro de domínio para o domínio), chame `generateDomainCredential` `(String, int, Principal, Date)`. Este método gerará um novo par de chaves de domínio e certificado de domínio. O servidor de domínio deve armazenar a chave privada e o certificado e fornecer esses objetos ao processar solicitações subsequentes para esse domínio. Também é possível gerar um novo par de chaves para um domínio para rolar sobre as chaves. Ao passar o mouse sobre as chaves de um domínio específico, certifique-se de incrementar a versão principal em `generateDomainCredential` também.

Sempre que uma máquina se registrar no mesmo domínio, a mesma chave privada e o mesmo certificado de domínio devem ser usados. Chame `addDomainCredential(DomainToken, PrivateKey)` para retornar uma credencial de domínio existente ao cliente. Se houver várias credenciais de domínio para o domínio porque as chaves de domínio foram alteradas, o servidor deverá fornecer credenciais de domínio para a chave de domínio atual e todas as chaves de domínio anteriores para que o cliente possa consumir licenças vinculadas a chaves de domínio mais antigas. Isso permite que uma licença vinculada a um token de domínio antigo seja movida para uma máquina recém-registrada e ainda possa ser reproduzida.
