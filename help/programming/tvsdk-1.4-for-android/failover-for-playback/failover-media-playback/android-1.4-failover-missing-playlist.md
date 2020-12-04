---
description: Quando uma lista de reprodução inteira estiver ausente, por exemplo, quando o arquivo M3U8 especificado em um arquivo manifest de nível superior não for baixado, o TVSDK tentará recuperar. Se ele não conseguir recuperar, seu aplicativo determinará a próxima etapa.
seo-description: Quando uma lista de reprodução inteira estiver ausente, por exemplo, quando o arquivo M3U8 especificado em um arquivo manifest de nível superior não for baixado, o TVSDK tentará recuperar. Se ele não conseguir recuperar, seu aplicativo determinará a próxima etapa.
seo-title: Failover de lista de reprodução ausente
title: Failover de lista de reprodução ausente
uuid: 91a537f3-3e69-4669-8f84-0292c19ac209
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# Failover da lista de reprodução ausente{#missing-playlist-failover}

Quando uma lista de reprodução inteira estiver ausente, por exemplo, quando o arquivo M3U8 especificado em um arquivo manifest de nível superior não for baixado, o TVSDK tentará recuperar. Se ele não conseguir recuperar, seu aplicativo determinará a próxima etapa.

Se a lista de reprodução associada à taxa de bits de resolução média estiver ausente, o TVSDK pesquisará uma lista de reprodução variante na mesma resolução. Se encontrar a mesma resolução, ele start o download da lista de reprodução variante e dos segmentos da posição correspondente. Se o TVSDK não encontrar a mesma lista de reprodução de resolução, ele tentará percorrer outras listas de reprodução de taxa de bits e suas variantes. Uma taxa de bits imediatamente menor é a primeira escolha, depois sua variante e assim por diante. Se todas as listas de reprodução de taxa de bits inferior e suas variantes estiverem esgotadas na tentativa de encontrar uma lista de reprodução válida, o TVSDK irá para a taxa de bits superior e contará a partir daí. Se não for possível encontrar uma lista de reprodução válida, o processo falhará e o player será movido para o estado ERROR.

Seu aplicativo pode determinar como lidar com essa situação. Por exemplo, talvez você queira fechar a atividade do player e direcionar o usuário para a atividade do catálogo. O evento de interesse é o evento `STATE_CHANGED` e o retorno de chamada correspondente é o método `onStateChanged`. Este é um código que monitora se o player altera seu estado interno para ERRO:

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

Para obter mais informações, consulte o arquivo [!DNL PlayerFragment.java] no SDK:

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

Se setNetworkDownVerificationUrl não estiver definido, o TVSDK usará o url MainManifest por padrão para determinar se a rede está inativa.
