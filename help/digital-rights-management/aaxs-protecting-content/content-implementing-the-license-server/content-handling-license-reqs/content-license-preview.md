---
title: Visualização da licença
description: Visualização da licença
copied-description: true
exl-id: 283ee661-b1ee-46b9-9337-0497c97bd785
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Visualização da licença{#license-preview}

O cliente pode enviar uma solicitação de visualização de licença, o que significa que o aplicativo pode realizar uma operação de visualização antes de solicitar que o usuário compre o conteúdo para determinar se a máquina do usuário realmente atende a todos os critérios necessários para a reprodução. *Visualização da licença* refere-se à capacidade do cliente de visualizar a licença (para ver quais direitos a licença permite) em vez de visualizar o conteúdo (visualizar uma pequena parte do conteúdo antes de decidir comprar). Alguns dos parâmetros exclusivos de cada computador são: saídas disponíveis e status de proteção, tempo de execução/versão de DRM disponível e nível de segurança do cliente de DRM. O modo de visualização de licença permite que o cliente de tempo de execução/DRM teste a lógica de negócios do servidor de licenças e forneça as informações ao usuário para que ele possa tomar uma decisão informada. Assim, o cliente pode ver a aparência de uma licença válida, mas não receberia a chave para descriptografar o conteúdo. O suporte para a pré-visualização de licença é opcional e só é necessário se você implementar um cliente personalizado que use essa funcionalidade.

Para determinar se o cliente enviou uma solicitação de visualização ou de aquisição de licença, ligue para `LicenseRequestMessage.getRequestPhase()`e compare-o com `LicenseRequestMessage.RequestPhase.Acquire`
