---
title: Definição de regras baseadas em tempo
description: Definição de regras baseadas em tempo
copied-description: true
exl-id: ef72ee76-7d83-486d-86fe-df90c2aaca3a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Definição de regras baseadas em tempo {#defining-time-based-rules}

O Adobe Access usa &quot;aplicação suave&quot; de restrições de licença baseadas em tempo. Se um direito de tempo expirar durante a reprodução de um vídeo, o comportamento padrão do Acesso ao Adobe é não restringir a reprodução até a próxima vez que o fluxo de vídeo for recriado (chamando `Netstream.stop()` e `Netstream.play()`).

Embora a aplicação flexível seja o comportamento padrão, você também pode ativar a aplicação forçada executando uma das seguintes tarefas:

* Peça ao reprodutor de vídeo que consulte periodicamente a licença para verificar se nenhuma das restrições de tempo expirou. Isso pode ser feito chamando `DRMManager.loadVoucher(LOCAL_ONLY).`Um código de erro indica que a licença armazenada localmente não é mais válida.
* Sempre que o usuário clicar no botão Pausar, você poderá gravar o carimbo de data e hora atual do vídeo e chamar `Netstream.stop().`Quando o usuário clica no botão Reproduzir, é possível buscar no local gravado e chamar `Netstream.play()`.

## Data inicial {#start-date}

Especifica a data após a qual uma licença é válida.

Exemplo de caso de uso: use uma data absoluta para emitir licenças de conteúdo antes da data de disponibilidade de um ativo, ou para aplicar um período de &quot;embargo&quot;.

## Data final {#end-date}

Especifica a data após a qual uma licença expira.

Exemplo de caso de uso: use uma data de expiração absoluta para refletir o fim dos direitos de distribuição.

## Data final relativa {#relative-end-date}

Especifica a data de expiração da licença, expressa em relação à data de embalagem.

Exemplo de caso de uso: em um processo automatizado de empacotamento, use uma única política com essa opção para uma série de vídeos, a fim de definir a data de expiração para 30 dias em relação à data do empacotamento.

## Duração do cache de licenças {#license-caching-duration}

Especifica a duração em que uma licença pode ser armazenada em cache no disco no License Store local do cliente sem exigir a reaquisição do servidor de licenças. Como alternativa, você pode especificar uma data/hora absoluta após a qual uma licença não poderá mais ser armazenada em cache.

Depois que a data de expiração do cache for ultrapassada, a licença não será mais válida e o cliente deverá solicitar uma nova licença ao servidor de licenças.

Exemplo de caso de uso: use a duração do armazenamento em cache de licença para especificar uma quantidade fixa de tempo válida para uma licença específica, como em um caso de uso de aluguel. Uma locação de 30 dias pode ser especificada (com cache de licença) para indicar a duração total da licença dentro da qual o conteúdo será consumido.

## Janela de reprodução {#playback-window}

Especifica a duração em que uma licença é válida após a primeira vez em que é usada para reproduzir conteúdo protegido.

Exemplo de caso de uso: alguns modelos de negócios permitem um período de aluguel de 30 dias, mas, uma vez que a reprodução começa, ela deve ser concluída em 48 horas. Essa duração de 48 horas da licença é definida como a janela de reprodução.

## Requisitos para sincronização {#requirements-for-synchronization}

Especifica a frequência com que o cliente sincronizará seu estado com o servidor. Se uma licença fora de banda tiver sido emitida ao cliente (sem que um servidor de licenças tenha sido contatado), as regras de uso poderão especificar que o cliente deve enviar mensagens de sincronização ao servidor para sincronizar o tempo seguro do cliente e relatar o estado do cliente ao servidor.

O comportamento de sincronização é definido usando os seguintes parâmetros:

* Intervalo de Início — Especifica o tempo de espera após a última sincronização bem-sucedida para iniciar outra solicitação de sincronização.
* Intervalo de Interrupção Permanente — (Opcional). Não permitir reprodução se uma sincronização bem-sucedida não tiver ocorrido no período especificado.
* Probabilidade de sincronização forçada — (opcional). Probabilidade com a qual o cliente deve enviar uma mensagem de sincronização antes do próximo intervalo de início.

>[!NOTE]
>
>Esta regra de uso é suportada pelos clientes Adobe Access versões 3.0 e superiores. O comportamento em clientes mais antigos depende da versão mínima do cliente suportada pelo servidor de licenças. Consulte [Versão Mínima do Cliente](../../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).
