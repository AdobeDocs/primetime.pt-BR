---
title: Visão geral das regras baseadas em tempo
description: Visão geral das regras baseadas em tempo
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Regras baseadas em tempo {#time-based-rules}

O Primetime DRM usa &quot;aplicação flexível&quot; de restrições de licença baseadas em tempo. Se um direito de tempo expirar durante a reprodução de um vídeo, o comportamento padrão do DRM do Primetime é não restringir a reprodução até a próxima vez que o fluxo de vídeo for recriado (chamando `Netstream.stop()` e `Netstream.play()`).

Embora a aplicação flexível seja o comportamento padrão, você também pode ativar a aplicação forçada executando uma das seguintes tarefas:

* Peça ao reprodutor de vídeo que consulte periodicamente a licença para verificar se nenhuma das restrições de tempo expirou. Isso pode ser feito chamando `DRMManager.loadVoucher(LOCAL_ONLY).` Um código de erro indica que a licença armazenada localmente não é mais válida.
* Sempre que o usuário clicar em **[!UICONTROL Pause]**, você poderá gravar o carimbo de data e hora atual do vídeo e chamar `Netstream.stop()`. Quando o usuário clica no botão Reproduzir, é possível buscar no local gravado e chamar `Netstream.play()`.