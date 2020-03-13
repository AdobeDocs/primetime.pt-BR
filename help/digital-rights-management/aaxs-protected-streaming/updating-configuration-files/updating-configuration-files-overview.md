---
seo-title: Atualização da visão geral dos arquivos de configuração
title: Atualização da visão geral dos arquivos de configuração
uuid: e9be21cf-ad23-4ed6-8bef-f194bc1fd749
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Atualização da visão geral dos arquivos de configuração {#updating-configuration-files-overview}

Quando o servidor de licenças ler um dos arquivos de configuração do servidor de licenças (configuração global ou de locatário), as informações de configuração serão armazenadas em cache na memória. Portanto, os arquivos não precisam ser lidos do disco para cada solicitação de licença. No entanto, o servidor também permite que a maioria dos valores nos arquivos de configuração sejam modificados sem a necessidade de uma reinicialização do servidor para que as alterações entrem em vigor. (Consulte abaixo para obter detalhes sobre quais valores de configuração são verificados para atualizações.)

Para recarregar a configuração quando as alterações são feitas, o servidor de licenças armazena a hora em que o arquivo foi modificado pela última vez. Em um intervalo configurável, o servidor verifica se a hora de modificação do arquivo foi alterada e, em caso afirmativo, recarrega o conteúdo do arquivo.

Para controlar a frequência com que o servidor verifica se há atualizações, defina o `refreshDelaySeconds` atributo no elemento Cache do arquivo de configuração global. Por exemplo, se `refreshDelaySeconds` estiver definido como 3600 segundos, levará no máximo uma hora do momento em que o arquivo for atualizado para que qualquer atualização de configuração seja detectada pelo servidor. Se `refreshDelaySeconds` estiver definido como 0, o servidor verificará se há atualizações de configuração em cada solicitação. Não é recomendável configurar `refreshDelaySeconds` para ambientes de produção, pois isso pode afetar o desempenho.

O elemento Cache também controla quantas configurações de inquilinos são armazenadas em cache ao mesmo tempo. É possível definir esse valor para um número menor que o número total de locatários para limitar a quantidade de memória usada para armazenar em cache as informações de configuração. Se uma solicitação for recebida para um locatário que não esteja no cache, a configuração será carregada antes que a solicitação possa ser processada. Se o cache estiver cheio, o locatário usado mais recentemente será removido do cache.

Se uma alteração for salva em um arquivo de configuração ou em qualquer um dos arquivos de certificado referenciados durante [!DNL flashaccess-tenant.xml] a tentativa do servidor de ler o arquivo, ou se o carimbo de data e hora do arquivo for encontrado menos de um segundo antes da hora atual ou estiver no futuro, a versão em cache da configuração será usada até a próxima vez que o servidor verificar se há atualizações. Se não houver uma versão em cache, o carregamento da configuração falhará e um erro será retornado ao cliente. O servidor tentará carregar o arquivo novamente na próxima vez que receber uma solicitação para o locatário.
