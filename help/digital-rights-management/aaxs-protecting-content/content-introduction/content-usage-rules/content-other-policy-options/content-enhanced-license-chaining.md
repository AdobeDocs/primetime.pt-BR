---
seo-title: Aumento do encadeamento de licenças
title: Aumento do encadeamento de licenças
uuid: d11b0631-5dfb-42b8-b7ba-cfeb1da488be
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237

---


# Aumento do encadeamento de licenças {#enhanced-license-chaining}

Permite que uma licença seja atualizada usando uma licença raiz pai para atualização em lote de licenças.

O Adobe Access 2.0 oferece suporte ao encadeamento de licenças no qual as licenças de folha e raiz estão vinculadas a uma máquina específica. O Adobe Access 3.0 tem suporte para encadeamento de licença aprimorado, no qual uma folha está vinculada a uma licença raiz, e somente a licença raiz está vinculada a uma máquina ou domínio específico. O encadeamento de licença aprimorado suporta a incorporação de licença de folha com o conteúdo, e o cliente só precisa adquirir a licença raiz do servidor de licença para consumir o conteúdo protegido.

Para ativar o encadeamento de licença aprimorado, uma chave de criptografia raiz é atribuída à política. A chave de criptografia raiz é usada para vincular criptograficamente a licença de folha à licença raiz.

>[!NOTE] {class=&quot;- tópico/observação &quot;}
>
>O encadeamento de licença aprimorado é suportado pelos clientes do Adobe Access versão 3.0 e superior. Se um cliente mais antigo solicitar uma licença para conteúdo compatível com o encadeamento de licença aprimorado, o servidor de licença ainda poderá emitir uma licença para esse cliente usando o encadeamento de licença suportado pelo Adobe Access 2.0.

Exemplo de caso de uso: Use esta opção para atualizar quaisquer licenças vinculadas baixando uma única licença raiz. Por exemplo, implemente modelos de assinatura nos quais o conteúdo pode ser reproduzido desde que o usuário renove a assinatura mensalmente. A vantagem dessa abordagem é que os usuários precisam apenas fazer uma única aquisição de licença para atualizar todas as licenças de assinatura.
