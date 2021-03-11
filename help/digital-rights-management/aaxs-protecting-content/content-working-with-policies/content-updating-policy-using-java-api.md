---
title: Atualização de uma política usando a API do Java
description: Atualização de uma política usando a API do Java
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Atualização de uma política usando a API Java {#updating-a-policy-using-the-java-api}

Para atualizar uma política usando a API do Java, execute as seguintes etapas:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em [Setting up the development environment](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) no seu projeto.
1. Crie uma instância `Policy` e leia a política a partir de um arquivo ou banco de dados.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. Atualize o objeto `Policy` definindo suas propriedades, como nome e regras de uso.

   ```java
     // Change the policy name.  
     policy.setName("UpdatedDemoPolicy");  
   
     // Add DRM module restrictions to the play right  
     for (Right r: policy.getRights()) {  
      if (r instanceof PlayRight) {  
       PlayRight pr = (PlayRight) r;  
       // Disallow Linux versions up to and including 1.9.  Allow  
       // all other OSes and Linux versions above 1.9  
       VersionInfo toExclude = new VersionInfo();  
       toExclude.setOS("Linux");  
       toExclude.setReleaseVersion("1.9");  
       Collection<VersionInfo> exclusions = new ArrayList<VersionInfo>();  
       exclusions.add(toExclude);  
       ModuleRequirements drmRestrictions = new ModuleRequirements();  
       drmRestrictions.setExcludedVersions(exclusions);  
       pr.setDRMModuleRequirements(drmRestrictions);  
       break;  
      }  
     }
   ```

1. Serialize o objeto `Policy` atualizado e armazene-o em um arquivo ou banco de dados.

   ```java
      // Serialize the policy.  
      byte[] policyBytes = policy.getBytes();  
      System.out.println("New policy revision number: "  
       +  policy.getRevision());      
      // Write the policy to a file.   
      // Alternatively, the policy may be stored in a database.  
      FileOutputStream out = new FileOutputStream("demopolicy-updated.pol");  
      out.write(policyBytes);  
      out.close(); 
   ```

Para obter a fonte completa deste código de amostra, consulte `com.adobe.flashaccess.samples.policy.UpdatePolicy` no diretório &quot;samples&quot; de Ferramentas de Linha de Comando de Implementação de Referência.
