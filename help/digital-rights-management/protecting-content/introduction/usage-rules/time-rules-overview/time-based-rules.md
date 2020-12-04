---
seo-title: Visão geral das regras baseadas em tempo
title: Visão geral das regras baseadas em tempo
uuid: 10b7766e-3b1a-4d8a-ba15-46976aa0847d
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Regras baseadas em tempo {#time-based-rules}

O Primetime DRM usa a &quot;aplicação flexível&quot; das restrições de licença baseadas em tempo. Se um direito de tempo expirar durante a reprodução de um vídeo, o comportamento padrão do DRM Primetime é não restringir a reprodução até a próxima vez que o fluxo de vídeo for recriado (chamando `Netstream.stop()` e `Netstream.play()`).

Embora a aplicação flexível seja o comportamento padrão, também é possível ativar a aplicação forçada executando uma das seguintes tarefas:

* Solicite ao seu reprodutor de vídeo que pesquise periodicamente a licença para verificar se nenhuma das restrições de tempo expirou. Isso pode ser feito chamando `DRMManager.loadVoucher(LOCAL_ONLY).` Um código de erro indica que a licença armazenada localmente não é mais válida.
* Sempre que o usuário clicar em **[!UICONTROL Pause]**, você poderá gravar o carimbo de data e hora do vídeo atual e depois chamar `Netstream.stop()`. Quando o usuário clica no botão Reproduzir, você pode procurar no local gravado e depois chamar `Netstream.play()`.