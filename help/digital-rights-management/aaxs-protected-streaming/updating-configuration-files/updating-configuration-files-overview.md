---
title: Visão geral da atualização dos arquivos de configuração
description: Visão geral da atualização dos arquivos de configuração
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# Atualização da visão geral dos arquivos de configuração {#updating-configuration-files-overview}

Depois que o servidor de licenças ler um dos arquivos de configuração do servidor de licenças (configuração global ou de locatário), as informações de configuração serão armazenadas em cache na memória. Portanto, os arquivos não precisam ser lidos do disco para cada solicitação de licença. No entanto, o servidor também permite que a maioria dos valores nos arquivos de configuração seja modificada sem exigir uma reinicialização do servidor para que as alterações entrem em vigor. (Consulte abaixo para obter detalhes sobre quais valores de configuração são verificados em busca de atualizações.)

Para recarregar a configuração quando as alterações forem feitas, o servidor de licenças armazena o momento em que o arquivo foi modificado pela última vez. Em um intervalo configurável, o servidor verifica se o tempo de modificação do arquivo foi alterado e, nesse caso, recarrega o conteúdo do arquivo.

Para controlar a frequência com que o servidor verifica se há atualizações, defina o atributo `refreshDelaySeconds` no elemento Cache do arquivo de configuração global. Por exemplo, se `refreshDelaySeconds` estiver definido como 3600 segundos, levará no máximo uma hora a partir do momento em que o arquivo for atualizado para que todas as atualizações de configuração sejam detectadas pelo servidor. Se `refreshDelaySeconds` estiver definido como 0, o servidor verificará se há atualizações de configuração em cada solicitação. Não é recomendado configurar `refreshDelaySeconds` para um valor baixo em ambientes de produção, pois isso pode afetar o desempenho.

O elemento Caching também controla quantas configurações de locatários são armazenadas em cache ao mesmo tempo. Você pode definir esse valor para um número menor que o número total de locatários para limitar a quantidade de memória usada para armazenar em cache as informações de configuração. Se uma solicitação for recebida para um locatário que não está no cache, a configuração será carregada antes que a solicitação possa ser processada. Se o cache estiver cheio, o locatário menos usado recentemente será removido do cache.

Se uma alteração for salva em um arquivo de configuração ou em qualquer um dos arquivos de certificado referenciados em [!DNL flashaccess-tenant.xml] enquanto o servidor estiver tentando ler o arquivo, ou se o carimbo de data e hora do arquivo for encontrado como menos de um segundo antes da hora atual ou no futuro, a versão em cache da configuração será usada até a próxima vez que o servidor verificar se há atualizações. Se não houver uma versão em cache, o carregamento da configuração falhará e um erro será retornado ao cliente. O servidor tenta carregar o arquivo novamente na próxima vez que receber uma solicitação para esse locatário.
