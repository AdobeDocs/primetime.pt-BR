---
seo-title: Regras baseadas em tempo
title: Regras baseadas em tempo
uuid: 19a6ee7e-9580-48bb-a3a6-ff2cedcc796a
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Regras baseadas em tempo {#time-based-rules}

O Primetime DRM usa a &quot;aplicação flexível&quot; das restrições de licença baseadas em tempo. Se um direito de tempo expirar durante a reprodução de um vídeo, o comportamento padrão do DRM Primetime é não restringir a reprodução até a próxima vez que o fluxo de vídeo for recriado (chamando `Netstream.stop()` e `Netstream.play()`).

Embora a aplicação flexível seja o comportamento padrão, também é possível ativar a aplicação forçada executando uma das seguintes tarefas:

* Solicite ao seu reprodutor de vídeo que pesquise periodicamente a licença para verificar se nenhuma das restrições de tempo expirou. Isso pode ser feito chamando `DRMManager.loadVoucher(LOCAL_ONLY).` Um código de erro indica que a licença armazenada localmente não é mais válida.
* Sempre que o usuário clica **[!UICONTROL Pause]**, você pode gravar o carimbo de data e hora do vídeo atual e depois chamar `Netstream.stop()`. Quando o usuário clica no botão Reproduzir, você pode procurar no local gravado e depois chamar `Netstream.play()`.

## Data de início {#start-date}

A data de início especifica a data após a qual uma licença é válida.

Exemplo de caso de uso: Use uma data absoluta para emitir licenças de conteúdo antes da data de disponibilidade de um ativo ou para aplicar um período de &quot;embargo&quot;.

## Data de término {#end-date}

A data de término especifica a data após a qual uma licença expira.

Exemplo de caso de uso: Use uma data de expiração absoluta para refletir o fim dos direitos de distribuição.

## Data final relativa {#relative-end-date}

A data de término relativa especifica a data de expiração da licença, que é expressa em relação à data da embalagem, não em relação à data em que a licença foi emitida.

Exemplo de caso de uso: Em um processo de empacotamento automatizado, use uma única política de DRM Primetime com essa opção para uma série de vídeos, para definir a data de expiração como 30 dias em relação à data de empacotamento.

## Duração do armazenamento em cache da licença{#license-caching-duration}

A duração do armazenamento em cache de licenças especifica por quanto tempo uma licença pode ser armazenada em cache no disco do Repositório de Licenças local do cliente sem a necessidade de reaquisição do servidor de licenças. Como alternativa, você pode especificar uma data e hora absolutas após as quais uma licença não pode mais ser armazenada em cache.

Depois que a data de expiração do cache for ultrapassada, a licença não será mais válida e o cliente deverá solicitar uma nova licença do servidor de licenças.

Exemplo de caso de uso: Use a duração do armazenamento em cache da licença para especificar um período fixo válido para uma licença específica, como em um caso de uso de aluguel. Você pode especificar um aluguel de 30 dias (com armazenamento em cache de licenças) para indicar a duração total da licença para consumir o conteúdo.

## Janela de reprodução {#playback-window}

A janela de reprodução especifica a duração de validade de uma licença após a primeira vez que é usada para reproduzir conteúdo protegido.

Exemplo de caso de uso: Alguns modelos de negócios permitem um período de aluguel de 30 dias, mas, uma vez iniciada a reprodução, a reprodução precisa ser concluída em 48 horas. Nesse caso, a duração de 48 horas da licença é a janela de reprodução.

**Da versão 5.3 em diante** - A janela de reprodução também suporta a opção de ativar ou desativar a Parada sólida, que indica se o contexto de descriptografia para a reprodução deve parar na expiração da janela de reprodução (ativada) ou continuar apesar da expiração (desativada).

>[!NOTE]
>
>A opção hard stop não funciona corretamente com a Janela de reprodução se usada em conjunto com ela (a janela de reprodução não será respeitada). Reproduzir conteúdo com a janela Reprodução sem parada segura respeita a restrição da janela de reprodução.