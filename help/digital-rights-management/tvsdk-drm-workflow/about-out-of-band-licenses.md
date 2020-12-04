---
seo-title: Visão geral das licenças fora de banda
title: Visão geral das licenças fora de banda
uuid: 82e4529a-ee1b-4c0c-8885-e0e68319d1a0
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---


# Licenças fora de banda {#out-of-band-licenses}

As licenças também podem ser obtidas fora de banda (sem entrar em contato com o Primetime DRM License Server), armazenando a licença no disco e na memória usando o método `storeVoucher()`.

Para reproduzir vídeos criptografados no Primetime, o tempo de execução respectivo precisa obter a licença para esse vídeo. A licença contém a chave de decodificação do vídeo e é gerada pelo servidor de licenças Primetime DRM que o cliente implantou.

O tempo de execução geralmente obtém essa licença enviando uma solicitação de licença para o servidor de licenças Primetime DRM indicado nos metadados DRM do vídeo (classe `DRMContentData`). O aplicativo pode acionar essa solicitação de licença chamando o método `DRMManager.loadVoucher()`.

`DRMManager.storeVoucher()` permite ao pedido enviar licenças obtidas fora de banda. O tempo de execução pode ignorar o processo de solicitação de licença e usar as licenças encaminhadas para reproduzir vídeos criptografados. A licença ainda precisa ser gerada pelo servidor de licenças Primetime DRM antes de ser obtida fora de banda. No entanto, você tem a opção de hospedar as licenças em qualquer servidor HTTP, em vez de um servidor de licenças DRM Primetime.

`DRMManager.storeVoucher()` também é usada para suportar o compartilhamento de licenças entre vários dispositivos. Após o Primetime DRM 3.0, esse recurso é conhecido como &quot;Suporte ao domínio do dispositivo&quot;. Se sua implantação suportar esse caso de uso, você poderá registrar várias máquinas em um grupo de dispositivos usando o método `DRMManager.addToDeviceGroup()`. Se houver uma máquina com uma licença válida vinculada ao domínio para um determinado conteúdo, o aplicativo poderá então extrair a licença serializada usando o método `DRMVoucher.toByteArray()` e em seus outros computadores você poderá importar as licenças usando o método `DRMManager.storeVoucher()`.

## Sobre o registro do dispositivo {#about-device-registration}

Todas as licenças de DRM Primetime, no momento da criação, devem estar vinculadas a uma entidade final. O vínculo é o processo criptográfico de permitir que somente uma entidade específica possa consumir a licença. Tal é necessário para evitar &quot;licenças flutuantes&quot; que possam ser utilizadas por qualquer dispositivo arbitrário. Para o DRM Primetime &quot;pré-gerar&quot; licenças, isso significa que o &quot;público alvo&quot; dessas licenças pré-geradas deve ser conhecido antecipadamente. O DRM Primetime refere-se a isso como &quot;Registro de dispositivo&quot;.

## Registrar um dispositivo {#register-a-device}

Suponhamos que você tenha realizado as seguintes tarefas:

* Você configurou o SDK do servidor DRM Primetime.
* Você configurou um servidor HTTP para a emissão de licenças pré-geradas.
* Você criou um aplicativo Primetime para visualização do conteúdo protegido.

 A fase de registro do dispositivo envolve as seguintes ações:

1. O aplicativo cria uma ID gerada aleatoriamente.
1. O aplicativo chama o método `DRMManager.authenticate()`. O aplicativo deve incluir a ID gerada aleatoriamente na solicitação de autenticação. Por exemplo, inclua a ID no campo nome de usuário.
1. A ação mencionada na Etapa 2 resultará no DRM Primetime enviando uma solicitação de autenticação ao servidor do cliente. Esta solicitação inclui o certificado do dispositivo:
   1. O servidor extrai o certificado do dispositivo e a ID gerada da solicitação e armazena.
   1. O subsistema do cliente pré-gera licenças para esse certificado de dispositivo, as armazena e concede acesso a elas de uma forma que as associa à ID gerada. .
1. O servidor responde à solicitação com uma mensagem de &quot;sucesso&quot;.
1. O aplicativo armazena a ID gerada.

Após o registro do dispositivo, o aplicativo usa a ID gerada da mesma forma que usaria a ID do dispositivo no esquema anterior:
1. O aplicativo tentará localizar a ID gerada.
1. Se a ID gerada for encontrada, o aplicativo usará a ID gerada ao baixar as licenças pré-geradas. O aplicativo enviará as licenças para o cliente DRM Primetime para consumo usando o método `DRMManager.storeVoucher()`. .
1. Se a ID gerada não for encontrada, o aplicativo passará pelo procedimento de registro do dispositivo.

## Redefinição de fábrica DRM {#drm-factory-reset}

Quando o usuário do dispositivo chamar a opção de redefinição de fábrica de DRM, o certificado do dispositivo será removido. Para continuar reproduzindo o conteúdo protegido, o aplicativo deve passar pelo procedimento de registro do dispositivo novamente. Se o aplicativo enviar uma licença pré-gerada desatualizada, o cliente DRM Primetime a rejeitará, pois a licença foi criptografada para uma ID de dispositivo mais antiga.

* API do Flash: [DRMManager.resetDRMVouchers()](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html#resetDRMVouchers()) - (Só pode ser chamado em resposta a determinados códigos de erro de DRM não recuperáveis.)
* API do iOS: [DRMManager resetDRM](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a0dd6c9662428583196e0419d3ea69446)
* API do Android: [DRMManager.resetDRM()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#resetDRM(com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))