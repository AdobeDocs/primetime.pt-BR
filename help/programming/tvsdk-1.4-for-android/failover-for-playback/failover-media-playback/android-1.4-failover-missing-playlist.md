---
description: Quando uma lista de reprodução inteira está ausente, por exemplo, quando o arquivo M3U8 especificado em um arquivo de manifesto de nível superior não é baixado, o TVSDK tenta se recuperar. Se não for possível recuperar, o aplicativo determinará a próxima etapa.
title: Failover de lista de reprodução ausente
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---


# Failover de lista de reprodução ausente{#missing-playlist-failover}

Quando uma lista de reprodução inteira está ausente, por exemplo, quando o arquivo M3U8 especificado em um arquivo de manifesto de nível superior não é baixado, o TVSDK tenta se recuperar. Se não for possível recuperar, o aplicativo determinará a próxima etapa.

Se a lista de reprodução associada à taxa de bits de resolução média estiver ausente, o TVSDK pesquisará uma lista de reprodução de variante na mesma resolução. Se encontrar a mesma resolução, ele começará a baixar a lista de reprodução da variante e os segmentos da posição correspondente. Se o TVSDK não encontrar a mesma lista de reprodução de resolução, ele tentará alternar entre outras listas de reprodução de taxa de bits e suas variantes. Uma taxa de bits imediatamente menor é a primeira escolha, depois sua variante e assim por diante. Se todas as listas de reprodução de taxa de bits inferior e suas variantes estiverem esgotadas na tentativa de encontrar uma lista de reprodução válida, o TVSDK irá para a taxa de bits superior e contará a partir daí. Se não for possível localizar uma lista de reprodução válida, o processo falhará e o reprodutor será movido para o estado ERROR.

Seu aplicativo pode determinar como lidar com essa situação. Por exemplo, talvez você queira fechar a atividade do reprodutor e direcionar o usuário para a atividade de catálogo. O evento de interesse é o evento `STATE_CHANGED` e o retorno de chamada correspondente é o método `onStateChanged`. Este é um código que monitora se o reprodutor altera seu estado interno para ERRO:

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

Para obter mais informações, consulte o arquivo [!DNL PlayerFragment.java] em seu SDK:

```
[…]/samples/PrimetimeReference/src/PrimetimeReference/src/com/adobe/primetime/reference/ui/player/
```

Se a rede do lado do cliente estiver inativa, você pode usar esse código para verificar.

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

A API fornecerá o url usado para verificar se a rede do lado do cliente está inativa. Esse deve ser um url válido, que retorna o código de resposta http 200 em solicitações http.

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

Se setNetworkDownCheckUrl não estiver definido, o TVSDK usa o url MainManifest por padrão para descobrir se a rede está inativa.
