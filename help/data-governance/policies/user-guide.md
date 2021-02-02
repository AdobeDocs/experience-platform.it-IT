---
keywords: ' Experience Platform;home;argomenti più comuni;gestione dei dati;guida utente per l''utilizzo dei dati'
solution: Experience Platform
title: Guida utente per i criteri di utilizzo dei dati
topic: policies
description: Adobe Experience Platform Data Governance fornisce un'interfaccia utente che consente di creare e gestire i criteri di utilizzo dei dati. Questo documento fornisce una panoramica delle azioni che potete eseguire nell'area di lavoro Criteri dell'interfaccia utente del Experience Platform .
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---


# Guida utente per i criteri di utilizzo dei dati

Adobe Experience Platform [!DNL Data Governance] fornisce un&#39;interfaccia utente che consente di creare e gestire i criteri di utilizzo dei dati. Questo documento fornisce una panoramica delle azioni che è possibile eseguire nell&#39;area di lavoro **Criteri** nell&#39;interfaccia utente [!DNL Experience Platform].

>[!IMPORTANT]
>
>Tutti i criteri di utilizzo dei dati (inclusi i criteri di base forniti dal Adobe ) sono disattivati per impostazione predefinita. Affinché un singolo criterio possa essere preso in considerazione per l&#39;applicazione, è necessario abilitare manualmente tale criterio. Per informazioni su come eseguire questa operazione nell&#39;interfaccia utente, vedere la sezione relativa all&#39; [attivazione dei criteri](#enable).

## Prerequisiti

Questa guida richiede una conoscenza approfondita dei seguenti concetti di [!DNL Experience Platform]:

- [[!DNL Data Governance]](../home.md)
- [Criteri di utilizzo dei dati](./overview.md)

## Visualizza criteri di utilizzo dei dati {#view-policies}

Nell&#39;interfaccia di [!DNL Experience Platform], selezionare **[!UICONTROL Policies]** per aprire l&#39;area di lavoro **[!UICONTROL Policies]**. Nella scheda **[!UICONTROL Browse]** è possibile visualizzare un elenco dei criteri disponibili, incluse le etichette associate, le azioni di marketing e lo stato.

![](../images/policies/browse-policies.png)

