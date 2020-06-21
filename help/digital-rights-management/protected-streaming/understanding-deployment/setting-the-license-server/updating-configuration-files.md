---
description: Assim que o servidor de licenças ler um dos arquivos de configuração do servidor de licenças (configuração global ou de locatário), as informações de configuração serão armazenadas em cache na memória. Portanto, os arquivos não precisam ser lidos do disco para cada solicitação de licença. No entanto, o servidor também permite que a maioria dos valores nos arquivos de configuração sejam modificados sem a necessidade de uma reinicialização do servidor para que as alterações entrem em vigor.
seo-description: Assim que o servidor de licenças ler um dos arquivos de configuração do servidor de licenças (configuração global ou de locatário), as informações de configuração serão armazenadas em cache na memória. Portanto, os arquivos não precisam ser lidos do disco para cada solicitação de licença. No entanto, o servidor também permite que a maioria dos valores nos arquivos de configuração sejam modificados sem a necessidade de uma reinicialização do servidor para que as alterações entrem em vigor.
seo-title: Atualização de arquivos de configuração
title: Atualização de arquivos de configuração
uuid: 34b3247c-3458-49de-b1b0-dc0ebbf61c88
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---


# Atualização de arquivos de configuração{#updating-configuration-files}

Assim que o servidor de licenças ler um dos arquivos de configuração do servidor de licenças (configuração global ou de locatário), as informações de configuração serão armazenadas em cache na memória. Portanto, os arquivos não precisam ser lidos do disco para cada solicitação de licença. No entanto, o servidor também permite que a maioria dos valores nos arquivos de configuração sejam modificados sem a necessidade de uma reinicialização do servidor para que as alterações entrem em vigor.

Sempre que você modifica o arquivo de configuração, o servidor de licenças armazena a hora em que o arquivo foi modificado pela última vez. Em um intervalo configurável, o servidor verifica se a hora de modificação do arquivo foi alterada. Se tiver sido alterado, o servidor recarregará automaticamente o conteúdo do arquivo de configuração.

Se você quiser controlar a frequência com que o servidor verifica se há atualizações, é necessário definir o `refreshDelaySeconds` atributo no `Caching` elemento do arquivo de configuração global. Por exemplo, se `refreshDelaySeconds` estiver definido como 3600 segundos, o servidor atualizará a configuração no máximo uma hora após a hora de modificação do arquivo de configuração. Se `refreshDelaySeconds` estiver definido como 0, o servidor verificará se há atualizações de configuração a cada solicitação. Não é recomendável definir um valor baixo `refreshDelaySeconds` em nenhum ambiente de produção, pois isso pode afetar o desempenho.

O `Caching` elemento também controla quantas configurações de inquilinos são armazenadas em cache ao mesmo tempo. É possível definir esse valor para um número menor que o número total de locatários para limitar a quantidade de memória usada para armazenar em cache as informações de configuração. Se uma solicitação for recebida para um locatário que não está no cache, a configuração será carregada antes que a solicitação possa ser processada. Se o cache estiver cheio, o locatário usado mais recentemente será removido do cache.

A versão em cache da configuração continua a ser usada nas seguintes situações (até a próxima vez que o servidor verificar atualizações):

* Se uma alteração for salva em um arquivo de configuração ou em qualquer um dos arquivos de certificado referenciados no [!DNL flashaccess-tenant.xml] arquivo enquanto o servidor tentar ler o arquivo
* Se o carimbo de data e hora do arquivo for encontrado com menos de um segundo antes da hora atual
* Se o carimbo de data e hora do arquivo estiver no futuro

Se não houver uma versão em cache, o carregamento da configuração falhará e um erro será retornado ao cliente. O servidor tentará carregar o arquivo novamente na próxima vez que receber uma solicitação para o locatário.

## Atualização do arquivo de configuração global {#section_AA546C72442646CFB8906AEEBDF50587}

Você pode modificar a senha HSM a qualquer [!DNL flashaccess-global.xml] momento. As alterações entrarão em vigor na próxima vez que o servidor recarregar o arquivo de configuração. No entanto, as alterações nos elementos de Log e Cache não são recarregadas. É necessário reiniciar o servidor antes que as alterações nesses elementos entrem em vigor.

## Atualização do arquivo de configuração do locatário {#section_71624DB8DF28480F84F34F0FF7FD4365}

Você pode modificar todos os valores especificados no [!DNL flashaccess-tenant.xml] arquivo a qualquer momento. As alterações entrarão em vigor na próxima vez que o servidor recarregar o arquivo de configuração. Além disso, o servidor verifica se há modificações em todos os arquivos de credencial ( [!DNL .pfx]) e o empacotador permite arquivos de certificado de lista referenciados no arquivo de configuração do locatário.
