---
description: 'Você deve garantir que está emitindo licenças com segurança. Considere essas práticas recomendadas para proteger o License Server '
title: Protegendo o servidor de licenças
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 0%

---


# Protegendo o Servidor de Licenças {#protecting-the-license-server}

Você deve garantir que está emitindo licenças com segurança. Considere estas práticas recomendadas para proteger o License Server:

## Consumo de CRLs geradas localmente {#consuming-locally-generated-crls}

Para consumir listas de revogação de certificados (CRLs) geradas localmente e listas de atualização de políticas, use as APIs de DRM do Adobe Primetime para verificar a assinatura.

As APIs a seguir verificam se as listas não foram violadas e se as listas foram assinadas pelo License Server correto:

* Chame [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) para verificar a assinatura antes de fornecer o [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) para qualquer API.

   Para obter mais informações, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Chame [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) para verificar a assinatura antes de fornecer `PolicyUpdateList` a qualquer APIs.

   Para obter mais informações, consulte [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

## Consumo de CRLs publicadas por Adobe{#consuming-crls-published-by-adobe}

O SDK baixa periodicamente CRLs publicadas pelo Adobe. Você deve garantir que o acesso a esses arquivos não seja bloqueado ou que a aplicação desses CRLs não seja impedida.

O SDK tem uma opção de configuração para ignorar erros ao recuperar CRLs de Adobe e você só pode aplicar essa opção em ambientes de desenvolvimento. Em ambientes de produção, o servidor de licenças deve recuperar as CRLs do Adobe. Se o servidor de licenças não conseguir obter uma CRL válida, ocorreu um erro.

## Geração de CRLs para complementar aqueles publicados pelo Adobe{#generating-crls-to-supplement-those-published-by-adobe}

Você pode usar o Adobe Primetime DRM para criar CRLs que complementam a CRL da máquina publicada pelo Adobe.

O SDK de DRM do Primetime verifica e aplica as CRLs do Adobe. No entanto, você pode não permitir máquinas cliente adicionais criando uma CRL que revoga credenciais de máquina adicionais transmitindo a CRL para o SDK de DRM do Primetime. Ao emitir uma licença, o SDK verifica a CRL do Adobe e a CRL.

Para gerar CRLs, consulte [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

## Detecção de reversão {#rollback-detection}

Se a implementação do DRM da Adobe Primetime usar regras de negócios que exigem que o cliente mantenha o estado (por exemplo, o intervalo da janela de reprodução), o Adobe recomenda que o servidor acompanhe o contador de reversão e use a lista de permissões AIR ou SWF.

O contador de reversão é enviado ao servidor na maioria das solicitações do cliente. Se a implementação do DRM do Primetime não exigir o contador de reversão, ele poderá ser ignorado. Caso contrário, o Adobe recomenda que o servidor armazene a ID de máquina aleatória, que é obtida usando [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()), e o valor do contador atual em um banco de dados.

Para obter mais informações sobre como incrementar e rastrear o contador de reversão, consulte [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) e a Detecção de reversão.

## Contagem de máquina ao emitir licenças {#machine-count-when-issuing-licenses}

Se as regras de negócios exigirem que o número de máquinas para um usuário seja rastreado, o License Server ou o Domain Server deverá armazenar as IDs do computador associadas ao usuário.

A maneira mais robusta de rastrear IDs de máquina é armazenar o valor retornado pelo método [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) em um banco de dados. Quando uma nova solicitação for recebida, compare a ID da máquina na solicitação com as IDs da máquina conhecidas usando [MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.matches()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) realiza uma comparação de IDs para determinar se as IDs representam a mesma máquina. Essa comparação só é prática se houver um pequeno número de IDs de máquina. Por exemplo, se os usuários tiverem permissão para cinco computadores em seus domínios, você poderá pesquisar o banco de dados para as IDs de máquina associadas ao nome de usuário do usuário e obter um pequeno conjunto de dados para comparação.

Essa comparação não é prática para implantações que permitem acesso anônimo. Nesse caso, [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) pode ser usado. No entanto, essa ID não pode ser a mesma se o usuário acessar o conteúdo do Flash e dos tempos de execução do Adobe AIR®.

>[!NOTE]
>
>A ID não sobrevive se o usuário reformatar o disco rígido.

## Reproduzir proteção {#replay-protection}

A proteção de repetição impede que um invasor reproduza uma mensagem de solicitação de licença e possivelmente causa um ataque de negação de serviço (DoS) contra o cliente.

Um ataque do DoS é uma tentativa dos atacantes de impedir que usuários legítimos de um serviço usem esse serviço. Por exemplo, um ataque de repetição que usa o contador de reversão poderia ser usado para &quot;enganar&quot; o License Server e pensar que o cliente DRM reverteu seu estado, o que causa uma suspensão da conta.

Para saber mais sobre a proteção de repetição, consulte [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).

## Manter uma lista de permissões de pacotes de conteúdo confiáveis {#maintain-a-allowlist-of-trusted-content-packagers}

Uma lista de permissões é uma lista de entidades confiáveis.

Para pacotes de conteúdo, as entidades são organizações confiáveis pelo proprietário do conteúdo para empacotar (ou criptografar) os arquivos de vídeo e criar conteúdo protegido por DRM. Ao implantar o Adobe Primetime DRM, você deve manter uma lista de permissões de pacotes de conteúdo confiáveis. Você também deve verificar a identidade do pacote de conteúdo nos metadados DRM de um arquivo protegido por DRM antes de emitir uma licença.

Para saber como obter informações sobre a entidade que empacotou o conteúdo, consulte [V2ContentMetaData.getPackagerInfo()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/media/drm/keys/v2/V2ContentMetaData.html#getPackagerInfo()).

## Tempo limite para tokens de autenticação{#timeout-for-authentication-tokens}

Todos os tokens de autenticação gerados pelo SDK do DRM da Adobe Primetime têm um intervalo de tempo limite para proteger a segurança do aplicativo.

A expiração do token de autenticação é especificada e use o SDK de DRM do Primetime ao manipular uma solicitação de autenticação. Depois de expirar, o token não é mais válido e o usuário deve autenticar novamente com o servidor de licenças.

Para saber mais sobre solicitações de autenticação, consulte [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).

## Substituição das opções de política {#overriding-policy-options}

Ao emitir uma licença, o servidor de licenças pode substituir as regras de uso especificadas na política.

Se a política especificar uma data de início, uma licença não será gerada antes dessa data de início. No entanto, é possível definir uma data de início futura na licença após a criação da licença. Essa opção deve ser usada com cuidado, pois o cliente não pode impedir que o usuário avance a hora do sistema para contornar a data de início.