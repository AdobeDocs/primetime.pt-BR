---
title: Notas de versão da autenticação Android 3.7.3
description: Notas de versão da autenticação Android 3.7.3
source-git-commit: fbc0e710d205532d268213ca0bdc81449e9c9835
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Notas de versão da autenticação Android 3.7.3 {#android-sdk-370-release-notes}

>[!NOTE]
>
>O conteúdo desta página é fornecido apenas para fins informativos. O uso desta API requer uma licença atual do Adobe. Não é permitida nenhuma utilização não autorizada.

Esta página descreve novos recursos, alterações e problemas conhecidos com esta versão:

## Número da Build {#build-no-android-sdk-373}

Autenticação do Adobe Primetime: Android 3.7.3

Data de lançamento: 19/09/2023



## Visão geral da versão {#overview-android-sdk-370}

* Alterações para suportar Android 14 e aplicativos direcionados ao nível 34 da API
   * Adicionar sinalizador exigido por [Receptores de transmissões registradas no tempo de execução do Android 14](https://developer.android.com/about/versions/14/behavior-changes-14#runtime-receivers-exported).
* Corrigir ChromeCustomTabs que não abrem para logon MVPD na API do emulador 32+
   * Observação: uma solução alternativa para esse problema no SDK &lt;3.7.3 é abrir o aplicativo Chrome no emulador e concluir a configuração antes de tentar fazer logon no MVPD


## Lançar pacote {#rel=pkg-android373}

Você pode baixar o Android SDK v3.7.3 em [aqui](https://tve.zendesk.com/hc/en-us/articles/204963219-Android-Native-AccessEnabler-Library).

Antes de atualizar para esta versão, verifique esta nota técnica.