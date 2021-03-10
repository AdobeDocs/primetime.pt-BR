---
title: Visão geral das regras baseadas em tempo
description: Visão geral das regras baseadas em tempo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Regras baseadas em tempo {#time-based-rules}

O DRM do Primetime usa a &quot;aplicação flexível&quot; de restrições de licença baseadas em tempo. Se um direito de tempo expirar durante a reprodução de um vídeo, o comportamento padrão do DRM do Primetime é não restringir a reprodução até a próxima vez que o fluxo de vídeo for recriado (chamando `Netstream.stop()` e `Netstream.play()`).

Embora a aplicação flexível seja o comportamento padrão, você também pode ativar a aplicação rígida executando uma das seguintes tarefas:

* Solicite ao seu reprodutor de vídeo que pesquise periodicamente a licença para verificar se nenhuma das restrições de tempo expirou. Isso pode ser feito ao chamar `DRMManager.loadVoucher(LOCAL_ONLY).` Um código de erro indica que a licença armazenada localmente não é mais válida.
* Sempre que o usuário clicar em **[!UICONTROL Pause]**, você poderá gravar o carimbo de data e hora do vídeo atual e, em seguida, chamar `Netstream.stop()`. Quando o usuário clica no botão Reproduzir , você pode procurar no local gravado e, em seguida, chamar `Netstream.play()`.