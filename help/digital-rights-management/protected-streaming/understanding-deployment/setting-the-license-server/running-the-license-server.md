---
seo-title: Execução do servidor DRM para streaming protegido
title: Execução do servidor DRM para streaming protegido
uuid: 9bbe211d-268b-43c2-9e55-7ce62de40d30
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 0%

---


# Execução do servidor DRM para streaming protegido {#running-the-drm-server-for-protected-streaming}

Antes de poder start do Adobe Primetime DRM Server for Protected Streaming, é recomendável verificar a validade das configurações nos arquivos de configuração.

Você pode verificar a validade das configurações usando os utilitários fornecidos com o servidor de licenças. (Consulte Validador *de configuração* neste guia.

Se você quiser start o Tomcat e o servidor de licenças, é necessário executar [!DNL catalina.bat start] ou executar [!DNL catalina.sh start] a partir do [!DNL bin] diretório do Tomcat.

Depois que o servidor for iniciado, verifique se ele foi configurado corretamente abrindo [!DNL https://<lic<span></span>ense-server-host:port>/flashaccess server/<tenant-name>/flashaccess/license/v1] em uma janela do navegador. Se a configuração do locatário tiver sido carregada com êxito, uma mensagem de confirmação será exibida.

## Arquivos de registro {#log-files}

Os arquivos de log gerados pelo Adobe Primetime DRM Server para o aplicativo Protected Streaming estão localizados no diretório especificado por LicenseServer.LogRoot.

>[!NOTE]
>
>Se os arquivos de log atuais forem excluídos ou movidos enquanto o servidor for executado, o arquivo de log talvez não seja recriado. Portanto, algumas informações de log podem ser excluídas.

### Estrutura do diretório de log {#section_F490A483D60145ADBC21038914C39203}

Os diretórios de log são estruturados para facilitar o uso. O diretório de log tem a seguinte estrutura:

```
<i class="+ topic ph hi-d="" i "="">
 LicenseServer.LogRoot/ 
 flashaccess-global.log 
     flashaccessserver/ 
         flashaccess-partition.log 
         tenants/ 
             
 <i class="+ topic ph hi-d="" i "="">
  tenantname/ 
                  flashaccess-tenant.log
 </i class="+ topic>
</i class="+ topic>
```

### Arquivo de log global {#section_1CFA90748142439C9F3BE380969539DA}

O arquivo de log global, [!DNL flashaccess-global.log], está localizado em *LicenseServer.LogRoot*. O log pode incluir mensagens de log que o Adobe Primetime DRM Java SDK ou as mensagens de log podem ter gerado durante o tempo em que o servidor foi inicializado.

### Arquivo de log de partição {#section_5660137CD6AA40519E72A4315534846B}

O arquivo de log de partição, [!DNL flashaccess-partition.log], está localizado no [!DNL <LicenseServer.LogRoot>/flashaccesserver] diretório. Inclui mensagens de log que foram geradas durante o processamento de uma solicitação de licença.

### Arquivo de log do locatário {#section_F0257CC0831647F18A746B4F02E3E910}

O arquivo de log de locatário de cada locatário, [!DNL flashaccess-tenant.log], está localizado em [!DNL &lt;LicenseServer.LogRoot>/flashaccessServer/tenants/<tenantname>]. O log de locatário inclui informações de auditoria que descrevem cada licença gerada para este locatário.

## Atualização de arquivos de configuração {#updating-configuration-files}

Assim que o servidor de licenças ler um dos arquivos de configuração do servidor de licenças (configuração global ou de locatário), as informações de configuração serão armazenadas em cache na memória. Portanto, os arquivos não precisam ser lidos do disco para cada solicitação de licença. No entanto, o servidor também permite que a maioria dos valores nos arquivos de configuração sejam modificados sem a necessidade de uma reinicialização do servidor para que as alterações entrem em vigor.

Sempre que você modifica o arquivo de configuração, o servidor de licenças armazena a hora em que o arquivo foi modificado pela última vez. Em um intervalo configurável, o servidor verifica se a hora de modificação do arquivo foi alterada. Se tiver sido alterado, o servidor recarregará automaticamente o conteúdo do arquivo de configuração.

Se você quiser controlar a frequência com que o servidor verifica se há atualizações, é necessário definir o `refreshDelaySeconds` atributo no `Caching` elemento do arquivo de configuração global. Por exemplo, se `refreshDelaySeconds` estiver definido como 3600 segundos, o servidor atualizará a configuração no máximo uma hora após a hora de modificação do arquivo de configuração. Se `refreshDelaySeconds` estiver definido como 0, o servidor verificará se há atualizações de configuração a cada solicitação. Não é recomendável definir um valor baixo `refreshDelaySeconds` em nenhum ambiente de produção, pois isso pode afetar o desempenho.

O `Caching` elemento também controla quantas configurações de inquilinos são armazenadas em cache ao mesmo tempo. É possível definir esse valor para um número menor que o número total de locatários para limitar a quantidade de memória usada para armazenar em cache as informações de configuração. Se uma solicitação for recebida para um locatário que não está no cache, a configuração será carregada antes que a solicitação possa ser processada. Se o cache estiver cheio, o locatário usado mais recentemente será removido do cache.

A versão em cache da configuração continua a ser usada nas seguintes situações (até a próxima vez que o servidor verificar atualizações):

* Se uma alteração for salva em um arquivo de configuração ou em qualquer um dos arquivos de certificado referenciados no [!DNL flashaccess-tenant.xml] arquivo enquanto o servidor tentar ler o arquivo
* Se o carimbo de data e hora do arquivo for encontrado com menos de um segundo antes da hora atual
* Se o carimbo de data e hora do arquivo estiver no futuro

Se não houver uma versão em cache, o carregamento da configuração falhará e um erro será retornado ao cliente. O servidor tentará carregar o arquivo novamente na próxima vez que receber uma solicitação para o locatário.

### Atualização do arquivo de configuração global {#section_AA546C72442646CFB8906AEEBDF50587}

Você pode modificar a senha HSM a qualquer [!DNL flashaccess-global.xml] momento. As alterações entrarão em vigor na próxima vez que o servidor recarregar o arquivo de configuração. No entanto, as alterações nos elementos de Log e Cache não são recarregadas. É necessário reiniciar o servidor antes que as alterações nesses elementos entrem em vigor.

### Atualização do arquivo de configuração do locatário {#section_71624DB8DF28480F84F34F0FF7FD4365}

Você pode modificar todos os valores especificados no [!DNL flashaccess-tenant.xml] arquivo a qualquer momento. As alterações entrarão em vigor na próxima vez que o servidor recarregar o arquivo de configuração. Além disso, o servidor verifica se há modificações em todos os arquivos de credencial ( [!DNL .pfx]) e arquivos de certificado de lista de permissões do empacotador referenciados no arquivo de configuração do locatário.