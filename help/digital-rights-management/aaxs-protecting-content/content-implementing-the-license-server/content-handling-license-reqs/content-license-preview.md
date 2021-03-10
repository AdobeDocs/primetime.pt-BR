---
title: Visualização da licença
description: Visualização da licença
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---


# Visualização da licença{#license-preview}

O cliente pode enviar uma solicitação de pré-visualização de licença, o que significa que o aplicativo pode realizar uma operação de pré-visualização antes de solicitar que o usuário compre o conteúdo para determinar se a máquina do usuário realmente atende a todos os critérios necessários para a reprodução. *A* pré-visualização da licença refere-se à capacidade do cliente de visualizar a licença (para ver quais direitos a licença permite) em vez de visualizar o conteúdo (visualizar uma pequena parte do conteúdo antes de decidir comprar). Alguns dos parâmetros exclusivos de cada máquina são: As saídas disponíveis e o status de proteção, a versão de tempo de execução/DRM disponível e o nível de segurança do cliente DRM. O modo de visualização de licença permite que o cliente de tempo de execução/DRM teste a lógica comercial do servidor de licenças e forneça informações ao usuário para que ele possa tomar uma decisão informada. Assim, o cliente pode ver a aparência de uma licença válida, mas não receberia a chave para descriptografar o conteúdo. O suporte para pré-visualização de licença é opcional e necessário somente se você implementar um cliente personalizado que use essa funcionalidade.

Para determinar se o cliente enviou uma solicitação de pré-visualização ou solicitação de aquisição de licença, chame `LicenseRequestMessage.getRequestPhase()`e compare-a com `LicenseRequestMessage.RequestPhase.Acquire`
