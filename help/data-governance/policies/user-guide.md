---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida utente per i criteri di utilizzo dei dati
topic: policies
translation-type: tm+mt
source-git-commit: c4554e3fbc0dd527606b81e2767cb5777b6e81e7
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 1%

---


# Guida utente per i criteri di utilizzo dei dati

 Adobe Experience Platform Data Governance fornisce un&#39;interfaccia utente che consente di creare e gestire i criteri di utilizzo dei dati. Questo documento fornisce una panoramica delle azioni che è possibile eseguire nell&#39;area di lavoro _Criteri_ nell&#39;interfaccia utente di Experience Platform .

>[!IMPORTANT] Tutti i criteri di utilizzo dei dati (inclusi i criteri di base forniti da Adobe) sono disattivati per impostazione predefinita. Affinché un singolo criterio possa essere preso in considerazione per l&#39;applicazione, è necessario abilitare manualmente tale criterio. Per informazioni su come [abilitare i criteri](#enable) , consulta la sezione relativa all’attivazione dei criteri nell’interfaccia utente.

## Prerequisiti

Questa guida richiede una conoscenza approfondita dei seguenti concetti  Experience Platform:

- [Governance dei dati](../home.md)
- [Criteri di utilizzo dei dati](./overview.md)

## Visualizzare i criteri di utilizzo dei dati {#view-policies}

Nell’interfaccia  di Experience Platform, fate clic **[!UICONTROL Policies]** per aprire l’ *[!UICONTROL Policies]* area di lavoro. Nella **[!UICONTROL Browse]** scheda è possibile visualizzare un elenco dei criteri disponibili, incluse le etichette associate, le azioni di marketing e lo stato.

![](../images/policies/browse-policies.png)

