---
seo-title: Atualização de uma política DRM com a API Java
title: Atualização de uma política DRM com a API Java
uuid: ec21351c-900e-48f5-845a-c0b430c210d7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Atualização de uma política DRM com a API Java {#updating-a-drm-policy-with-the-java-api}

Para atualizar uma política de DRM com a API Java:

1. Configure seu ambiente de desenvolvimento e inclua no seu projeto todos os arquivos JAR listados em [Configurando o ambiente](../../protecting-content/setting-up-the-sdk/setup-dev-env.md)de desenvolvimento.
1. Crie uma `Policy` instância DRM e leia a política DRM de um arquivo ou banco de dados.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. Atualize o `Policy` objeto DRM definindo suas propriedades, como nome e regras de uso.

   ```java
   // Change the DRM policy name.  
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

1. Serialize o `Policy` objeto DRM atualizado e armazene-o em um arquivo ou banco de dados.

   ```java
   // Serialize the DRM policy.  
   byte[] policyBytes = policy.getBytes();  
   System.out.println("New DRM policy revision number: "  
       +  policy.getRevision());      
   // Write the DRM policy to a file.   
   // Alternatively, the DRM policy may be stored in a database.  
   FileOutputStream out = new FileOutputStream("demopolicy-updated.pol");  
   out.write(policyBytes);  
   out.close();
   ```

Consulte `com.adobe.flashaccess.samples.policy.UpdatePolicy` o diretório Ferramentas de Linha de Comando de Implementação de Referência [!DNL samples] para obter a origem desse código de amostra.
