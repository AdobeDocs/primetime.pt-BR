---
description: Problemas comuns durante os testes geralmente envolvem os autenticadores ExpressPlay, protocolos de transporte e parâmetros de solicitação de serviço necessários.
title: Solução de problemas de início rápido
exl-id: d8908f9c-98f4-4100-a003-d3b990105dee
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# Solução de problemas de início rápido{#troubleshooting-your-quick-start}

Problemas comuns durante os testes geralmente envolvem os autenticadores ExpressPlay, protocolos de transporte e parâmetros de solicitação de serviço necessários.

Se o seu [!DNL curl] Se as solicitações do ExpressPlay para geração de token falharem, o corpo da resposta conterá uma mensagem de erro que explica o motivo da falha.

Se a geração do token for bem-sucedida, mas o conteúdo ainda não for reproduzido, verifique os logs de resgate do token ExpressPlay para ver se há erros como &quot;Token expirado&quot;.

Se a geração do token foi bem-sucedida e o resgate não teve erro, mas o vídeo ainda não é reproduzido, verifique se o CEK corresponde ao conteúdo e se o formato de conteúdo corresponde aos recursos do dispositivo de destino.

Além disso:

* Verifique se você está usando o Autenticador do cliente correto em suas solicitações de serviço. É fácil usar acidentalmente o autenticador de produção quando você pretende usar o autenticador de teste. Além disso, verifique se você está usando *seu* autenticador. Por exemplo, durante os testes você pode pegar o de outra pessoa emprestado `curl` e esqueça de trocar o autenticador pelo autenticador.

* Verifique se você está usando o protocolo de transporte adequado em suas solicitações ou manifestos ( `https://` versus `https://`ou, no caso do FairPlay, `skd://` versus `https://` versus `https://`.

* Certifique-se de incluir todos os parâmetros de consulta necessários para a solução de DRM com a qual você está trabalhando. É fácil confundir o PlayReady com o Widevine, por exemplo, porque ambos estão trabalhando com o DASH, mas os parâmetros de solicitação e as configurações de empacotamento necessários são diferentes.
* Confirme se sua conta ExpressPlay tem créditos de token suficientes e se não está esgotada.
* Confirme se o trio de dados DRM que está sendo enviado ao TVSDK está correto: token ExpressPlay, URL do servidor de licença e tipo DRM.
* Confirme se todos os seus componentes estão fazendo a mesma suposição sobre qual ambiente ExpressPlay está em uso, pois há dois ambientes: Teste e Produção.
* Esteja ciente de que navegadores diferentes normalmente suportam apenas um DRM para conteúdo DASH.
* A partir do TVSDK 2.4, somente o perfil de empacotamento DASH-LIVE é compatível. (O suporte DASH-OnDemand está no roteiro.)
* O suporte ao Android TV PlayReady é intermitente devido às limitações do fabricante do dispositivo. Para dar exemplos,

   * o dispositivo Razer Forge tem problemas com o conteúdo PlayReady
   * O Amazon FireTV não pode consumir conteúdo DASH com faixa de áudio criptografada

* A partir do TVSDK 2.4, apenas dispositivos Android TV normalmente suportam DRMs PlayReady e Widevine. Todos os outros dispositivos Android normalmente só são compatíveis com o Widevine.
* A partir do TVSDK 2.4, o Android TVSDK exige atualmente que a caixa PSSH esteja no manifesto .mpd. Isso é contrário ao padrão DASH, que especifica que a caixa PSSH pode estar em qualquer lugar, como no próprio conteúdo e não apenas em .mpd.
