---
title: Janela de reprodução
description: Janela de reprodução
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Janela de reprodução{#playback-window}

A janela de reprodução especifica a duração em que uma licença é válida após a primeira vez em que é usada para reproduzir conteúdo protegido.

Exemplo de caso de uso: alguns modelos de negócios permitem um período de aluguel de 30 dias, mas, uma vez que a reprodução começar, ela deverá ser concluída em 48 horas. Nesse caso, a duração de 48 horas da licença é a janela de reprodução.

**Da versão 5.3 em diante** - A janela de reprodução também suporta a opção de ativar ou desativar a paragem forçada, que indica se o contexto de descriptografia da reprodução deve parar ao expirar a janela de reprodução (ativada) ou continuar apesar da expiração (desativada).

>[!NOTE]
>
>A opção de parada forçada não funciona corretamente com a Janela de reprodução se usada em conjunto com ela (a Janela de reprodução não será aplicada). A reprodução de conteúdo com a janela de reprodução sem interrupção segura respeita a restrição da janela de reprodução.

