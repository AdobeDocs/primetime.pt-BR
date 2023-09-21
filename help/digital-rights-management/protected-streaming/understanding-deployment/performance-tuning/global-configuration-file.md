---
description: Este tópico descreve as considerações relacionadas ao desempenho. Quaisquer configurações no arquivo de configuração global chamado flashaccess-global.xml afetam o desempenho.
title: Arquivo de configuração global
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Ajuste de desempenho {#performance-tuning}

Este tópico descreve as considerações relacionadas ao desempenho. Quaisquer configurações no arquivo de configuração global chamado flashaccess-global.xml afetam o desempenho.

## Arquivo de configuração global {#global-configuration-file}

O arquivo de configuração inclui os seguintes elementos de configurações:

* `<Caching>` A variável `<Caching>` os controles de elemento armazenam arquivos de configuração em cache na memória. A variável `<Caching>` O elemento suporta a seguinte sintaxe:

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` Controla a frequência com que o servidor verifica se há atualizações para os arquivos de configuração. Um valor baixo para `refreshDelaySeconds` afeta negativamente o desempenho, enquanto um valor mais alto pode melhorar o desempenho.

  Consulte *Atualização de arquivos de configuração* para obter mais informações sobre `refreshDelaySeconds`.

* `numTenants` especifica o número de locatários. Um valor menor que o número de locatários afeta o desempenho porque as solicitações aos locatários restantes resultam em erros de cache. Um erro de cache para qualquer dado de configuração afeta negativamente o desempenho. Portanto, é recomendável definir esse valor como um número maior do que o número de locatários configurados para o servidor, a menos que haja limitações de memória que você precise considerar.

* `<Logging>` A variável `<Logging>` elemento especifica o nível de log e a frequência com que os arquivos de log são rolados. A variável `<Logging>` O elemento suporta a seguinte sintaxe:

  ```
  <Logging level="..." rollingFrequency="..."/>
  ```

* `<level>`  `level` especifica mensagens para um log. Um valor de `DEBUG` O gera muitas mensagens de log, o que pode afetar negativamente o desempenho. É recomendável aplicar uma configuração de `WARN` para obter o desempenho ideal. No entanto, esse valor pode resultar na perda de informações essenciais de tempo de execução, como auditorias de licença. Para salvar informações de registro com impacto mínimo no desempenho, é necessário aplicar um valor de `INFO`.

* `<rollingFrequency>`  `rollingFrequency` especifica a frequência com que os arquivos de log são *rolados*. *`Rolling`* é um processo que designa qualquer novo arquivo de log como um log ativo. Portanto, o arquivo de log ativo anteriormente não pode mais ser modificado e é considerado *`rolled`*. Você pode definir o intervalo de rolagem como `MINUTELY`, `HOURLY`, `TWICE-DAILY`, `DAILY`, `WEEKLY`, `MONTHLY`ou `NEVER`.

Consulte *Utilização do SDK do Adobe Primetime DRM para proteção de conteúdo* para obter dicas sobre como otimizar o desempenho.
