---
description: A Adobe recomenda que, se você fizer alterações no arquivo de configuração, execute o utilitário Validador de configurações antes de iniciar o servidor. Esse utilitário pode detectar a maioria dos erros de configuração antecipadamente, antes que eles causem falhas durante o processamento da solicitação.
title: Validador de configuração
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Validador de configuração{#configuration-validator}

A Adobe recomenda que, se você fizer alterações no arquivo de configuração, execute o utilitário Validador de configurações antes de iniciar o servidor. Esse utilitário pode detectar a maioria dos erros de configuração antecipadamente, antes que eles causem falhas durante o processamento da solicitação.

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

Para cada um dos arquivos de configuração do servidor de licenças, o Validador pode executar a validação baseada em arquivos, o que garante que o arquivo XML esteja bem formado e esteja em conformidade com o esquema do arquivo de configuração.

Para executar a validação baseada em arquivo no arquivo de configuração global, digite:

```
Validator --<file path>/flashaccess-global.xml --global
```

Para executar a validação baseada em arquivo no arquivo de configuração do locatário, digite:

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

O Validador também pode executar a validação baseada em implantação. Além de verificar a conformidade com o esquema, esse nível de validação também verifica se os valores especificados são válidos. Por exemplo, ela garante que os arquivos referenciados existam.

A validação baseada em implantação pode ser executada nos seguintes níveis:

* `Tenant` — Valida o arquivo de configuração e as credenciais para um locatário específico. Se desejar validar a configuração para `<tenant1>`, tipo:

  ```
      Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
  ```

* `Global` — Valida o arquivo de configuração global e a validação do locatário para todos os locatários. Se você deseja executar a validação baseada em implantação global, digite:

  ```
      Validator --<root-path-to-LicenseServer.ConfigRoot> -g
  ```
