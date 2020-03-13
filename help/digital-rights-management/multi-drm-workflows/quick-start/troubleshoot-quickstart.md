---
description: Problemas comuns durante os testes geralmente envolvem autenticadores do ExpressPlay, protocolos de transporte e parâmetros de solicitação de serviço necessários.
seo-description: Problemas comuns durante os testes geralmente envolvem autenticadores do ExpressPlay, protocolos de transporte e parâmetros de solicitação de serviço necessários.
seo-title: Solução de problemas de inicialização rápida
title: Solução de problemas de inicialização rápida
uuid: 42256aa0-2efc-4602-aefc-3bab2dc58ec0
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Solução de problemas de inicialização rápida{#troubleshooting-your-quick-start}

Problemas comuns durante os testes geralmente envolvem autenticadores do ExpressPlay, protocolos de transporte e parâmetros de solicitação de serviço necessários.

Se suas [!DNL curl] solicitações ao ExpressPlay para geração de token falharem, o corpo da resposta conterá uma mensagem de erro que explica o motivo da falha.

Se a geração de token for bem-sucedida, mas o conteúdo ainda não for reproduzido, verifique se há erros nos registros de resgate de token do ExpressPlay, como &quot;Token expirado&quot;.

Se a geração de token tiver sido bem-sucedida e o resgate não tiver ocorrido, mas o vídeo ainda não for reproduzido, verifique se o CEK corresponde ao conteúdo e se o formato do conteúdo corresponde aos recursos do dispositivo de destino.

Além disso:

* Verifique se você está usando o Autenticador de cliente correto em suas solicitações de serviço. É fácil usar acidentalmente o autenticador de produção quando você pretendia usar o autenticador de teste. Além disso, verifique se você está usando *seu* autenticador. Por exemplo, durante os testes você pode pegar o comando de outra pessoa e esquecer de trocar o seu autenticador pelo `curl` deles.

* Verifique se você está usando o protocolo de transporte apropriado em suas solicitações ou em seus manifestos ( `https://` versus `https://`, ou no caso do FairPlay, `skd://` versus `https://` versus `https://`.

* Certifique-se de incluir todos os parâmetros de consulta necessários para a solução DRM com a qual você está trabalhando. É fácil se confundir entre PlayReady e Widevine, por exemplo, porque ambos estão trabalhando com DASH, mas os parâmetros de solicitação necessários e as configurações de empacotamento são diferentes.
* Confirme se sua conta ExpressPlay tem créditos de token suficientes e se não foi esgotada.
* Confirme se o triplo dos dados de DRM que estão sendo enviados para o TVSDK está correto: Token do ExpressPlay, URL do servidor de licenças e tipo de DRM.
* Confirme se todos os seus componentes estão assumindo que o ambiente ExpressPlay está sendo usado, pois há dois ambientes: Teste e Produção.
* Lembre-se de que navegadores diferentes geralmente suportam apenas um DRM para conteúdo DASH.
* A partir do TVSDK 2.4, somente o perfil de empacotamento DASH-LIVE é suportado. (O suporte DASH-OnDemand está no roteiro.)
* O suporte para AndroidTV PlayReady é intermitente devido às limitações do fabricante do dispositivo. Para dar exemplos,

   * o dispositivo Razer Forge tem problemas com o conteúdo PlayReady
   * O Amazon FireTV não pode consumir conteúdo DASH que tenha a faixa de áudio criptografada

* A partir do TVSDK 2.4, somente os dispositivos AndroidTV normalmente suportam DRMs PlayReady e Widevine. Todos os outros dispositivos Android normalmente suportam somente o Widevine.
* A partir do TVSDK 2.4, o Android TVSDK atualmente exige que a caixa PSSH esteja no manifesto .mpd. Isso é contrário ao padrão DASH, que especifica que a caixa PSSH pode estar em qualquer lugar, como no próprio conteúdo, e não apenas no .mpd.

