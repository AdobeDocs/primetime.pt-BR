---
title: Execução do servidor DRM para transmissão protegida
description: Execução do servidor DRM para transmissão protegida
copied-description: true
exl-id: 05dc4c55-a97e-4bdc-aea8-32741299454c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---

# Execução do servidor DRM para transmissão protegida {#running-the-drm-server-for-protected-streaming}

Antes de iniciar o servidor DRM da Adobe Primetime para transmissão protegida, é recomendável verificar a validade das configurações nos arquivos de configuração.

Você pode verificar a validade das configurações usando os utilitários fornecidos com o servidor de licenças. (Consulte *Validador de configuração* neste guia.

Se você deseja iniciar o Tomcat e o servidor de licenças, é necessário executar [!DNL catalina.bat start] ou [!DNL catalina.sh start] do Tomcat [!DNL bin] diretório.

Depois que o servidor for iniciado, é necessário verificar se ele foi configurado corretamente abrindo `https://<lic<span></span>ense-server-host:port>/flashaccessserver/<tenant-name>/flashaccess/license/v1` em uma janela do navegador. Se a configuração do locatário tiver sido carregada com sucesso, uma mensagem de confirmação será exibida.

## Arquivos de log {#log-files}

Os arquivos de log gerados pelo aplicativo Adobe Primetime DRM Server for Protected Streaming estão localizados no diretório especificado por LicenseServer.LogRoot.

>[!NOTE]
>
>Se os arquivos de log atuais forem excluídos ou movidos enquanto o servidor estiver em execução, talvez o arquivo de log não seja recriado. Portanto, algumas informações de log podem ser excluídas.

### Estrutura do diretório de log {#section_F490A483D60145ADBC21038914C39203}

Os diretórios de registro são estruturados para facilitar o uso. O diretório de log tem a seguinte estrutura:

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

O arquivo de log global, [!DNL flashaccess-global.log], está localizado em *LicenseServer.LogRoot*. O registro pode incluir mensagens de registro que o SDK do Java do Adobe Primetime DRM ou mensagens de registro podem ter gerado durante o tempo em que o servidor foi inicializado.

### Arquivo de log da partição {#section_5660137CD6AA40519E72A4315534846B}

O arquivo de log da partição, [!DNL flashaccess-partition.log], está localizado na `<LicenseServer.LogRoot>/flashaccesserver` diretório. Inclui mensagens de log que foram geradas durante o processamento de uma solicitação de licença.

### Arquivo de log do locatário {#section_F0257CC0831647F18A746B4F02E3E910}

Arquivo de log do locatário de cada locatário, [!DNL flashaccess-tenant.log], está localizado em `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`. O log do locatário inclui informações de auditoria que descrevem cada licença gerada para este locatário.

## Atualização de arquivos de configuração {#updating-configuration-files}

Assim que o servidor de licença ler um dos arquivos de configuração do servidor de licença (configuração global ou de locatário), as informações de configuração serão armazenadas em cache na memória. Portanto, os arquivos não precisam ser lidos do disco para cada solicitação de licença. No entanto, o servidor também permite que a maioria dos valores nos arquivos de configuração seja modificada sem exigir uma reinicialização do servidor para que as alterações entrem em vigor.

Sempre que você modifica o arquivo de configuração, o servidor de licença armazena a hora em que o arquivo foi modificado pela última vez. Em um intervalo configurável, o servidor verifica se a hora de modificação do arquivo foi alterada. Se tiver sido alterado, o servidor recarregará automaticamente o conteúdo do arquivo de configuração.

Se quiser controlar a frequência com que o servidor verifica se há atualizações, é necessário definir o `refreshDelaySeconds` atributo no `Caching` elemento do arquivo de configuração global. Por exemplo, se `refreshDelaySeconds` for definida como 3600 segundos, o servidor atualizará a configuração no máximo uma hora após o horário de modificação do arquivo de configuração. Se `refreshDelaySeconds` for definido como 0, o servidor verificará as atualizações de configuração a cada solicitação. Não é recomendável definir `refreshDelaySeconds` a um valor baixo em qualquer ambiente de produção, pois isso pode afetar o desempenho.

A variável `Caching` O elemento também controla quantas configurações de locatários são armazenadas em cache de uma só vez. Você pode definir esse valor como um número menor que o número total de locatários para limitar a quantidade de memória que está sendo usada para armazenar as informações de configuração em cache. Se uma solicitação for recebida para um locatário que não está no cache, a configuração será carregada antes que a solicitação possa ser processada. Se o cache estiver cheio, o locatário menos usado recentemente será removido do cache.

A versão em cache da configuração continua a ser usada nas seguintes situações (até a próxima vez que o servidor verificar se há atualizações):

* Se uma alteração for salva em um arquivo de configuração ou em qualquer um dos arquivos de certificado referenciados na [!DNL flashaccess-tenant.xml] enquanto o servidor tenta ler o arquivo
* Se o carimbo de data e hora do arquivo for anterior em menos de um segundo à hora atual
* Se o carimbo de data e hora do arquivo estiver no futuro

Se não houver nenhuma versão em cache, o carregamento da configuração falhará e um erro será retornado ao cliente. O servidor tenta carregar o arquivo novamente na próxima vez que receber uma solicitação para esse locatário.

### Atualização do arquivo de configuração global {#section_AA546C72442646CFB8906AEEBDF50587}

Você pode modificar a senha do HSM no [!DNL flashaccess-global.xml] a qualquer momento. As alterações entrarão em vigor na próxima vez que o servidor recarregar o arquivo de configuração. No entanto, as alterações nos elementos de Log e Cache não são recarregadas. Você precisa reiniciar o servidor antes que qualquer alteração nesses elementos se torne efetiva.

### Atualizando o arquivo de configuração do locatário {#section_71624DB8DF28480F84F34F0FF7FD4365}

Você pode modificar todos os valores especificados na variável [!DNL flashaccess-tenant.xml] arquivo a qualquer momento. As alterações entrarão em vigor na próxima vez que o servidor recarregar o arquivo de configuração. Além disso, o servidor verifica se há modificações em todas as credenciais ( [!DNL .pfx]) arquivos e arquivos de certificado de lista de permissões do empacotador referenciados no arquivo de configuração do locatário.
