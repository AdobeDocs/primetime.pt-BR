---
seo-title: Definição de regras baseadas em tempo
title: Definição de regras baseadas em tempo
uuid: 17c69869-ac81-4561-9fb6-b1c5c9c4006d
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---


# Definição de regras baseadas em tempo {#defining-time-based-rules}

O Adobe Access usa a &quot;aplicação flexível&quot; das restrições de licença baseadas em tempo. Se um direito de tempo expirar durante a reprodução de um vídeo, o comportamento padrão do Acesso a Adobe é não restringir a reprodução até a próxima vez que o fluxo de vídeo for recriado (chamando `Netstream.stop()` e `Netstream.play()`).

Embora a aplicação flexível seja o comportamento padrão, também é possível ativar a aplicação forçada executando uma das seguintes tarefas:

* Solicite ao seu reprodutor de vídeo que pesquise periodicamente a licença para verificar se nenhuma das restrições de tempo expirou. Isso pode ser feito chamando `DRMManager.loadVoucher(LOCAL_ONLY).`Um código de erro indica que a licença armazenada localmente não é mais válida.
* Sempre que o usuário clicar no botão Pausar, você poderá gravar o carimbo de data e hora do vídeo atual e, em seguida, chamar `Netstream.stop().`Quando o usuário clicar no botão Reproduzir, você poderá procurar o local gravado e, em seguida, chamar `Netstream.play()`.

## data do start {#start-date}

Especifica a data após a qual uma licença é válida.

Exemplo de caso de uso: Use uma data absoluta para emitir licenças de conteúdo antes da data de disponibilidade de um ativo ou para aplicar um período de &quot;embargo&quot;.

## Data de término {#end-date}

Especifica a data após a qual as licenças expiram.

Exemplo de caso de uso: Use uma data de expiração absoluta para refletir o fim dos direitos de distribuição.

## Data final relativa {#relative-end-date}

Especifica a data de expiração da licença, expressa em relação à data do empacotamento.

Exemplo de caso de uso: Em um processo de empacotamento automatizado, use uma única política com essa opção para uma série de vídeos para definir a data de expiração como 30 dias em relação à data do empacotamento.

## Duração do armazenamento em cache da licença {#license-caching-duration}

Especifica a duração em que uma licença pode ser armazenada em cache no armazenamento local de licença do cliente sem precisar de nova aquisição do servidor de licença. Como alternativa, você pode especificar uma data/hora absoluta após a qual uma licença não pode mais ser armazenada em cache.

Depois que a data de expiração do cache for ultrapassada, a licença não será mais válida e o cliente deverá solicitar uma nova licença do servidor de licenças.

Exemplo de caso de uso: Use a duração do armazenamento em cache da licença para especificar um período fixo válido para uma licença específica, como em um caso de uso de aluguel. É possível especificar um aluguel de 30 dias (com armazenamento em cache de licenças) para indicar a duração total da licença para consumir o conteúdo.

## Janela de reprodução {#playback-window}

Especifica a duração de validade de uma licença após a primeira vez que é usada para reproduzir conteúdo protegido.

Exemplo de caso de uso: Alguns modelos de negócios permitem um período de aluguel de 30 dias, mas, uma vez iniciada a reprodução, ela deve ser concluída em 48 horas. Essa longevidade de 48 horas da licença é definida como a janela de reprodução.

## Requisitos para sincronização {#requirements-for-synchronization}

Especifica a frequência na qual o cliente sincronizará seu estado com o servidor. Se o cliente tiver recebido uma licença fora de banda (sem que um servidor de licenças seja contatado), as regras de uso poderão especificar que o cliente deverá enviar mensagens de sincronização ao servidor para sincronizar o horário seguro do cliente e informar o estado do cliente ao servidor.

O comportamento de sincronização é definido usando os seguintes parâmetros:

* Intervalo de start — Especifica por quanto tempo esperar após a última sincronização bem-sucedida para start de outra solicitação de sincronização.
* Intervalo de Parada Rígida — (Opcional). Desative a reprodução se uma sincronização bem-sucedida não tiver ocorrido no período especificado.
* Forçar Sincronização Probabilidade — (Opcional). Probabilidade com a qual o cliente deve enviar uma mensagem de sincronização antes do próximo intervalo de start.

>[!NOTE]
>
>Esta regra de uso é suportada pelos clientes do Adobe Access versão 3.0 e superior. O comportamento de clientes mais antigos depende da versão mínima do cliente suportada pelo servidor de licenças. Consulte, Versão [](../../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md)mínima do cliente.