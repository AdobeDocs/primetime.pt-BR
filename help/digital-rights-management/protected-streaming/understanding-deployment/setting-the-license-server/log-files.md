---
description: Os arquivos de log gerados pelo aplicativo Adobe Primetime DRM Server for Protected Streaming estão localizados no diretório especificado por LicenseServer.LogRoot.
title: Arquivos de log
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Arquivos de log{#log-files}

Os arquivos de log gerados pelo aplicativo Adobe Primetime DRM Server for Protected Streaming estão localizados no diretório especificado por LicenseServer.LogRoot.

>[!NOTE]
>
>Se os arquivos de log atuais forem excluídos ou movidos enquanto o servidor é executado, o arquivo de log pode não ser recriado. Portanto, algumas informações de log podem ser excluídas.

## Estrutura do diretório de log {#section_F490A483D60145ADBC21038914C39203}

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

## Arquivo de log global {#section_1CFA90748142439C9F3BE380969539DA}

O arquivo de log global, `flashaccess-global.log`, está localizado em *LicenseServer.LogRoot*. O log pode incluir mensagens de log que o Adobe Primetime DRM Java SDK ou mensagens de log podem ter gerado durante o tempo em que o servidor foi inicializado.

## Arquivo de log de partição {#section_5660137CD6AA40519E72A4315534846B}

O arquivo de log da partição, `flashaccess-partition.log`, está localizado no diretório `<LicenseServer.LogRoot>/flashaccesserver`. Ele inclui mensagens de log que foram geradas durante o processamento de uma solicitação de licença.

## Arquivo de log do locatário {#section_F0257CC0831647F18A746B4F02E3E910}

O arquivo de log do locatário de cada locatário, `flashaccess-tenant.log`, está localizado em `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`. O log de locatários inclui informações de auditoria que descrevem cada licença gerada para este locatário.
