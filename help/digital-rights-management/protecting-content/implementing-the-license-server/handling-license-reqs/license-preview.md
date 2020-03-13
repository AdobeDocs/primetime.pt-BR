---
seo-title: Visualização de licença
title: Visualização de licença
uuid: 3069aa16-5bf3-4af6-801c-ad823530d7eb
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Visualização de licença{#license-preview}

O cliente pode enviar uma solicitação de visualização de licença, o que significa que o aplicativo pode realizar uma operação de visualização antes de solicitar que o usuário compre o conteúdo para determinar se o computador do usuário realmente atende a todos os critérios necessários para a reprodução.

*`License preview`* refere-se à capacidade de um cliente visualizar a licença (para ver quais direitos a licença permite) em vez de visualizar o conteúdo (exibir uma pequena parte do conteúdo antes de decidir comprar). Alguns dos parâmetros exclusivos para cada máquina são: saídas disponíveis e seu status de proteção, o tempo de execução/versão DRM disponível e o nível de segurança do cliente DRM. O modo de visualização de licença permite que o cliente do tempo de execução/DRM teste a lógica comercial do servidor de licença e forneça informações ao usuário para que ele possa tomar uma decisão informada. Assim, o cliente pode ver a aparência de uma licença válida, mas não receberá a chave para descriptografar o conteúdo. O suporte para visualização de licença é opcional e só é necessário se você implementar um cliente personalizado que usa essa funcionalidade.

Para determinar se o cliente enviou uma solicitação de visualização ou de aquisição de licença, chame `LicenseRequestMessage.getRequestPhase()`e compare-a com `LicenseRequestMessage.RequestPhase.Acquire`
