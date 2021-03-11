---
title: Criação de uma política usando a API do Java
description: Criação de uma política usando a API do Java
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Criação de uma política usando a API Java {#creating-a-policy-using-the-java-api}

Para criar uma política usando a API do Java, execute as seguintes etapas:

1. Configure seu ambiente de desenvolvimento e inclua todos os arquivos JAR mencionados em [Setting up the development environment](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) no seu projeto.
1. Crie um objeto `com.adobe.flashaccess.sdk.policy.Policy` e especifique suas propriedades, como direitos, duração do armazenamento em cache de licenças e data final da política.

   ```java
     // Create a new Policy object.  
     // False indicates the policy does not use license chaining.  
     Policy policy = new Policy(false);  
   
     policy.setName("DemoPolicy");  
   
     // Specify that the policy requires authentication to obtain a license.  
     policy.setLicenseServerInfo  
      (new LicenseServerInfo(AuthenticationType.UsernamePassword));  
   
     // A policy must have at least one Right, typically the play right  
     PlayRight play = new PlayRight();  
   
     // Users may only view content for 24 hours.  
     play.setPlaybackWindow(24L * 60 * 60);  
   
     // Add the play right to the policy.  
     List<Right> rightsList = new ArrayList<Right>();  
     rightsList.add(play);  
     policy.setRights(rightsList);  
   
     // Licenses may be stored on the client for 7 days after downloading  
     policy.setLicenseCachingDuration(7L * 24 * 60 * 60);  
     try {  
      // Content will expire December 31, 2010  
      SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");  
      policy.setPolicyEndDate(dateFormat.parse("2010-12-31"));  
     } catch (ParseException e) {  
      // Invalid date specified in dateFormat.parse()  
      e.printStackTrace();  
     }
   ```

1. Serialize o objeto `Policy` e o armazene em um arquivo ou banco de dados.

   ```java
     // Serialize the policy  
     byte[] policyBytes = policy.getBytes();  
     System.out.println("Created policy with ID: " + policy.getId());  
   
     // Write the policy to a file.   
     // Alternatively, the policy may be stored in a database.  
     FileOutputStream out = new FileOutputStream("demopolicy.pol");  
     out.write(policyBytes);  
     out.close();
   ```

Para obter a fonte completa desse código de amostra, consulte *com.adobe.flashaccess.samples.policy.CreatePolicy* no diretório Ferramentas de Linha de Comando de Implementação de Referência &quot;[!DNL samples]&quot;.
