---
description: Os arquivos de log gerados pelo Adobe Primetime DRM Server para o aplicativo Protected Streaming estão localizados no diretório especificado por LicenseServer.LogRoot.
seo-description: Os arquivos de log gerados pelo Adobe Primetime DRM Server para o aplicativo Protected Streaming estão localizados no diretório especificado por LicenseServer.LogRoot.
seo-title: Arquivos de registro
title: Arquivos de registro
uuid: 4498fe60-65af-4f99-8f9b-e85013d0c9e9
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Arquivos de registro{#log-files}

Os arquivos de log gerados pelo Adobe Primetime DRM Server para o aplicativo Protected Streaming estão localizados no diretório especificado por LicenseServer.LogRoot.

>[!NOTE]
>
>Se os arquivos de log atuais forem excluídos ou movidos enquanto o servidor for executado, o arquivo de log talvez não seja recriado. Portanto, algumas informações de log podem ser excluídas.

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

O arquivo de log global, `flashaccess-global.log`, está localizado em *LicenseServer.LogRoot*. O log pode incluir mensagens de log que o Adobe Primetime DRM Java SDK ou as mensagens de log podem ter gerado durante o tempo em que o servidor foi inicializado.

## Arquivo de log de partição {#section_5660137CD6AA40519E72A4315534846B}

O arquivo de log de partição, `flashaccess-partition.log`, está localizado no `<LicenseServer.LogRoot>/flashaccesserver` diretório. Inclui mensagens de log que foram geradas durante o processamento de uma solicitação de licença.

## Arquivo de log do locatário {#section_F0257CC0831647F18A746B4F02E3E910}

O arquivo de log do locatário de cada locatário, `flashaccess-tenant.log`, está localizado em `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`. O log de locatário inclui informações de auditoria que descrevem cada licença gerada para este locatário.
