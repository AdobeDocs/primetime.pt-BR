---
title: Ativar o Acessar o logon único (SSO) do Android SDK em aplicativos Android 10
description: Ativar o Acessar o logon único (SSO) do Android SDK em aplicativos Android 10
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---



# Ativar o Acessar o logon único (SSO) do Android SDK em aplicativos Android 10 {#access-enabler-android-sdk-single-sign-on-sso-on-android-10-apps}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins de informação. O uso dessa API requer uma licença atual do Adobe. Não é permitida a utilização não autorizada.

## Visão geral

O Logon único (SSO) entre aplicativos com autenticação da Adobe Primetime está disponível em dispositivos que usam o sistema operacional Android por meio do SDK do Android com Ativador de Acesso. Para oferecer o Logon único (SSO) em dispositivos Android, o SDK do Android do Access Enabler versão 3.2.1 (mais recente) e as versões anteriores usam um arquivo de banco de dados compartilhado salvo em uma implementação de armazenamento Android, acessível por todos os aplicativos com autenticação Adobe Primetime.

No entanto, a Google na versão mais recente do Android 10 produziu algumas alterações &quot;para dar aos usuários mais controle sobre seus arquivos e para limitar a desorganização de arquivos, os aplicativos direcionados ao Android 10 (nível de API 29) e superior recebem acesso com escopo em um dispositivo de armazenamento externo ou armazenamento com escopo, por padrão. Esses aplicativos podem ver somente o diretório específico do aplicativo `\[...\]`&quot;. Mais detalhes relacionados a essas alterações de armazenamento do Android 10 são apresentados em [Documentação de armazenamento de dados e arquivos para Android](https://developer.android.com/training/data-storage/files/external-scoped).

Como resultado dessas alterações, o Single Sign-On (SSO) oferecido pela versão do Access Enabler Android **SDK 3.2.1 (mais recente)** e versões anteriores podem ser afetadas em dispositivos Android 10, conforme explicado na próxima seção.

Consulte [Visão geral do Roku SSO](/help/authentication/roku-sso-overview.md).

## Comportamento

Dependendo do **nível do SDK do target** ou a utilização de **android:requestLegacyExternalStorage** atributo manifest o Single Sign-On (SSO) oferecido pelo Access Enabler Android versão 3.2.1 SDK (mais recente) e as versões anteriores se comportarão da seguinte maneira:

- Destinos do seu aplicativo **Android 9 (nível de API 28)** ou inferior **-\>** Logon único (SSO) **funcionará**
- Destinos do seu aplicativo **Android 10** **(nível 29 da API)** e faz **set** o valor de **requestLegacyExternalStorage para verdadeiro** no arquivo manifest do aplicativo **-\>** Logon único (SSO) **funcionará**
- Destinos do seu aplicativo **Android 10** **(nível 29 da API)** e faz **não definido** o valor de **requestLegacyExternalStorage para verdadeiro** no arquivo manifest do aplicativo **-\>** Logon único (SSO) **não funcionará**


>[!TIP]
>
> Antes de o SDK do Android Enabler de Acesso à autenticação da Adobe Primetime ser totalmente compatível com o armazenamento com escopo, você pode recusar temporariamente com base no nível do SDK de destino do seu aplicativo ou no atributo de manifesto requestLegacyExternalStorage , conforme explicado em público [Documentação do Android](https://developer.android.com/training/data-storage/files/external-scoped#opt-out-of-scoped-storage).

