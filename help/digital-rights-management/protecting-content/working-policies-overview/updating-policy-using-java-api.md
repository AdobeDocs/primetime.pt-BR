---
title: Atualização de uma política DRM com a API Java
description: Atualização de uma política DRM com a API Java
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# Atualização de uma política DRM com a API Java {#updating-a-drm-policy-with-the-java-api}

Para atualizar uma política DRM com a API do Java:

1. Configure seu ambiente de desenvolvimento e inclua em seu projeto todos os arquivos JAR listados em [Configuração do ambiente de desenvolvimento](../../protecting-content/setting-up-the-sdk/setup-dev-env.md).
1. Criar um DRM `Policy` e leia a política DRM de um arquivo ou banco de dados.

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. Atualizar o DRM `Policy` definindo suas propriedades, como nome e regras de uso.

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

1. Serializar o DRM atualizado `Policy` objeto e armazená-lo em um arquivo ou banco de dados.

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

Consulte `com.adobe.flashaccess.samples.policy.UpdatePolicy` nas Ferramentas de linha de comando da Implementação de referência [!DNL samples] diretório para a origem deste código de amostra.
