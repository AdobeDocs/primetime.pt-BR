---
description: Problemas comuns durante o teste geralmente envolvem autenticadores do ExpressPlay, protocolos de transporte e parâmetros de solicitação de serviço necessários.
title: Solução de problemas do início rápido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# Solução de problemas de início rápido{#troubleshooting-your-quick-start}

Problemas comuns durante o teste geralmente envolvem autenticadores do ExpressPlay, protocolos de transporte e parâmetros de solicitação de serviço necessários.

Se as solicitações [!DNL curl] para o ExpressPlay para geração de token falharem, o corpo da resposta conterá uma mensagem de erro que explica o motivo da falha.

Se a geração de token for bem-sucedida, mas o conteúdo ainda não for reproduzido, verifique os registros de resgate do token ExpressPlay em busca de erros como &quot;Token expirado&quot;.

Se a geração do token foi bem-sucedida e o resgate não teve erro, mas o vídeo ainda não é reproduzido, verifique se o CEK corresponde ao conteúdo e se o formato do conteúdo corresponde aos recursos do dispositivo de destino.

Além disso:

* Verifique se você está usando o Autenticador de cliente correto em suas solicitações de serviço. É fácil usar acidentalmente o autenticador de produção quando você quis usar o autenticador de teste. Além disso, verifique se você está usando o *autenticador*. Por exemplo, durante os testes, você pode pegar o comando `curl` de outra pessoa e esquecer de trocar o autenticador pelo deles.

* Verifique se você está usando o protocolo de transporte adequado em suas solicitações ou em seus manifestos ( `https://` versus `https://`, ou no caso do FairPlay, `skd://` versus `https://` versus `https://`.

* Certifique-se de incluir todos os parâmetros de consulta necessários para a solução de DRM com a qual você está trabalhando. É fácil confundir o PlayReady com o Widevine, por exemplo, porque ambos estão trabalhando com DASH, mas os parâmetros de solicitação necessários e as configurações de empacotamento são diferentes.
* Confirme se a conta do ExpressPlay tem créditos de token suficientes e se não está esgotada.
* Confirme se o triplet de dados de DRM que estão sendo enviados para o TVSDK está correto: Token ExpressPlay, URL do servidor de licenças e tipo de DRM.
* Confirme se todos os seus componentes estão assumindo qual ambiente ExpressPlay está em uso, pois há dois ambientes: Teste e Produção.
* Lembre-se de que navegadores diferentes normalmente suportam apenas um DRM para conteúdo DASH.
* A partir do TVSDK 2.4, somente o perfil de pacote DASH-LIVE é compatível. (O suporte DASH-OnDemand está no roteiro.)
* O suporte para AndroidTV PlayReady é intermitente devido às limitações do fabricante do dispositivo. Para dar exemplos,

   * o dispositivo Razer Forge tem problemas com o conteúdo PlayReady
   * O Amazon FireTV não pode consumir conteúdo DASH que tenha a faixa de áudio criptografada

* A partir do TVSDK 2.4, somente os dispositivos AndroidTV normalmente suportam DRMs PlayReady e Widevine. Todos os outros dispositivos Android normalmente são compatíveis apenas com a Widevine.
* A partir do TVSDK 2.4, o Android TVSDK exige atualmente que a caixa PSSH esteja no manifesto .mpd . Isso é contrário ao padrão DASH, que especifica que a caixa PSSH pode estar em qualquer lugar, como no próprio conteúdo, e não apenas no .mpd.

