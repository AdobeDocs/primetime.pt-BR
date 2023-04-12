---
title: Autenticação Adobe Primetime e o novo modelo de permissões "Marshmallow" do Android 6
description: Autenticação Adobe Primetime e o novo modelo de permissões "Marshmallow" do Android 6
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---



# Autenticação Adobe Primetime e o novo modelo de permissões &quot;Marshmallow&quot; do Android 6 {#adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

</br>

A nova versão do Android 6 Marshmallow apresenta algumas atualizações ao modelo de permissões, o que pode afetar o comportamento dos aplicativos que usam o SDK de autenticação da Adobe Primetime versão 1.8 e posterior. 

Como um novo recurso, o novo sistema operacional Android oferece [controle granular sobre as permissões que os aplicativos exigem no momento da instalação e no tempo de execução](https://developer.android.com/about/versions/marshmallow/android-6.0-changes.html).

>[!IMPORTANT]
>
>As alterações descritas abaixo irão **afeta apenas aplicativos desenvolvidos especificamente para Android 6.0** (targetSdkVersion=23). Eles não afetam os aplicativos mais antigos já instalados no dispositivo do usuário ao atualizar para o Android 6.0. 


Especificamente, para aplicativos desenvolvidos no Android Studio usando [Nível 23 da API](http://developer.android.com/sdk/api_diff/23/changes.html) e que usam o SDK de autenticação da Adobe Primetime, o desenvolvedor precisará gravar o código personalizado (consulte o trecho de código abaixo) [para acionar a caixa de diálogo permitir/negar permissões](https://developer.android.com/training/permissions/requesting.html). 

A seguir, o trecho de código usado para solicitar acesso de gravação ao armazenamento externo do dispositivo:

```java
// Here, thisActivity is the current activity
if (ContextCompat.checkSelfPermission(thisActivity,
                Manifest.permission.WRITE_EXTERNAL_STORAGE)
        != PackageManager.WRITE_EXTERNAL_STORAGE) {

    // Should we show an explanation?
    if (ActivityCompat.shouldShowRequestPermissionRationale(thisActivity,
            Manifest.permission.WRITE_EXTERNAL_STORAGE)) {

        // Show an expanation to the user *asynchronously* -- don't block
        // this thread waiting for the user's response! After the user
        // sees the explanation, try again to request the permission.

    } else {

        // No explanation needed, we can request the permission.

        ActivityCompat.requestPermissions(thisActivity,
                new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
                MY_PERMISSIONS_REQUEST_WRITE_EXTERNAL_STORAGE);

        // MY_PERMISSIONS_REQUEST_WRITE_EXTERNAL_STORAGE is an
        // app-defined int constant. The callback method gets the
        // result of the request.
    }
}
```




**Da perspectiva dos usuários**, após a instalação, os usuários são recebidos por uma janela solicitando que confirmem permissões de leitura/gravação para arquivos (consulte a figura 2 abaixo). Isso leva a um dos dois resultados a seguir:

1. Se o usuário **confirm** com as permissões, o fluxo de autenticação regular será mantido e os tokens serão armazenados no armazenamento global. Os usuários permanecerão autenticados no aplicativo e em todos os aplicativos usando a autenticação da Adobe Primetime enquanto os tokens forem válidos.
1. Se o usuário **nega** as permissões, as ações de gravação no armazenamento falharão e os usuários só serão autenticados até que saiam do aplicativo. Observe que alguns aplicativos são reinicializados ao alternar entre primeiro e segundo plano, para que os usuários sejam desconectados ao executar essa ação. Os tokens NÃO são armazenados e os usuários precisarão se autenticar sempre que usarem o aplicativo. 


>[!TIP]
>
>Um recurso que introduz a resiliência de armazenamento está atualmente em desenvolvimento para o SDK de autenticação da Adobe Primetime 1.9. O novo SDK é direcionado para **lançamento na última semana de outubro**. O aplicativo falará para escrever no armazenamento da sandbox do aplicativo sempre que o armazenamento geral não puder ser usado. Isso abrange o caso em que, para aplicativos desenvolvidos no nível 23 da API, os usuários NÃO aceitam permissões de leitura/gravação no armazenamento global. Os tokens são armazenados individualmente por aplicativo, o que significa que o Logon único entre aplicativos que usam a autenticação da Adobe Primetime será desativado.


![](assets/android-permissions-request.png)

*Figura: A caixa de diálogo solicitação de permissão para aplicativos da API de direcionamento gravado nível 23*

>[!IMPORTANT]
>
> Adobe informa **seus parceiros para desenvolver aplicativos usando o nível 22 da API (targetSdkVersion=22) ou posterior, a fim de garantir a melhor experiência possível do usuário no processo de autenticação**. 