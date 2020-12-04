---
seo-title: Processar solicitações de registro de domínio
title: Processar solicitações de registro de domínio
uuid: d92db6c2-5a16-41ea-a1aa-541c59780678
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---


# Processar solicitações de registro de domínio {#handle-domain-registration-requests}

Se os metadados do DRM indicarem que o registro de domínio é necessário para reproduzir o conteúdo, o aplicativo cliente deve chamar a API do ActionScript `DRMManager.addToDeviceGroup()` ou a API do iOS `joinLicenseDomain()`. Se o cliente ainda não se registrou no servidor de domínio especificado (ou se o aplicativo está forçando uma nova adesão), uma solicitação de registro de domínio é enviada. O servidor de domínio determina se o cliente tem permissão para ingressar em um domínio e emite uma ou mais credenciais de domínio para o cliente.

* A classe do manipulador de solicitações é `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* A classe de mensagem de solicitação é `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* Se o protocolo de suporte do cliente e do servidor versão 5, o URL da solicitação será &quot;URL do servidor de domínio nos metadados: + &quot; [!DNL /flashaccess/domain/v4]&quot;. Caso contrário, o URL da solicitação será o URL do Servidor de Domínio nos metadados&quot; + &quot; [!DNL /flashaccess/domain/v3]&quot;

Ao inicializar o `DomainRegistrationHandler`, você deve especificar o URL do servidor de domínio. Esse URL é incluído nos tokens de domínio emitidos pelo manipulador para indicar ao servidor de domínio que o token foi emitido. O URL deve corresponder ao URL do servidor de domínio especificado em qualquer política DRM que exija o registro do domínio no servidor.

Para determinar se o cliente tem permissão para ingressar no domínio, o servidor pode examinar as informações do computador e do usuário na solicitação. O servidor também pode determinar que domínio o cliente tem permissão para ingressar.

>[!NOTE]
>
>Um cliente só pode ser membro de um domínio por URL do servidor de domínio. Se o computador já tiver um token de domínio para este URL do servidor de domínio, a solicitação de registro de domínio incluirá o nome de domínio atual ( `getRequestDomainName()`).

Para uma solicitação de nova adesão, o servidor de domínio deve retornar o conjunto atual de credenciais de domínio para este domínio ou retornar um erro. O servidor de domínio pode não retornar as credenciais de domínio para um domínio diferente.

Consulte [Usando identificadores de máquina](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#use-machine-identifiers) para obter informações sobre como identificar e contar máquinas que ingressam no domínio.

Se o servidor de domínio exigir autenticação para ingressar em um domínio, a solicitação deverá conter um token de autenticação. Assim como com uma solicitação de licença, o registro de domínio pode exigir nome de usuário/senha ou autenticação personalizada.

Consulte [Autenticação do usuário](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#user-authentication) para obter detalhes sobre como gerenciar tokens de autenticação.

O servidor de domínio é responsável por armazenar e gerenciar as chaves de domínio associadas a cada domínio. Quando um novo par de chaves precisa ser gerado para um domínio (o primeiro registro de domínio para o domínio), você precisa chamar `generateDomainCredential(String, int, Principal, Date)`. Este método gera um novo par de chaves de domínio e certificado de domínio. O servidor de domínio deve armazenar a chave privada e o certificado e fornecer esses objetos ao processar solicitações subsequentes para esse domínio. Também é possível gerar um novo par de chaves para um domínio para rolar sobre as chaves. Ao passar o mouse sobre as chaves de um domínio específico, certifique-se de incrementar a versão principal em `generateDomainCredential`.

Cada vez que uma máquina se registra com o mesmo domínio, a mesma chave privada e o mesmo certificado de domínio devem ser usados. Chame `addDomainCredential(DomainToken, PrivateKey)` para retornar uma credencial de domínio existente ao cliente. Se houver várias credenciais de domínio para o domínio porque as chaves de domínio foram alteradas, o servidor deverá fornecer credenciais de domínio para a chave de domínio atual e todas as chaves de domínio anteriores para que o cliente possa consumir licenças vinculadas a chaves de domínio mais antigas. Isso permite que uma licença vinculada a um token de domínio antigo seja movida para uma máquina recém-registrada e ainda possa ser reproduzida.
