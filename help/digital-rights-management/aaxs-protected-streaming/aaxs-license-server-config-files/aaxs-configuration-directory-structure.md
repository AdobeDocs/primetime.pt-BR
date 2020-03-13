---
description: 'O Adobe Access Server for Protected Streaming requer dois tipos de arquivos de configuração: um arquivo de configuração global (flashaccess-global.xml) e um arquivo de configuração de locatário para cada locatário (flashaccess-locatário.xml).'
seo-description: 'O Adobe Access Server for Protected Streaming requer dois tipos de arquivos de configuração: um arquivo de configuração global (flashaccess-global.xml) e um arquivo de configuração de locatário para cada locatário (flashaccess-locatário.xml).'
seo-title: Estrutura do Diretório de Configuração
title: Estrutura do Diretório de Configuração
uuid: c6cfc734-6b7c-4502-9bdb-c7aaca156e0e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Arquivos de configuração do servidor de licenças e Estrutura do Diretório de Configuração {#configuration-directory-structure}

O Adobe Access Server for Protected Streaming requer dois tipos de arquivos de configuração: um arquivo de configuração global (flashaccess-global.xml) e um arquivo de configuração de locatário para cada locatário (flashaccess-locatário.xml).

Após editar os arquivos de configuração, a Adobe recomenda usar os utilitários fornecidos com o Adobe Access Server for Protected Streaming para verificar se os arquivos estão bem formados. Para obter mais informações, consulte &quot;Validador[de configuração](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)&quot;.

Para evitar disponibilizar senhas em texto nítido nos arquivos de configuração, todas as senhas especificadas nos arquivos de configuração global e locatário devem ser criptografadas. Para obter mais informações sobre como criptografar senhas, consulte &quot;[Scrambler](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)&quot;.

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