Fate clic su un criterio elencato per visualizzarne la descrizione e il tipo. Se è selezionato un criterio personalizzato, vengono visualizzati controlli aggiuntivi per modificare, eliminare o [attivare/disattivare il criterio](#enable).

![](../images/policies/policy-details.png)

## Creazione di un criterio di utilizzo dati personalizzato {#create-policy}

Per creare un nuovo criterio di utilizzo dei dati personalizzato, fate clic **[!UICONTROL Create policy]** nell&#39;angolo superiore destro della **[!UICONTROL Browse]** scheda nell&#39;area di lavoro *Criteri* .

![](../images/policies/create-policy-button.png)

Viene *[!UICONTROL Create policy]* visualizzato il flusso di lavoro. Iniziate fornendo un nome e una descrizione per il nuovo criterio.

![](../images/policies/create-policy-description.png)

Quindi, selezionate le etichette di utilizzo dei dati su cui verrà basato il criterio. Quando si selezionano più etichette, è possibile scegliere se i dati devono contenere tutte le etichette o solo una di esse per poter applicare il criterio. Al termine fai clic su **[!UICONTROL Next]** (Continua).

![](../images/policies/add-labels.png)

Viene *[!UICONTROL Select marketing actions]* visualizzato il passaggio. Scegli le azioni di marketing appropriate dall&#39;elenco fornito, quindi fai clic **[!UICONTROL Next]** per continuare.

>[!NOTE] Quando si selezionano più azioni di marketing, il criterio le interpreta come una regola &quot;OR&quot;. In altre parole, il criterio si applica se viene eseguita _una_ delle azioni di marketing selezionate.

![](../images/policies/add-marketing-actions.png)

Viene visualizzato il *[!UICONTROL Review]* passaggio che consente di esaminare i dettagli del nuovo criterio prima di crearlo. Una volta soddisfatti, fate clic **[!UICONTROL Finish]** per creare il criterio.

![](../images/policies/policy-review.png)

La *[!UICONTROL Browse]* scheda viene visualizzata di nuovo, in cui ora viene visualizzato il criterio appena creato con lo stato &quot;Bozza&quot;. Per abilitare il criterio, vedere la sezione successiva.

![](../images/policies/created-policy.png)

## Attivare o disattivare un criterio di utilizzo dei dati {#enable}

Tutti i criteri di utilizzo dei dati (inclusi i criteri di base forniti da Adobe) sono disattivati per impostazione predefinita. Affinché un singolo criterio possa essere preso in considerazione per l&#39;implementazione, è necessario attivarlo manualmente tramite l&#39;API o l&#39;interfaccia utente.

Potete attivare o disattivare i criteri dalla *[!UICONTROL Browse]* scheda nell&#39; *[!UICONTROL Policies]* area di lavoro. Selezionate un criterio personalizzato dall&#39;elenco per visualizzarne i dettagli a destra. In *[!UICONTROL Status]* questa sezione, fate clic sul pulsante di attivazione per attivare o disattivare il criterio.

![](../images/policies/enable-policy.png)

## Visualizzazione delle azioni di marketing {#view-marketing-actions}

Nell&#39; **[!UICONTROL Policies]** area di lavoro, seleziona la **[!UICONTROL Marketing actions]** scheda per visualizzare un elenco delle azioni di marketing disponibili definite da Adobe e dalla tua organizzazione.

![](../images/policies/marketing-actions.png)

## Creazione di un&#39;azione di marketing {#create-marketing-action}

Per creare una nuova azione di marketing personalizzata, fai clic **[!UICONTROL Create marketing action]** nell&#39;angolo superiore destro della **[!UICONTROL Marketing actions]** scheda nell&#39;area di *[!UICONTROL Policies]* lavoro.

![](../images/policies/create-marketing-action.png)

Viene visualizzata *[!UICONTROL Create marketing action]* la finestra di dialogo. Immetti un nome e una descrizione per l&#39;azione di marketing, quindi fai clic su **[!UICONTROL Create]**.

![](../images/policies/create-marketing-action-details.png)

L’azione appena creata viene visualizzata nella *[!UICONTROL Marketing actions]* scheda. Ora puoi utilizzare l&#39;azione di marketing per [creare nuovi criteri](#create-policy)di utilizzo dei dati.

![](../images/policies/created-marketing-action.png)

## Modifica o eliminazione di un&#39;azione di marketing {#edit-delete-marketing-action}

>[!NOTE] È possibile modificare solo le azioni di marketing personalizzate definite dalla tua organizzazione. Le azioni di marketing definite da Adobe non possono essere modificate o eliminate.

Nell&#39; **[!UICONTROL Policies]** area di lavoro, seleziona la **[!UICONTROL Marketing actions]** scheda per visualizzare un elenco delle azioni di marketing disponibili definite da Adobe e dalla tua organizzazione. Seleziona un&#39;azione di marketing personalizzata dall&#39;elenco, quindi utilizza i campi forniti nella sezione di destra per modificare i dettagli dell&#39;azione di marketing.

![](../images/policies/edit-marketing-action.png)

Se l&#39;azione di marketing non è utilizzata da alcun criterio di utilizzo esistente, puoi eliminarla facendo clic su **[!UICONTROL Delete marketing action]**.

>[!NOTE] Se si tenta di eliminare un&#39;azione di marketing utilizzata da un criterio esistente, verrà visualizzato un messaggio di errore che indica che il tentativo di eliminazione non è riuscito.

![](../images/policies/delete-marketing-action.png)

## Passaggi successivi

In questo documento è stata fornita una panoramica su come gestire i criteri di utilizzo dei dati nell’interfaccia utente  Experience Platform. Per i passaggi su come gestire i criteri tramite l&#39;API DULE Policy, vedete la guida [](../api/getting-started.md)per gli sviluppatori. Per informazioni su come applicare i criteri di utilizzo dei dati, consultate la panoramica [sull&#39;applicazione dei](../enforcement/overview.md)criteri.

Il seguente video illustra come utilizzare i criteri di utilizzo nell’interfaccia utente  di Experience Platform:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)