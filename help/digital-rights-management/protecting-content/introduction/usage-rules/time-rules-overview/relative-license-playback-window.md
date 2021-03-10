---
title: Janela de reprodução
description: Janela de reprodução
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Janela de reprodução{#playback-window}

A janela de reprodução especifica a duração em que uma licença é válida após a primeira vez em que é usada para reproduzir conteúdo protegido.

Exemplo de caso de uso: Alguns modelos de negócios permitem um período de aluguel de 30 dias, mas, uma vez iniciada a reprodução, a reprodução deve ser concluída em 48 horas. Nesse caso, a duração de 48 horas da licença é a janela de reprodução.

**A partir da versão 5.3**  - A janela de reprodução também oferece suporte à opção de ativar ou desativar a Parada forçada, indicando se o contexto de descriptografia para a reprodução deve parar na expiração da janela de reprodução (ativada) ou continuar apesar da expiração (desativada).

>[!NOTE]
>
>A opção de interrupção permanente não funciona corretamente com a Janela de reprodução, se usada em conjunto com ela (a Janela de reprodução não será respeitada). Reproduzir o conteúdo com a janela Reprodução sem parada segura respeita a restrição da janela de reprodução.

