---
title: Definição de regras baseadas em tempo
description: Definição de regras baseadas em tempo
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# Definindo regras baseadas em tempo {#defining-time-based-rules}

O Adobe Access utiliza a &quot;aplicação flexível&quot; de restrições de licença baseadas em tempo. Se um direito de tempo expirar durante a reprodução de um vídeo, o comportamento padrão do Acesso ao Adobe é não restringir a reprodução até a próxima vez que o fluxo de vídeo for recriado (chamando `Netstream.stop()` e `Netstream.play()`).

Embora a aplicação flexível seja o comportamento padrão, você também pode ativar a aplicação rígida executando uma das seguintes tarefas:

* Solicite ao seu reprodutor de vídeo que pesquise periodicamente a licença para verificar se nenhuma das restrições de tempo expirou. Isso pode ser feito ao chamar `DRMManager.loadVoucher(LOCAL_ONLY).`Um código de erro indica que a licença armazenada localmente não é mais válida.
* Sempre que o usuário clicar no botão Pausar, você poderá gravar o carimbo de data e hora do vídeo atual e chamar `Netstream.stop().`Quando o usuário clicar no botão Reproduzir , você poderá procurar no local gravado e, em seguida, chamar `Netstream.play()`.

## Data de início {#start-date}

Especifica a data após a qual uma licença é válida.

Exemplo de caso de uso: Use uma data absoluta para emitir licenças de conteúdo antes da data de disponibilidade de um ativo ou para aplicar um período de &quot;embargo&quot;.

## Data final {#end-date}

Especifica a data após a qual as licenças expiram.

Exemplo de caso de uso: Use uma data de expiração absoluta para refletir o fim dos direitos de distribuição.

## Data final relativa {#relative-end-date}

Especifica a data de expiração da licença, expressa em relação à data do empacotamento.

Exemplo de caso de uso: Em um processo de empacotamento automatizado, use uma única política com essa opção para uma série de vídeos para definir a data de expiração como 30 dias em relação à data do empacotamento.

## Duração do armazenamento em cache da licença {#license-caching-duration}

Especifica a duração em que uma licença pode ser armazenada em cache no disco no License Store local do cliente sem exigir reaquisição do servidor de licença. Como alternativa, você pode especificar uma data/hora absoluta após a qual uma licença não pode mais ser armazenada em cache.

Depois que a data de expiração do cache tiver passado, a licença não será mais válida e o cliente deverá solicitar uma nova licença do servidor de licenças.

Exemplo de caso de uso: Use a duração do armazenamento em cache de licenças para especificar um período fixo válido para uma licença específica, como em um caso de uso de aluguel. É possível especificar um aluguel de 30 dias (com armazenamento em cache de licenças) para indicar a duração total da licença dentro da qual consumir o conteúdo.

## Janela de reprodução {#playback-window}

Especifica a duração em que uma licença é válida após a primeira vez em que é usada para reproduzir conteúdo protegido.

Exemplo de caso de uso: Alguns modelos de negócios permitem um período de aluguel de 30 dias, mas, uma vez iniciada a reprodução, ele deve ser concluído em 48 horas. Essa longevidade de 48 horas da licença é definida como a janela de reprodução.

## Requisitos para sincronização {#requirements-for-synchronization}

Especifica a frequência na qual o cliente sincronizará seu estado com o servidor. Se o cliente tiver recebido uma licença fora de banda (sem que um servidor de licenças seja contatado), as regras de uso poderão especificar que o cliente deve enviar mensagens de sincronização para o servidor a fim de sincronizar a hora segura do cliente e relatar o estado do cliente ao servidor.

O comportamento de sincronização é definido usando os seguintes parâmetros:

* Intervalo de Início — Especifica o tempo de espera após a última sincronização bem-sucedida para iniciar outra solicitação de sincronização.
* Intervalo de Parada Rígida — (Opcional). Não permitir a reprodução se uma sincronização bem-sucedida não tiver ocorrido no período especificado.
* Forçar Probabilidade de Sincronização — (Opcional). Probabilidade com a qual o cliente deve enviar uma mensagem de sincronização antes do próximo intervalo de início.

>[!NOTE]
>
>Essa regra de uso é compatível com os clientes do Adobe Access versão 3.0 e superior. O comportamento em clientes mais antigos depende da versão mínima do cliente compatível com o servidor de licenças. Consulte [Versão mínima do cliente](../../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).