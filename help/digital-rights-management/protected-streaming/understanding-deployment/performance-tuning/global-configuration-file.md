---
description: Este tópico descreve considerações relacionadas ao desempenho. Qualquer configuração no arquivo de configuração global chamada flashaccess-global.xml afeta o desempenho.
title: Arquivo de configuração global
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Ajuste de desempenho {#performance-tuning}

Este tópico descreve considerações relacionadas ao desempenho. Qualquer configuração no arquivo de configuração global chamada flashaccess-global.xml afeta o desempenho.

## Arquivo de configuração global {#global-configuration-file}

O arquivo de configuração inclui os seguintes elementos de configuração:

* `<Caching>` O  `<Caching>` elemento controla o armazenamento em cache dos arquivos de configuração na memória. O elemento `<Caching>` suporta a seguinte sintaxe:

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` Controla a frequência com que o servidor verifica se há atualizações nos arquivos de configuração. Um valor baixo para `refreshDelaySeconds` afeta negativamente o desempenho, enquanto um valor mais alto pode melhorar o desempenho.

   Consulte *Atualizando arquivos de configuração* para obter mais informações sobre `refreshDelaySeconds`.

* `numTenants` especifica o número de locatários. Um valor menor que o número de locatários afeta o desempenho, pois as solicitações aos locatários restantes resultam em erros de cache. Um erro de cache para quaisquer dados de configuração afeta negativamente o desempenho. Portanto, é recomendável definir esse valor mais alto do que o número de locatários configurados para o servidor, a menos que haja limitações de memória que você precise considerar.

* `<Logging>` O  `<Logging>` elemento especifica o nível de registro e a frequência com que os arquivos de log são rolados. O elemento `<Logging>` suporta a seguinte sintaxe:

   ```
   <Logging level="..." rollingFrequency="..."/>
   ```

* `<level>`  `level` especifica mensagens para um log. Um valor `DEBUG` gera muitas mensagens de log, o que pode afetar negativamente o desempenho. É recomendável aplicar uma configuração de `WARN` para obter o desempenho ideal. No entanto, esse valor pode resultar na perda de informações essenciais de tempo de execução, como auditorias de licenças. Se quiser salvar as informações do log com impacto mínimo no desempenho, é necessário aplicar um valor `INFO`.

* `<rollingFrequency>`  `rollingFrequency` especifica a frequência com que os arquivos de log são  *rolados*. *`Rolling`* é um processo que designa qualquer novo arquivo de log como um log ativo. Portanto, o arquivo de log ativo anteriormente não pode mais ser modificado e é considerado *`rolled`*. Você pode definir o intervalo acumulado como `MINUTELY`, `HOURLY`, `TWICE-DAILY`, `DAILY`, `WEEKLY`, `MONTHLY` ou `NEVER`.

Consulte *Using the Adobe Primetime DRM SDK for Protecting Content* para obter dicas sobre como otimizar o desempenho.