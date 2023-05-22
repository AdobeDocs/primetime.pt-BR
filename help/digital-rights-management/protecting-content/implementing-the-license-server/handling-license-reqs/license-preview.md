---
title: Visualização da licença
description: Visualização da licença
copied-description: true
exl-id: 7e6b1062-7240-4dae-86bb-bd26e7be1f14
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Visualização da licença{#license-preview}

O cliente pode enviar uma solicitação de visualização de licença, o que significa que o aplicativo pode realizar uma operação de visualização antes de solicitar que o usuário compre o conteúdo para determinar se a máquina do usuário realmente atende a todos os critérios necessários para a reprodução.

*`License preview`* refere-se à capacidade de um cliente de visualizar a licença (para ver quais direitos a licença permite) em vez de visualizar o conteúdo (visualizar uma pequena parte do conteúdo antes de decidir comprar). Alguns dos parâmetros exclusivos de cada computador são: saídas disponíveis e status de proteção, tempo de execução/versão de DRM disponível e nível de segurança do cliente de DRM. O modo de visualização de licença permite que o cliente de tempo de execução/DRM teste a lógica de negócios do servidor de licenças e forneça as informações ao usuário para que ele possa tomar uma decisão informada. Assim, o cliente pode ver a aparência de uma licença válida, mas não receberia a chave para descriptografar o conteúdo. O suporte para a pré-visualização de licença é opcional e só é necessário se você implementar um cliente personalizado que use essa funcionalidade.

Para determinar se o cliente enviou uma solicitação de visualização ou de aquisição de licença, ligue para `LicenseRequestMessage.getRequestPhase()`e compare-o com `LicenseRequestMessage.RequestPhase.Acquire`
