---
title: Visão geral das licenças fora de banda
description: Visão geral das licenças fora de banda
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---


# Licenças fora de banda {#out-of-band-licenses}

As licenças também podem ser obtidas fora de banda (sem entrar em contato com um servidor de licença do Primetime DRM) armazenando a licença em disco e na memória usando o método `storeVoucher()`.

Para reproduzir vídeos criptografados no Primetime, o respectivo tempo de execução precisa obter a licença para esse vídeo. A licença contém a chave de descriptografia do vídeo e é gerada pelo servidor de licenças Primetime DRM que o cliente implantou.

O tempo de execução geralmente obtém essa licença, enviando uma solicitação de licença para o servidor de licenças Primetime DRM indicado nos metadados DRM do vídeo (classe `DRMContentData` ). O aplicativo pode acionar essa solicitação de licença, chamando o método `DRMManager.loadVoucher()`.

`DRMManager.storeVoucher()` permite ao pedido enviar licenças obtidas fora de banda. O tempo de execução pode ignorar o processo de solicitação de licença e usar as licenças encaminhadas para reproduzir vídeos criptografados. A licença ainda precisa ser gerada pelo servidor de licenças Primetime DRM antes de ser obtida fora de banda. No entanto, você tem a opção de hospedar as licenças em qualquer servidor HTTP, em vez de um servidor de licenças DRM do Primetime.

`DRMManager.storeVoucher()` O também é usado para suportar o compartilhamento de licenças entre vários dispositivos. Após o Primetime DRM 3.0, esse recurso é chamado de &quot;Suporte a domínio do dispositivo&quot;. Se a implantação suportar esse caso de uso, você poderá registrar várias máquinas em um grupo de dispositivos usando o método `DRMManager.addToDeviceGroup()`. Se houver uma máquina com uma licença válida vinculada a um domínio para um determinado conteúdo, o aplicativo poderá extrair a licença serializada usando o método `DRMVoucher.toByteArray()` e, em suas outras máquinas, você poderá importar as licenças usando o método `DRMManager.storeVoucher()`.

## Sobre o registro do dispositivo {#about-device-registration}

Todas as licenças de DRM do Primetime, no momento da criação, devem ser vinculadas a uma entidade final. O vínculo é o processo criptográfico que permite somente que uma entidade específica possa consumir a licença. Tal é necessário para evitar &quot;licenças flutuantes&quot; que possam ser utilizadas por qualquer dispositivo arbitrário. Para que o DRM do Primetime &quot;pré-gere&quot; licenças, isso significa que o &quot;target&quot; dessas licenças pré-geradas deve ser conhecido com antecedência. O DRM do Primetime refere-se a isso como &quot;Registro do dispositivo&quot;.

## Registrar um dispositivo {#register-a-device}

Suponhamos que você tenha realizado as seguintes tarefas:

* Você configurou o SDK do servidor DRM do Primetime.
* Você configurou um servidor HTTP para emitir licenças pré-geradas.
* Você criou um aplicativo Primetime para exibir o conteúdo protegido.

 A fase de registro do dispositivo envolve as seguintes ações:

1. O aplicativo cria uma ID gerada aleatoriamente.
1. O aplicativo chama o método `DRMManager.authenticate()`. O aplicativo deve incluir a ID gerada aleatoriamente na solicitação de autenticação. Por exemplo, inclua a ID no campo nome de usuário.
1. A ação mencionada na Etapa 2 resultará no DRM do Primetime enviando uma solicitação de autenticação ao servidor do cliente. Essa solicitação inclui o certificado do dispositivo:
   1. O servidor extrai o certificado do dispositivo e a ID gerada da solicitação e armazena.
   1. O subsistema do cliente pré-gera licenças para esse certificado de dispositivo, as armazena e concede acesso a elas de uma forma que as associa com a ID gerada. .
1. O servidor responde à solicitação com uma mensagem de &quot;sucesso&quot;.
1. O aplicativo armazena a ID gerada.

Após o registro do dispositivo, o aplicativo usa a ID gerada da mesma forma que usaria a ID do dispositivo no esquema anterior:
1. O aplicativo tentará localizar a ID gerada.
1. Se a ID gerada for encontrada, o aplicativo usará a ID gerada ao baixar as licenças pré-geradas. O aplicativo enviará as licenças para o cliente DRM do Primetime para consumo usando o método `DRMManager.storeVoucher()`. .
1. Se a ID gerada não for encontrada, o aplicativo passará pelo procedimento de registro do dispositivo.

## Redefinição de fábrica de DRM {#drm-factory-reset}

Quando o usuário do dispositivo chamar a opção de redefinição de fábrica de DRM, o certificado do dispositivo será removido. Para continuar reproduzindo o conteúdo protegido, o aplicativo deve passar pelo procedimento de registro do dispositivo novamente. Se o aplicativo enviar uma licença pré-gerada desatualizada, o cliente DRM do Primetime a rejeitará, pois a licença foi criptografada para uma ID de dispositivo mais antiga.

* API do Flash: [DRMManager.resetDRMVouchers()](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html#resetDRMVouchers()) - (Só pode ser chamado em resposta a determinados códigos de erro de DRM não recuperáveis.)
* API do iOS: [DRMManager resetDRM](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a0dd6c9662428583196e0419d3ea69446)
* API do Android: [DRMManager.resetDRM()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#resetDRM(com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))