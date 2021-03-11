---
title: Regras baseadas em tempo
description: Regras baseadas em tempo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---


# Regras baseadas em tempo {#time-based-rules}

O DRM do Primetime usa a &quot;aplicação flexível&quot; de restrições de licença baseadas em tempo. Se um direito de tempo expirar durante a reprodução de um vídeo, o comportamento padrão do DRM do Primetime é não restringir a reprodução até a próxima vez que o fluxo de vídeo for recriado (chamando `Netstream.stop()` e `Netstream.play()`).

Embora a aplicação flexível seja o comportamento padrão, você também pode ativar a aplicação rígida executando uma das seguintes tarefas:

* Solicite ao seu reprodutor de vídeo que pesquise periodicamente a licença para verificar se nenhuma das restrições de tempo expirou. Isso pode ser feito ao chamar `DRMManager.loadVoucher(LOCAL_ONLY).` Um código de erro indica que a licença armazenada localmente não é mais válida.
* Sempre que o usuário clicar em **[!UICONTROL Pause]**, você poderá gravar o carimbo de data e hora do vídeo atual e, em seguida, chamar `Netstream.stop()`. Quando o usuário clica no botão Reproduzir , você pode procurar no local gravado e, em seguida, chamar `Netstream.play()`.

## Data de início {#start-date}

A data de início especifica a data após a qual uma licença é válida.

Exemplo de caso de uso: Use uma data absoluta para emitir licenças de conteúdo antes da data de disponibilidade de um ativo ou para aplicar um período de &quot;embargo&quot;.

## Data final {#end-date}

A data final especifica a data após a qual uma licença expira.

Exemplo de caso de uso: Use uma data de expiração absoluta para refletir o fim dos direitos de distribuição.

## Data final relativa {#relative-end-date}

A data final relativa especifica a data de expiração da licença, que é expressa em relação à data da embalagem, não em relação à data em que a licença foi emitida.

Exemplo de caso de uso: Em um processo de empacotamento automatizado, use uma única política de DRM do Primetime com essa opção para uma série de vídeos, para definir a data de expiração como 30 dias em relação à data do empacotamento.

## Duração do armazenamento em cache de licenças{#license-caching-duration}

A duração do armazenamento em cache de licenças especifica por quanto tempo uma licença pode ser armazenada em cache no disco no License Store local do cliente sem exigir reaquisição do servidor de licenças. Como alternativa, você pode especificar uma data e hora absolutas após as quais uma licença não pode mais ser armazenada em cache.

Depois que a data de expiração do cache tiver passado, a licença não será mais válida e o cliente deverá solicitar uma nova licença do servidor de licenças.

Exemplo de caso de uso: Use a duração do armazenamento em cache de licenças para especificar um período fixo válido para uma licença específica, como em um caso de uso de aluguel. Você pode especificar um aluguel de 30 dias (com armazenamento em cache de licenças) para indicar a duração total da licença dentro da qual consumir o conteúdo.

## Janela de reprodução {#playback-window}

A janela de reprodução especifica a duração em que uma licença é válida após a primeira vez em que é usada para reproduzir conteúdo protegido.

Exemplo de caso de uso: Alguns modelos de negócios permitem um período de aluguel de 30 dias, mas, uma vez iniciada a reprodução, a reprodução deve ser concluída em 48 horas. Nesse caso, a duração de 48 horas da licença é a janela de reprodução.

**A partir da versão 5.3**  - A janela de reprodução também oferece suporte à opção de ativar ou desativar a Parada forçada, indicando se o contexto de descriptografia para a reprodução deve parar na expiração da janela de reprodução (ativada) ou continuar apesar da expiração (desativada).

>[!NOTE]
>
>A opção de interrupção permanente não funciona corretamente com a Janela de reprodução, se usada em conjunto com ela (a Janela de reprodução não será respeitada). Reproduzir o conteúdo com a janela Reprodução sem parada segura respeita a restrição da janela de reprodução.