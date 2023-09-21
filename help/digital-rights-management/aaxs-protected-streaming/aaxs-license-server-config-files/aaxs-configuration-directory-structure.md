---
description: 'O Adobe Access Server para transmissão protegida requer dois tipos de arquivos de configuração: um arquivo de configuração global (flashaccess-global.xml) e um arquivo de configuração de locatário para cada locatário (flashaccess-tenant.xml).'
title: Estrutura do diretório de configuração
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# Arquivos de configuração do servidor de licenças e estrutura do diretório de configuração {#configuration-directory-structure}

O Adobe Access Server para transmissão protegida requer dois tipos de arquivos de configuração: um arquivo de configuração global (flashaccess-global.xml) e um arquivo de configuração de locatário para cada locatário (flashaccess-tenant.xml).

Após editar os arquivos de configuração, o Adobe recomenda usar os utilitários fornecidos com o Adobe Access Server para transmissão protegida para verificar se os arquivos estão bem formados. Para obter mais informações, consulte &quot;[Validador de configuração](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Para evitar a disponibilização de senhas em texto não criptografado nos arquivos de configuração, todas as senhas especificadas nos arquivos de configuração global e de locatário devem ser criptografadas. Para obter mais informações sobre como criptografar senhas, consulte &quot;[Scrambler de senhas](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)&quot;.

Os diretórios de configuração têm a seguinte estrutura:

```
<i class="+ topic ph hi-d="" i "="">
  LicenseServer.ConfigRoot/  
  flashaccess-global.xml  
  pkcs11.cfg (optional)  
  flashaccessserver/  
   libs/ (optional)  
   tenants/  
     
 <i class="+ topic ph hi-d="" i "="">
   tenantname/  
      flashaccess-tenant.xml  
       
  <i class="+ topic ph hi-d="" i "="">
    credential.pfx (optional)  
        
   <i class="+ topic ph hi-d="" i "="">
     packagercert.cer (optional) 
   </i class="+ topic> 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```
