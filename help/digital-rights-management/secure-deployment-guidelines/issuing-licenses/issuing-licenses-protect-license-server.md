---
description: 'Você deve garantir que está emitindo licenças com segurança. Considere estas práticas recomendadas para proteger o License Server '
seo-description: 'Você deve garantir que está emitindo licenças com segurança. Considere estas práticas recomendadas para proteger o License Server '
seo-title: Protegendo o License Server
title: Protegendo o License Server
uuid: 7b5de17d-d0a7-41df-9651-4ff51c9965c6
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Protegendo o License Server {#protecting-the-license-server}

Você deve garantir que está emitindo licenças com segurança. Considere estas práticas recomendadas para proteger o License Server:

## Consumir CRLs geradas localmente {#consuming-locally-generated-crls}

Para consumir listas de revogação de certificados (CRLs) e listas de atualização de políticas geradas localmente, use as APIs DRM do Adobe Primetime para verificar a assinatura.

As APIs a seguir verificam se as listas não foram adulteradas e se as listas foram assinadas pelo License Server correto:

* Chame [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) para verificar a assinatura antes de fornecer a [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) a qualquer API.

   Para obter mais informações, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Chame [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) para verificar a assinatura antes de fornecer a `PolicyUpdateList` APIs.

   Para obter mais informações, consulte [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

## Consumir CRLs publicadas pela Adobe{#consuming-crls-published-by-adobe}

O SDK baixa periodicamente CRLs publicadas pela Adobe. Você deve garantir que o acesso a esses arquivos não esteja bloqueado ou que a aplicação dessas CRLs não seja impedida.

O SDK tem uma opção de configuração para ignorar erros ao recuperar CRLs da Adobe, e você só pode aplicar essa opção em ambientes de desenvolvimento. Em ambientes de produção, o servidor de licenças deve recuperar as CRLs da Adobe. Se o servidor de licenças não conseguir obter uma CRL válida, ocorreu um erro.

## Geração de CRLs para complementar as publicadas pela Adobe{#generating-crls-to-supplement-those-published-by-adobe}

Você pode usar o Adobe Primetime DRM para criar CRLs que complementam a CRL da máquina publicada pela Adobe.

O Primetime DRM SDK verifica e aplica as CRLs da Adobe. No entanto, você pode proibir computadores clientes adicionais criando uma CRL que revogue credenciais adicionais do computador transmitindo a CRL para o SDK do DRM Primetime. Quando você emite uma licença, o SDK verifica a Adobe CRL e sua CRL.

Para gerar CRLs, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

## Detecção de retorno {#rollback-detection}

Se sua implementação do Adobe Primetime DRM usar regras de negócios que exigem que o cliente mantenha o estado (por exemplo, o intervalo da janela de reprodução), a Adobe recomenda que o servidor rastreie o contador de reversão e use a lista de permissões AIR ou SWF.

O contador de reversão é enviado para o servidor na maioria das solicitações do cliente. Se a implementação do Primetime DRM não exigir o contador de reversão, ele poderá ser ignorado. Caso contrário, a Adobe recomenda que o servidor armazene a ID aleatória da máquina, que é obtida usando [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()), e o valor atual do contador em um banco de dados.

Para obter mais informações sobre como incrementar e rastrear o contador de reversão, consulte Detecção de [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) e Reversão.

## Contagem de máquina ao emitir licenças {#machine-count-when-issuing-licenses}

Se as regras de negócios exigirem que o número de máquinas para um usuário seja rastreado, o License Server ou o Domain Server deverá armazenar as IDs de máquina associadas ao usuário.

A maneira mais robusta de rastrear IDs de máquina é armazenar o valor retornado pelo método [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) em um banco de dados. Quando uma nova solicitação for recebida, compare a ID da máquina na solicitação com as IDs da máquina conhecidas usando [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) executa uma comparação de IDs para determinar se as IDs representam a mesma máquina. Essa comparação só é prática se houver um pequeno número de IDs de máquina. Por exemplo, se os usuários tiverem cinco computadores em seus domínios, você poderá pesquisar no banco de dados as IDs de máquina associadas ao nome de usuário do usuário e obter um pequeno conjunto de dados para comparação.

Essa comparação não é prática para implantações que permitem acesso anônimo. Nesse caso, [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) pode ser usado. No entanto, essa ID não pode ser a mesma se o usuário acessar o conteúdo dos tempos de execução do Flash e do Adobe AIR®.

>[!NOTE]
>
>A ID não sobrevive se o usuário reformatar o disco rígido.

## Proteção contra repetição {#replay-protection}

A proteção de repetição impede que um invasor reproduza uma mensagem de solicitação de licença e possivelmente causa um ataque de negação de serviço (DoS) contra o cliente.

Um ataque do DoS é uma tentativa dos atacantes de impedir que usuários legítimos de um serviço usem esse serviço. Por exemplo, um ataque de repetição que usa o contador de reversão poderia ser usado para &quot;enganar&quot; o License Server e pensar que o cliente DRM reverteu seu estado, o que causa uma suspensão da conta.

Para saber mais sobre a proteção de repetição, consulte [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).

## Manter uma lista de permissões de pacotes de conteúdo confiáveis{#maintain-a-whitelist-of-trusted-content-packagers}

Uma lista de permissões é uma lista de entidades confiáveis.

Para os empacotadores de conteúdo, as entidades são organizações confiáveis pelo proprietário do conteúdo para disponibilizar (ou criptografar) os arquivos de vídeo e criar conteúdo protegido por DRM. Ao implantar o Adobe Primetime DRM, você deve manter uma lista de permissões de pacotes de conteúdo confiáveis. Você também deve verificar a identidade do empacotador de conteúdo nos metadados DRM de um arquivo protegido por DRM antes de emitir uma licença.

Para saber como obter informações sobre a entidade que empacotou o conteúdo, consulte [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).

## Tempo limite para tokens de autenticação{#timeout-for-authentication-tokens}

Todos os tokens de autenticação gerados pelo SDK do Adobe Primetime DRM têm um intervalo de tempo limite para proteger a segurança do aplicativo.

A expiração do token de autenticação é especificada. Use o SDK do Primetime DRM ao manipular uma solicitação de autenticação. Depois de expirar, o token não é mais válido e o usuário deve autenticar novamente com o servidor de licenças.

Para saber mais sobre solicitações de autenticação, consulte [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).

## Substituição de opções de política {#overriding-policy-options}

Quando você emite uma licença, o servidor de licenças pode substituir as regras de uso especificadas na política.

Se a política especificar uma data de início, uma licença não será gerada antes dessa data de início. No entanto, você pode definir uma data inicial futura na licença depois que ela for gerada. Essa opção deve ser usada com cautela, pois o cliente não pode impedir que o usuário faça avançar o tempo do sistema para contornar a data de início.