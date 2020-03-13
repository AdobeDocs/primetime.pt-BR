---
seo-title: Atualização de uma política usando a API Java
title: Atualização de uma política usando a API Java
uuid: 23c50f05-799e-4f5a-869b-4b5e29a36ce1
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Atualização de uma política usando a API Java {#updating-a-policy-using-the-java-api}

Para atualizar uma política usando a API Java, execute as seguintes etapas:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em [Configurar o ambiente](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) de desenvolvimento dentro do projeto.
1. Crie uma `Policy` instância e leia a política a partir de um arquivo ou banco de dados.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. Atualize o `Policy` objeto definindo suas propriedades, como nome e regras de uso.

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

1. Serialize o `Policy` objeto atualizado e armazene-o em um arquivo ou banco de dados.

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

Para obter a fonte completa desse código de amostra, consulte `com.adobe.flashaccess.samples.policy.UpdatePolicy` o diretório &quot;samples&quot; das Ferramentas de Linha de Comando de Implementação de Referência.
