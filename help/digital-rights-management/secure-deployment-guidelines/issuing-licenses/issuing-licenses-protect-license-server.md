---
description: Você deve se certificar de que está emitindo licenças com segurança. Considere estas práticas recomendadas para proteger o License Server
title: Protegendo o License Server
exl-id: 88b8f44f-c140-4cbc-be0a-f67058548fc3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 0%

---

# Protegendo o License Server {#protecting-the-license-server}

Você deve se certificar de que está emitindo licenças com segurança. Considere estas práticas recomendadas para proteger o License Server:

## Consumindo CRLs geradas localmente {#consuming-locally-generated-crls}

Para consumir listas de certificados revogados (CRLs) geradas localmente e listas de atualização de políticas, use as APIs do Adobe Primetime DRM para verificar a assinatura.

As APIs a seguir verificam se as listas não foram adulteradas e se as listas foram assinadas pelo License Server correto:

* Chame [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) para verificar a assinatura antes de fornecer a [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) a qualquer API.

   Para obter mais informações, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Chame [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) para verificar a assinatura antes de fornecer a `PolicyUpdateList` a qualquer API.

   Para obter mais informações, consulte [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

## Consumindo CRLs publicadas pelo Adobe{#consuming-crls-published-by-adobe}

O SDK baixa periodicamente as CRLs publicadas pelo Adobe. Você deve garantir que o acesso a esses arquivos não seja bloqueado ou que a imposição dessas CRLs não seja impedida.

O SDK tem uma opção de configuração para ignorar erros ao recuperar CRLs de Adobe, e você só pode aplicar essa opção em ambientes de desenvolvimento. Em ambientes de produção, o servidor de licenças deve recuperar as CRLs do Adobe. Ocorreu um erro se o servidor de licenças não puder obter uma CRL válida.

## Gerar CRLs para complementar aquelas publicadas pelo Adobe{#generating-crls-to-supplement-those-published-by-adobe}

Você pode usar o Adobe Primetime DRM para criar CRLs que complementam a CRL da máquina publicada pelo Adobe.

O SDK do DRM do Primetime verifica e impõe as CRLs de Adobe. No entanto, você pode não permitir máquinas clientes adicionais criando uma CRL que revogue credenciais de máquina adicionais transmitindo a CRL para o SDK DRM do Primetime. Quando você emite uma licença, o SDK verifica a CRL do Adobe e a CRL.

Para gerar CRLs, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

## Detecção de reversão {#rollback-detection}

Se sua implementação do Adobe Primetime DRM usar regras de negócios que exigem que o cliente mantenha o estado (por exemplo, o intervalo da janela de reprodução), o Adobe recomenda que o servidor acompanhe o contador de reversão e use o AIR ou a lista de permissões do SWF.

O contador de reversão é enviado ao servidor na maioria das solicitações do cliente. Se a implementação do PRIMETIME DRM não exigir o contador de reversão, ele poderá ser ignorado. Caso contrário, a Adobe recomenda que o servidor armazene a ID de máquina aleatória, que é obtida usando [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())e o valor do contador atual em um banco de dados.

Para obter mais informações sobre como incrementar e rastrear o contador de reversão, consulte [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) e a detecção de reversão.

## Contagem de máquinas ao emitir licenças {#machine-count-when-issuing-licenses}

Se as regras de negócios exigirem que o número de máquinas para um usuário seja rastreado, o Servidor de licenças ou o Servidor de domínio deverá armazenar as IDs de máquina associadas ao usuário.

A maneira mais eficiente de rastrear IDs de máquina é armazenar o valor retornado pela variável [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) em um banco de dados. Quando uma nova solicitação for recebida, compare a ID da máquina na solicitação com as IDs de máquina conhecidas usando [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) O executa uma comparação de IDs para determinar se as IDs representam a mesma máquina. Essa comparação só será prática se houver um pequeno número de IDs de máquina. Por exemplo, se os usuários tiverem permissão para cinco máquinas em seu domínio, você poderá pesquisar no banco de dados as IDs de máquina associadas ao nome de usuário do usuário e obter um pequeno conjunto de dados para comparação.

Essa comparação não é prática para implantações que permitem acesso anônimo. Nesse caso, [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) pode ser usado. No entanto, essa ID não pode ser a mesma se o usuário acessar o conteúdo do Flash e do Adobe AIR® Runtimes.

>[!NOTE]
>
>A ID não sobrevive se o usuário reformatar o disco rígido.

## Proteção contra repetição {#replay-protection}

A proteção contra repetição impede que um invasor reproduza uma mensagem de solicitação de licença e, possivelmente, cause um ataque de negação de serviço (DoS) contra o cliente.

Um ataque de DoS é uma tentativa dos invasores de impedir que usuários legítimos de um serviço usem esse serviço. Por exemplo, um ataque de repetição que usa o contador de reversão pode ser usado para &quot;enganar&quot; o License Server para que ele pense que o cliente DRM reverteu seu estado, o que causa uma suspensão da conta.

Para saber mais sobre a proteção de repetição, consulte [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).

## Mantenha uma lista de permissões de empacotadores de conteúdo confiáveis {#maintain-a-allowlist-of-trusted-content-packagers}

Uma lista de permissões é uma lista de entidades confiáveis.

Para os empacotadores de conteúdo, as entidades são organizações nas quais o proprietário do conteúdo confia para empacotar (ou criptografar) os arquivos de vídeo e criar conteúdo protegido por DRM. Ao implantar o Adobe Primetime DRM, você deve manter uma lista de permissões de compactadores de conteúdo confiáveis. Você também deve verificar a identidade do empacotador de conteúdo nos metadados de DRM de um arquivo protegido por DRM antes de emitir uma licença.

Para saber como obter informações sobre a entidade que compactou o conteúdo, consulte [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).

## Tempo limite para tokens de autenticação{#timeout-for-authentication-tokens}

Todos os tokens de autenticação gerados pelo SDK do Adobe Primetime DRM têm um intervalo de tempo limite para proteger a segurança do aplicativo.

A expiração do token de autenticação é especificada ao usar o SDK DRM do Primetime ao manipular uma solicitação de autenticação. Após a expiração, o token não é mais válido e o usuário deve se autenticar novamente no servidor de licenças.

Para saber mais sobre solicitações de autenticação, consulte [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).

## Substituição de opções de política {#overriding-policy-options}

Ao emitir uma licença, o servidor de licenças pode substituir as regras de uso especificadas na política.

Se a política especificar uma data de início, uma licença não será gerada antes dessa data de início. No entanto, você pode definir uma data de início futura na licença após ela ter sido gerada. Essa opção deve ser usada com cuidado, pois o cliente não pode impedir o usuário de adiantar o tempo do sistema para contornar a data de início.
