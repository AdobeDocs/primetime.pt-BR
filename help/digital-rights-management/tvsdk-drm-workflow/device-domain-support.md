---
description: Normalmente, todas as licenças de DRM do Primetime, no momento da criação, estão vinculadas a um dispositivo exclusivo. Esse vínculo impede que os usuários compartilhem licenças em diferentes dispositivos sem autorização. Além do vínculo por dispositivo, o DRM do Primetime fornece a capacidade de vincular licenças a um domínio do dispositivo ou a um grupo de dispositivos.
title: Reproduzir conteúdo criptografado usando o suporte de domínio
exl-id: 3c9badfc-046b-4c56-bde1-7b3b708bfaa2
source-git-commit: 59f7f8aa82be59c4012ee80648032600590bc4e1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Suporte ao domínio do dispositivo {#device-domain-support}

Normalmente, todas as licenças de DRM do Primetime, no momento da criação, estão vinculadas a um dispositivo exclusivo. Esse vínculo impede que os usuários compartilhem licenças em diferentes dispositivos sem autorização. Além do vínculo por dispositivo, o DRM do Primetime fornece a capacidade de vincular licenças a um domínio do dispositivo ou a um grupo de dispositivos.

Se os metadados de conteúdo especificarem que o registro de domínio do dispositivo é obrigatório, o aplicativo poderá chamar uma API para se associar a um grupo de dispositivos. Essa ação aciona uma solicitação de registro de domínio para ser enviada ao servidor de domínio. Depois que uma licença é emitida para um grupo de dispositivos, ela pode ser exportada e compartilhada com outros dispositivos que aderiram ao grupo de dispositivos.

As informações do grupo de dispositivos são usadas no objeto `DRMContentData` `VoucherAccessInfo`, que será usado para apresentar as informações necessárias para recuperar e consumir com êxito uma licença.

## Reproduzir conteúdo criptografado usando o suporte de domínio {#play-encrypted-content-using-domain-support}

Para reproduzir conteúdo criptografado usando o Primetime DRM , execute as seguintes etapas:

1. Usando `VoucherAccessInfo.deviceGroup`, verifique se o registro do grupo de dispositivos é necessário.
1. Se a autenticação for necessária:
   1. Use a propriedade `DeviceGroupInfo.authenticationMethod` para descobrir se a autenticação é necessária.
   1. Se a autenticação for necessária, autentique o usuário executando uma das seguintes etapas:

      * Obtenha o nome de usuário e a senha do usuário e chame `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`.
      * Obtenha um token de autenticação armazenado em cache/pré-gerado e chame `DRMManager.setAuthenticationToken()`.
   1. Chamar `DRMManager.addToDeviceGroup()`
1. Obtenha a licença do conteúdo executando uma das seguintes tarefas:
   1. Use o método `DRMManager.loadVoucher()`.
   1. Obtenha a licença de um dispositivo diferente registrado no mesmo grupo de dispositivos e forneça a licença para `DRMManager` por meio do método `DRMManager.storeVoucher()`.
1. Reproduzir o conteúdo criptografado usando o método `Primetime.play()`.
Para exportar a licença para o conteúdo, qualquer um dos dispositivos pode fornecer os bytes brutos da licença usando o método `DRMVoucher.toByteArray()` após obter a licença do servidor de licenças DRM do Primetime. Os provedores de conteúdo normalmente limitam o número de dispositivos em um grupo de dispositivos. Se o limite for atingido, talvez seja necessário chamar o método `DRMManager.removeFromDeviceGroup()` em um dispositivo não utilizado antes de registrar o dispositivo atual.
