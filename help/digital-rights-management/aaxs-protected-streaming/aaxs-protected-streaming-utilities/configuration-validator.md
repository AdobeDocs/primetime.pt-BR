---
seo-title: Validador de configuração
title: Validador de configuração
uuid: 60ebd35c-290a-4f08-9bd0-178903857149
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# Validador de configuração {#configuration-validator}

O Adobe recomenda executar o utilitário Configuration Validator antes de iniciar o servidor sempre que forem feitas alterações no arquivo de configuração. Este utilitário pode detectar a maioria dos erros de configuração precocemente, antes de causar falhas durante o processamento da solicitação.

Para executar o validador, use o comando:

```
Validator.bat options  
```

ou o comando:

```
java -jar libs/flashaccess-validator.jar options 
```

Para cada um dos arquivos de configuração do servidor de licenças, o Validador pode executar a validação baseada em arquivo, o que garante que o arquivo XML esteja bem formado e esteja em conformidade com o schema do arquivo de configuração. Para executar a validação baseada em arquivo no arquivo de configuração global, execute o comando:

```
Validator --file path/flashaccess-global.xml --global
```

Para executar a validação baseada em arquivo no arquivo de configuração do locatário, execute o comando:

```
Validator --file path/flashaccess-tenant.xml --tenant
```

O Validador também pode executar a validação baseada na implantação; além de verificar a conformidade com o schema, este nível de validação também verifica se os valores especificados são válidos (por exemplo, garante a existência de arquivos referenciados). A validação baseada em implantação pode ser executada em dois níveis:

* Locatário — Valida o arquivo de configuração e as credenciais de um locatário específico. Para validar a configuração de &quot;locatário1&quot;, execute o comando:

```
Validator --root-path-to-LicenseServer.ConfigRoot -d flashaccessserver/tenant1 -t 
```

* Global — Valida o arquivo de configuração global e a validação do locatário para todos os locatários. Para executar a validação global baseada em implantação, execute o comando:

```
Validator --root-path-to-LicenseServer.ConfigRoot -g 
```

