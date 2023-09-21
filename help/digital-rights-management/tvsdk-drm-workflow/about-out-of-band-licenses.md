---
title: Visão geral das licenças fora de banda
description: Visão geral das licenças fora de banda
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Licenças fora de banda {#out-of-band-licenses}

As licenças também podem ser obtidas fora de banda (sem entrar em contato com um servidor de licenças do Primetime DRM), armazenando a licença em disco e na memória usando o `storeVoucher()` método.

Para reproduzir vídeos criptografados no Primetime, o respectivo tempo de execução precisa obter a licença para esse vídeo. A licença contém a chave de descriptografia do vídeo e é gerada pelo servidor de licença do Primetime DRM implantado pelo cliente.

O tempo de execução geralmente obtém essa licença enviando uma solicitação de licença ao servidor de licença do Primetime DRM indicado nos metadados DRM do vídeo ( `DRMContentData` classe). O aplicativo pode acionar essa solicitação de licença chamando o `DRMManager.loadVoucher()` método.

`DRMManager.storeVoucher()` permite que o aplicativo envie licenças obtidas fora da faixa. O tempo de execução pode então ignorar o processo de solicitação de licença e usar as licenças encaminhadas para reproduzir vídeos criptografados. A licença ainda precisa ser gerada pelo servidor de licença do Primetime DRM antes que possa ser obtida fora da faixa. No entanto, você tem a opção de hospedar as licenças em qualquer servidor HTTP, em vez de um servidor de licença DRM do Primetime.

`DRMManager.storeVoucher()` O também é usado para suportar o compartilhamento de licenças entre vários dispositivos. Após o Primetime DRM 3.0, esse recurso é conhecido como &quot;Suporte ao domínio do dispositivo&quot;. Se a implantação der suporte a esse caso de uso, você poderá registrar vários computadores em um grupo de dispositivos usando o `DRMManager.addToDeviceGroup()` método. Se houver um computador com uma licença válida vinculada a domínio para um determinado conteúdo, o aplicativo poderá extrair a licença serializada usando o `DRMVoucher.toByteArray()` e em outros computadores, você pode importar as licenças usando o `DRMManager.storeVoucher()` método.

## Sobre o registro de dispositivos {#about-device-registration}

Todas as licenças de DRM do Primetime, no momento da criação, devem ser vinculadas a uma entidade final. A vinculação é o processo criptográfico que permite que apenas uma entidade específica consuma a licença. Isso é necessário para evitar &quot;licenças flutuantes&quot; que podem ser usadas por qualquer dispositivo arbitrário. Para que o Primetime DRM &quot;pré-gere&quot; licenças, isso significa que o &quot;destino&quot; dessas licenças pré-geradas deve ser conhecido antecipadamente. O DRM do Primetime se refere a isso como &quot;Registro do dispositivo&quot;.

## Registrar um dispositivo {#register-a-device}

Vamos supor que você tenha executado as seguintes tarefas:

* Você configurou o SDK do servidor DRM Primetime.
* Você configurou um servidor HTTP para emitir licenças pré-geradas.
* Você criou um aplicativo Primetime para exibir o conteúdo protegido.

 A fase de registro do dispositivo envolve as seguintes ações:

1. O aplicativo cria uma ID gerada aleatoriamente.
1. O aplicativo invoca a variável `DRMManager.authenticate()` método. O aplicativo deve incluir a ID gerada aleatoriamente na solicitação de autenticação. Por exemplo, inclua a ID no campo de nome de usuário.
1. A ação mencionada na Etapa 2 resultará no envio de uma solicitação de autenticação do DRM do Primetime para o servidor do cliente. Essa solicitação inclui o certificado do dispositivo:
   1. O servidor extrai o certificado do dispositivo e a ID gerada da solicitação e armazena.
   1. O subsistema do cliente pré-gera licenças para esse certificado de dispositivo, armazena e concede acesso a ele de uma maneira que as associa à ID gerada. .
1. O servidor responde à solicitação com uma mensagem de &quot;êxito&quot;.
1. O aplicativo armazena a ID gerada.

Após o registro do dispositivo, o aplicativo usa a ID gerada da mesma forma que usaria a ID do dispositivo no esquema anterior:
1. O aplicativo tentará localizar a ID gerada.
1. Se a ID gerada for encontrada, o aplicativo usará a ID gerada ao baixar as licenças pré-geradas. O aplicativo enviará as licenças ao cliente DRM do Primetime para consumo usando o `DRMManager.storeVoucher()` método. .
1. Se a ID gerada não for encontrada, o aplicativo passará pelo procedimento de registro do dispositivo.

## Redefinição de fábrica DRM {#drm-factory-reset}

Quando o usuário do dispositivo chamar a opção de redefinição de fábrica do DRM, o certificado do dispositivo será apagado. Para continuar a reproduzir o conteúdo protegido, o aplicativo deve passar pelo procedimento de registro do dispositivo novamente. Se o aplicativo enviar uma licença pré-gerada desatualizada, o cliente DRM do Primetime a rejeitará, pois a licença foi criptografada para uma ID de dispositivo mais antiga.

* API do Flash: [DRMManager.resetDRMVouchers()](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html#resetDRMVouchers()) - (Só pode ser chamado em resposta a determinados códigos de erro DRM irrecuperáveis.)
* API do iOS: [DRMManager resetDRM](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a0dd6c9662428583196e0419d3ea69446)
* API do Android: [DRMManager.resetDRM()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#resetDRM(com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))
