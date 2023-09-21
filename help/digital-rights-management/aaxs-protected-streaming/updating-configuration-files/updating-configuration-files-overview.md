---
title: Visão geral da atualização de arquivos de configuração
description: Visão geral da atualização de arquivos de configuração
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Visão geral da atualização de arquivos de configuração {#updating-configuration-files-overview}

Quando o servidor de licença ler um dos arquivos de configuração do servidor de licença (configuração global ou de locatário), as informações de configuração serão armazenadas em cache na memória. Portanto, os arquivos não precisam ser lidos do disco para cada solicitação de licença. No entanto, o servidor também permite que a maioria dos valores nos arquivos de configuração seja modificada sem exigir uma reinicialização do servidor para que as alterações entrem em vigor. (Consulte abaixo para obter detalhes sobre quais valores de configuração são verificados em busca de atualizações.)

Para recarregar a configuração quando são feitas alterações, o servidor de licença armazena a hora em que o arquivo foi modificado pela última vez. Em um intervalo configurável, o servidor verifica se a hora de modificação do arquivo foi alterada e, nesse caso, recarrega o conteúdo do arquivo.

Para controlar a frequência com que o servidor verifica se há atualizações, defina o `refreshDelaySeconds` no elemento Caching do arquivo de configuração global. Por exemplo, se `refreshDelaySeconds` for definido como 3600 segundos, levará no máximo uma hora a partir do momento em que o arquivo for atualizado para que qualquer atualização de configuração seja detectada pelo servidor. Se `refreshDelaySeconds` for definido como 0, o servidor verificará se há atualizações de configuração em cada solicitação. Configuração `refreshDelaySeconds` para um valor baixo não é recomendado para ambientes de produção, pois poderia afetar o desempenho.

O elemento Cache também controla quantas configurações de locatários são armazenadas em cache de uma só vez. Você pode definir esse valor como um número menor que o número total de locatários para limitar a quantidade de memória usada para armazenar as informações de configuração em cache. Se uma solicitação for recebida para um locatário que não está no cache, a configuração será carregada antes que a solicitação possa ser processada. Se o cache estiver cheio, o locatário menos usado recentemente será removido do cache.

Se uma alteração for salva em um arquivo de configuração ou em qualquer um dos arquivos de certificado referenciados no [!DNL flashaccess-tenant.xml] enquanto o servidor está tentando ler o arquivo, ou se o carimbo de data e hora do arquivo for encontrado menos de um segundo antes da hora atual ou estiver no futuro, a versão em cache da configuração será usada até a próxima vez que o servidor verificar se há atualizações. Se não houver nenhuma versão em cache, o carregamento da configuração falhará e um erro será retornado ao cliente. O servidor tenta carregar o arquivo novamente na próxima vez que receber uma solicitação para esse locatário.
