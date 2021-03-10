---
description: Assim que o servidor de licenças ler um dos arquivos de configuração do servidor de licenças (configuração global ou de locatário), as informações de configuração serão armazenadas em cache na memória. Portanto, os arquivos não precisam ser lidos do disco para cada solicitação de licença. No entanto, o servidor também permite que a maioria dos valores nos arquivos de configuração seja modificada sem exigir uma reinicialização do servidor para que as alterações entrem em vigor.
title: Atualização de arquivos de configuração
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# Atualização dos arquivos de configuração{#updating-configuration-files}

Assim que o servidor de licenças ler um dos arquivos de configuração do servidor de licenças (configuração global ou de locatário), as informações de configuração serão armazenadas em cache na memória. Portanto, os arquivos não precisam ser lidos do disco para cada solicitação de licença. No entanto, o servidor também permite que a maioria dos valores nos arquivos de configuração seja modificada sem exigir uma reinicialização do servidor para que as alterações entrem em vigor.

Sempre que você modifica o arquivo de configuração, o servidor de licenças armazena a hora em que o arquivo foi modificado pela última vez. Em um intervalo configurável, o servidor verifica se o tempo de modificação do arquivo foi alterado. Se tiver sido alterado, o servidor recarregará automaticamente o conteúdo do arquivo de configuração.

Se você quiser controlar a frequência com que o servidor verifica se há atualizações, é necessário definir o atributo `refreshDelaySeconds` no elemento `Caching` do arquivo de configuração global. Por exemplo, se `refreshDelaySeconds` for definido como 3600 segundos, o servidor atualizará a configuração no máximo uma hora após o tempo de modificação do arquivo de configuração. Se `refreshDelaySeconds` estiver definido como 0, o servidor verificará se há atualizações de configuração a cada solicitação. Não é recomendável definir `refreshDelaySeconds` como um valor baixo em qualquer ambiente de produção, pois isso pode afetar o desempenho.

O elemento `Caching` também controla quantas configurações de locatários são armazenadas em cache ao mesmo tempo. Você pode definir esse valor para um número menor que o número total de locatários para limitar a quantidade de memória usada para armazenar em cache as informações de configuração. Se uma solicitação for recebida para um locatário que não está no cache, a configuração será carregada antes que a solicitação possa ser processada. Se o cache estiver cheio, o locatário menos usado recentemente será removido do cache.

A versão em cache da configuração continua a ser usada nas seguintes situações (até a próxima vez que o servidor verificar se há atualizações):

* Se uma alteração for salva em um arquivo de configuração ou em qualquer um dos arquivos de certificado referenciados no arquivo [!DNL flashaccess-tenant.xml] enquanto o servidor tenta ler o arquivo
* Se o carimbo de data e hora do arquivo for menos de um segundo antes da hora atual
* Se o carimbo de data e hora do arquivo estiver no futuro

Se não houver uma versão em cache, o carregamento da configuração falhará e um erro será retornado ao cliente. Em seguida, o servidor tenta carregar o arquivo novamente na próxima vez que receber uma solicitação para esse locatário.

## Atualização do arquivo de configuração global {#section_AA546C72442646CFB8906AEEBDF50587}

Você pode modificar a senha do HSM em [!DNL flashaccess-global.xml] a qualquer momento. As alterações entrarão em vigor na próxima vez que o servidor recarregar o arquivo de configuração. No entanto, as alterações nos elementos Log e Caching não são recarregadas. É necessário reiniciar o servidor antes que qualquer alteração nesses elementos se torne efetiva.

## Atualização do arquivo de configuração do locatário {#section_71624DB8DF28480F84F34F0FF7FD4365}

Você pode modificar todos os valores especificados no arquivo [!DNL flashaccess-tenant.xml] a qualquer momento. As alterações entrarão em vigor na próxima vez que o servidor recarregar o arquivo de configuração. Além disso, o servidor verifica se há modificações em todos os arquivos de credencial ( [!DNL .pfx]) e de certificado de lista de permissões do empacotador referenciados no arquivo de configuração do locatário.