Selezionate un criterio elencato per visualizzarne la descrizione e il tipo. Se è selezionato un criterio personalizzato, vengono visualizzati controlli aggiuntivi per modificare, eliminare o [abilitare/disabilitare il criterio](#enable).

![](../images/policies/policy-details.png)

## Creare un criterio di utilizzo dei dati personalizzato {#create-policy}

Per creare un nuovo criterio di utilizzo dei dati personalizzato, selezionare **[!UICONTROL Create policy]** nell&#39;angolo superiore destro della scheda **[!UICONTROL Browse]** nell&#39;area di lavoro **[!UICONTROL Policies]**.

![](../images/policies/create-policy-button.png)

Viene visualizzato il flusso di lavoro **[!UICONTROL Create policy]**. Iniziate fornendo un nome e una descrizione per il nuovo criterio.

![](../images/policies/create-policy-description.png)

Quindi, selezionate le etichette di utilizzo dei dati su cui verrà basato il criterio. Quando si selezionano più etichette, è possibile scegliere se i dati devono contenere tutte le etichette o solo una di esse per poter applicare il criterio. Al termine, fai clic su **[!UICONTROL Next]**.

![](../images/policies/add-labels.png)

Viene visualizzato il passaggio **[!UICONTROL Select marketing actions]**. Scegli le azioni di marketing appropriate dall&#39;elenco fornito, quindi seleziona **[!UICONTROL Next]** per continuare.

>[!NOTE]
>
>Quando si selezionano più azioni di marketing, il criterio le interpreta come una regola &quot;OR&quot;. In altre parole, il criterio si applica se vengono eseguite **qualsiasi** delle azioni di marketing selezionate.

![](../images/policies/add-marketing-actions.png)

Viene visualizzato il passaggio **[!UICONTROL Review]**, che consente di esaminare i dettagli del nuovo criterio prima di crearlo. Una volta soddisfatti, selezionate **[!UICONTROL Finish]** per creare il criterio.

![](../images/policies/policy-review.png)

Viene nuovamente visualizzata la scheda **[!UICONTROL Browse]**, che ora elenca il criterio appena creato in stato &quot;Bozza&quot;. Per abilitare il criterio, vedere la sezione successiva.

![](../images/policies/created-policy.png)

## Abilita o disabilita un criterio di utilizzo dei dati {#enable}

Tutti i criteri di utilizzo dei dati (inclusi i criteri di base forniti dal Adobe ) sono disattivati per impostazione predefinita. Affinché un singolo criterio venga preso in considerazione per l&#39;implementazione, è necessario attivarlo manualmente tramite l&#39;API o l&#39;interfaccia utente.

È possibile abilitare o disabilitare i criteri dalla scheda **[!UICONTROL Browse]** nell&#39;area di lavoro **[!UICONTROL Policies]**. Selezionate un criterio personalizzato dall&#39;elenco per visualizzarne i dettagli a destra. In **[!UICONTROL Status]**, selezionate il pulsante di attivazione per attivare o disattivare il criterio.

![](../images/policies/enable-policy.png)

## Visualizza azioni di marketing {#view-marketing-actions}

Nell&#39;area di lavoro **[!UICONTROL Policies]**, seleziona la scheda **[!UICONTROL Marketing actions]** per visualizzare un elenco delle azioni di marketing disponibili definite dal Adobe  e dalla tua organizzazione.

![](../images/policies/marketing-actions.png)

## Creare un&#39;azione di marketing {#create-marketing-action}

Per creare una nuova azione di marketing personalizzata, selezionate **[!UICONTROL Create marketing action]** nell&#39;angolo superiore destro della scheda **[!UICONTROL Marketing actions]** nell&#39;area di lavoro **[!UICONTROL Policies]**.

![](../images/policies/create-marketing-action.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Create marketing action]**. Immetti un nome e una descrizione per l&#39;azione di marketing, quindi seleziona **[!UICONTROL Create]**.

![](../images/policies/create-marketing-action-details.png)

L&#39;azione appena creata viene visualizzata nella scheda **[!UICONTROL Marketing actions]**. Ora puoi utilizzare l&#39;azione di marketing quando [crei nuovi criteri di utilizzo dei dati](#create-policy).

![](../images/policies/created-marketing-action.png)

## Modifica o eliminazione di un&#39;azione di marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>È possibile modificare solo le azioni di marketing personalizzate definite dalla tua organizzazione. Le azioni di marketing definite da  Adobe non possono essere modificate o eliminate.

Nell&#39;area di lavoro **[!UICONTROL Policies]**, seleziona la scheda **[!UICONTROL Marketing actions]** per visualizzare un elenco delle azioni di marketing disponibili definite dal Adobe  e dalla tua organizzazione. Seleziona un&#39;azione di marketing personalizzata dall&#39;elenco, quindi utilizza i campi forniti nella sezione di destra per modificare i dettagli dell&#39;azione di marketing.

![](../images/policies/edit-marketing-action.png)

Se l&#39;azione di marketing non è utilizzata da alcun criterio di utilizzo esistente, puoi eliminarla selezionando **[!UICONTROL Delete marketing action]**.

>[!NOTE]
>
>Se si tenta di eliminare un&#39;azione di marketing utilizzata da un criterio esistente, verrà visualizzato un messaggio di errore che indica che il tentativo di eliminazione non è riuscito.

![](../images/policies/delete-marketing-action.png)

## Passaggi successivi

Questo documento fornisce una panoramica su come gestire i criteri di utilizzo dei dati nell&#39;interfaccia utente di [!DNL Experience Platform]. Per istruzioni su come gestire i criteri utilizzando [!DNL Policy Service API], vedere la [guida per gli sviluppatori](../api/getting-started.md). Per informazioni su come applicare i criteri di utilizzo dei dati, vedere la [panoramica sull&#39;applicazione dei criteri](../enforcement/overview.md).

Il seguente video illustra come utilizzare i criteri di utilizzo nell&#39;interfaccia utente di [!DNL Experience Platform]:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)