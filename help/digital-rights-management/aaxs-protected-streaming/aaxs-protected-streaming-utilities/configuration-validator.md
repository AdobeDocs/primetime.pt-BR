---
title: Validador de configuração
description: Validador de configuração
copied-description: true
exl-id: 9b73e107-6ab7-4089-b415-0af8c9f86995
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# Validador de configuração {#configuration-validator}

O Adobe recomenda executar o utilitário Validador de configuração antes de iniciar o servidor sempre que alterações forem feitas no arquivo de configuração. Esse utilitário pode detectar a maioria dos erros de configuração antecipadamente, antes que eles causem falhas durante o processamento da solicitação.

Para executar o validador, use o comando:

```
Validator.bat options  
```

ou o comando:

```
java -jar libs/flashaccess-validator.jar options 
```

Para cada um dos arquivos de configuração do servidor de licenças, o Validador pode executar a validação baseada em arquivos, o que garante que o arquivo XML esteja bem formado e esteja em conformidade com o esquema do arquivo de configuração. Para executar a validação baseada em arquivo no arquivo de configuração global, execute o comando:

```
Validator --file path/flashaccess-global.xml --global
```

Para executar a validação baseada em arquivo no arquivo de configuração do locatário, execute o comando:

```
Validator --file path/flashaccess-tenant.xml --tenant
```

O Validador também pode executar a validação baseada em implantação. Além de verificar a conformidade com o esquema, esse nível de validação também verifica se os valores especificados são válidos (por exemplo, ele garante que os arquivos referenciados existam). A validação baseada em implantação pode ser executada em dois níveis:

* Locatário — Valida o arquivo de configuração e as credenciais de um locatário específico. Para validar a configuração de &quot;tenant1&quot;, execute o comando:

```
Validator --root-path-to-LicenseServer.ConfigRoot -d flashaccessserver/tenant1 -t 
```

* Global — Valida o arquivo de configuração global e a validação de todos os locatários. Para executar a validação baseada em implantação global, execute o comando:

```
Validator --root-path-to-LicenseServer.ConfigRoot -g 
```
