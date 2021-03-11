---
description: 'O Adobe Access Server for Protected Streaming requer dois tipos de arquivos de configuração: um arquivo de configuração global (flashaccess-global.xml) e um arquivo de configuração de locatário para cada locatário (flashaccess-tenant.xml).'
title: Estrutura do Diretório de Configuração
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Arquivos de configuração do servidor de licenças e Estrutura do Diretório de Configuração {#configuration-directory-structure}

O Adobe Access Server for Protected Streaming requer dois tipos de arquivos de configuração: um arquivo de configuração global (flashaccess-global.xml) e um arquivo de configuração de locatário para cada locatário (flashaccess-tenant.xml).

Após editar os arquivos de configuração, o Adobe recomenda usar os utilitários fornecidos com o Adobe Access Server for Protected Streaming para verificar se os arquivos estão bem formados. Para obter mais informações, consulte &quot;[Validador de Configuração](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Para evitar disponibilizar senhas em texto claro nos arquivos de configuração, todas as senhas especificadas nos arquivos de configuração global e do locatário devem ser criptografadas. Para obter mais informações sobre criptografia de senhas, consulte &quot;[Scrambler de senha](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)&quot;.

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

