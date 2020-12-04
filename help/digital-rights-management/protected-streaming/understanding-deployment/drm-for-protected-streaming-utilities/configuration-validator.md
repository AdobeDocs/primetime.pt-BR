---
description: A Adobe recomenda que, se você fizer alterações no arquivo de configuração, execute o utilitário Configuration Validator antes de start do servidor. Este utilitário pode detectar a maioria dos erros de configuração precocemente, antes de causar falhas durante o processamento da solicitação.
seo-description: A Adobe recomenda que, se você fizer alterações no arquivo de configuração, execute o utilitário Configuration Validator antes de start do servidor. Este utilitário pode detectar a maioria dos erros de configuração precocemente, antes de causar falhas durante o processamento da solicitação.
seo-title: Validador de configuração
title: Validador de configuração
uuid: 7b44919a-0319-4675-95e2-ad1ad72ec0cb
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# Validador de configuração{#configuration-validator}

A Adobe recomenda que, se você fizer alterações no arquivo de configuração, execute o utilitário Configuration Validator antes de start do servidor. Este utilitário pode detectar a maioria dos erros de configuração precocemente, antes de causar falhas durante o processamento da solicitação.

Para executar o validador, digite:

```
Validator.bat  
<i class="+ topic ph hi-d="" i "="">
  options  
</i class="+ topic>
```

ou

```
java -jar libs/flashaccess-validator.jar  
<i class="+ topic ph hi-d="" i "="">
  options 
</i class="+ topic>
```

Para cada um dos arquivos de configuração do servidor de licenças, o Validador pode executar a validação baseada em arquivo, garantindo que o arquivo XML esteja bem formado e esteja em conformidade com o schema do arquivo de configuração.

Para executar a validação baseada em arquivo no arquivo de configuração global, digite:

```
Validator --<file path>/flashaccess-global.xml --global
```

Para executar a validação baseada em arquivo no arquivo de configuração do locatário, digite:

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

O Validador também pode executar a validação baseada em implantação. Além de verificar a conformidade com o schema, esse nível de validação também verifica se os valores especificados são válidos. Por exemplo, garante que os arquivos referenciados existam.

A validação baseada na implantação pode ser executada nos seguintes níveis:

* `Tenant` — Valida o arquivo de configuração e as credenciais de um locatário específico. Se desejar validar a configuração para `<tenant1>`, digite:

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
   ```

* `Global` — Valida o arquivo de configuração global e a validação do locatário para todos os locatários. Se desejar executar a validação global baseada em implantação, digite:

   ```
       Validator --<root-path-to-LicenseServer.ConfigRoot> -g
   ```

