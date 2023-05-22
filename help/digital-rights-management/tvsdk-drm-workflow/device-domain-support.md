---
description: Normalmente, todas as licenças de DRM do Primetime, no momento da criação, estão vinculadas a um dispositivo exclusivo. Essa vinculação impede que os usuários compartilhem licenças em diferentes dispositivos sem autorização. Além da vinculação por dispositivo, o Primetime DRM oferece a capacidade de vincular licenças a um Domínio de dispositivo ou grupo de dispositivos.
title: Reproduzir conteúdo criptografado usando suporte a domínio
exl-id: 3c9badfc-046b-4c56-bde1-7b3b708bfaa2
source-git-commit: 59f7f8aa82be59c4012ee80648032600590bc4e1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Suporte a domínio de dispositivo {#device-domain-support}

Normalmente, todas as licenças de DRM do Primetime, no momento da criação, estão vinculadas a um dispositivo exclusivo. Essa vinculação impede que os usuários compartilhem licenças em diferentes dispositivos sem autorização. Além da vinculação por dispositivo, o Primetime DRM oferece a capacidade de vincular licenças a um Domínio de dispositivo ou grupo de dispositivos.

Se os metadados de conteúdo especificarem que o registro de domínio do dispositivo é necessário, o aplicativo poderá chamar uma API para ingressar em um grupo de dispositivos. Esta ação aciona uma solicitação de registro de domínio para ser enviada ao servidor de domínio. Depois que uma licença é emitida para um grupo de dispositivos, ela pode ser exportada e compartilhada com outros dispositivos que ingressaram no grupo.

As informações do grupo de dispositivos são usadas na `DRMContentData` `VoucherAccessInfo` objeto, que será usado para apresentar as informações necessárias para recuperar e consumir uma licença com êxito.

## Reproduzir conteúdo criptografado usando suporte a domínio {#play-encrypted-content-using-domain-support}

Para reproduzir conteúdo criptografado usando o Primetime DRM, execute as seguintes etapas:

1. Usar `VoucherAccessInfo.deviceGroup`, verifique se o registro do grupo de dispositivos é obrigatório.
1. Se a autenticação for necessária:
   1. Use o `DeviceGroupInfo.authenticationMethod` propriedade descubra se a autenticação é necessária.
   1. Se a autenticação for necessária, autentique o usuário executando UMA das seguintes etapas:

      * Obter o nome de usuário e a senha do usuário e chamar `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`.
      * Obter um token de autenticação em cache/pré-gerado e invocar `DRMManager.setAuthenticationToken()`.
   1. Chamar `DRMManager.addToDeviceGroup()`
1. Obtenha a licença para o conteúdo executando uma das seguintes tarefas:
   1. Use o `DRMManager.loadVoucher()` método.
   1. Obtenha a licença de um dispositivo diferente registrado no mesmo grupo de dispositivos e forneça a licença ao `DRMManager` por meio da `DRMManager.storeVoucher()` método.
1. Reproduzir o conteúdo criptografado usando o `Primetime.play()` método.
Para exportar a licença para o conteúdo, qualquer um dos dispositivos pode fornecer os bytes brutos da licença usando o `DRMVoucher.toByteArray()` após obter a licença do servidor de licenças do Primetime DRM. Os provedores de conteúdo normalmente limitam o número de dispositivos em um grupo de dispositivos. Se o limite for atingido, talvez seja necessário chamar o `DRMManager.removeFromDeviceGroup()` em um dispositivo não utilizado antes de registrar o dispositivo atual.
