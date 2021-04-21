---
keywords: Experience Platform;home;argomenti comuni;governance dei dati;guida utente per i criteri di utilizzo dei dati
solution: Experience Platform
title: Gestire i criteri di utilizzo dei dati nell’interfaccia utente
topic-legacy: policies
description: La governance dei dati di Adobe Experience Platform offre un’interfaccia utente che consente di creare e gestire i criteri di utilizzo dei dati. Questo documento fornisce una panoramica delle azioni che è possibile eseguire nell'area di lavoro Criteri nell'interfaccia utente di Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 0%

---

# Gestire i criteri di utilizzo dei dati nell’interfaccia utente

Adobe Experience Platform [!DNL Data Governance] fornisce un&#39;interfaccia utente che consente di creare e gestire i criteri di utilizzo dei dati. Questo documento fornisce una panoramica delle azioni eseguibili nell&#39;area di lavoro **Criteri** nell&#39;interfaccia utente [!DNL Experience Platform].

>[!IMPORTANT]
>
>Per impostazione predefinita, tutti i criteri di utilizzo dei dati (inclusi i criteri principali forniti da Adobe) sono disabilitati. Affinché un singolo criterio possa essere preso in considerazione per l&#39;applicazione, è necessario abilitare manualmente tale criterio. Per informazioni su come eseguire questa operazione nell’interfaccia utente, consulta la sezione relativa all’ [abilitazione dei criteri](#enable) .

## Prerequisiti

Questa guida richiede una comprensione pratica dei seguenti concetti [!DNL Experience Platform]:

- [[!DNL Data Governance]](../home.md)
- [Criteri di utilizzo dei dati](./overview.md)

## Visualizza criteri esistenti {#view-policies}

Nell’interfaccia utente [!DNL Experience Platform], seleziona **[!UICONTROL Policies]** per aprire l’area di lavoro **[!UICONTROL Policies]**. Nella scheda **[!UICONTROL Browse]** puoi visualizzare un elenco dei criteri disponibili, incluse le etichette associate, le azioni di marketing e lo stato.

![](../images/policies/browse-policies.png)

Selezionare un criterio elencato per visualizzarne la descrizione e il tipo. Se è selezionato un criterio personalizzato, vengono visualizzati controlli aggiuntivi per modificare, eliminare o [abilitare/disabilitare il criterio](#enable).

![](../images/policies/policy-details.png)

## Creare un criterio personalizzato {#create-policy}

Per creare un nuovo criterio di utilizzo dei dati personalizzato, seleziona **[!UICONTROL Create policy]** nell’angolo in alto a destra della scheda **[!UICONTROL Browse]** nell’area di lavoro **[!UICONTROL Policies]**.

![](../images/policies/create-policy-button.png)

Viene visualizzato il flusso di lavoro **[!UICONTROL Create policy]** . Per iniziare, fornisci un nome e una descrizione per il nuovo criterio.

![](../images/policies/create-policy-description.png)

Quindi, seleziona le etichette di utilizzo dei dati su cui verrà basato il criterio. Quando selezioni più etichette, ti viene data la possibilità di scegliere se i dati devono contenere tutte le etichette o solo una di esse per applicare il criterio. Al termine, fai clic su **[!UICONTROL Next]**.

![](../images/policies/add-labels.png)

Viene visualizzato il passaggio **[!UICONTROL Select marketing actions]** . Scegli le azioni di marketing appropriate dall’elenco fornito, quindi seleziona **[!UICONTROL Next]** per continuare.

>[!NOTE]
>
>Quando selezioni più azioni di marketing, il criterio le interpreta come una regola &quot;OR&quot;. In altre parole, il criterio si applica se viene eseguito **qualsiasi** delle azioni di marketing selezionate.

![](../images/policies/add-marketing-actions.png)

Viene visualizzato il passaggio **[!UICONTROL Review]** , che consente di esaminare i dettagli del nuovo criterio prima di crearlo. Una volta soddisfatti, seleziona **[!UICONTROL Finish]** per creare il criterio.

![](../images/policies/policy-review.png)

Viene visualizzata nuovamente la scheda **[!UICONTROL Browse]**, che elenca i criteri appena creati nello stato &quot;Bozza&quot;. Per abilitare il criterio, consulta la sezione successiva.

![](../images/policies/created-policy.png)

## Attivare o disattivare un criterio {#enable}

Per impostazione predefinita, tutti i criteri di utilizzo dei dati (inclusi i criteri principali forniti da Adobe) sono disabilitati. Affinché un singolo criterio possa essere preso in considerazione per l’implementazione, devi abilitare manualmente tale criterio tramite l’API o l’interfaccia utente.

È possibile abilitare o disabilitare i criteri dalla scheda **[!UICONTROL Browse]** nell&#39;area di lavoro **[!UICONTROL Policies]**. Seleziona un criterio personalizzato dall’elenco per visualizzarne i dettagli a destra. In **[!UICONTROL Status]**, seleziona il pulsante di attivazione/disattivazione per abilitare o disabilitare il criterio.

![](../images/policies/enable-policy.png)

## Visualizzare le azioni di marketing {#view-marketing-actions}

Nell’area di lavoro **[!UICONTROL Policies]**, seleziona la scheda **[!UICONTROL Marketing actions]** per visualizzare un elenco delle azioni di marketing disponibili definite da Adobe e dalla tua organizzazione.

![](../images/policies/marketing-actions.png)

## Creare un’azione di marketing {#create-marketing-action}

Per creare una nuova azione di marketing personalizzata, seleziona **[!UICONTROL Create marketing action]** nell’angolo in alto a destra della scheda **[!UICONTROL Marketing actions]** nell’area di lavoro **[!UICONTROL Policies]**.

![](../images/policies/create-marketing-action.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Create marketing action]**. Immetti un nome e una descrizione per l’azione di marketing, quindi seleziona **[!UICONTROL Create]**.

![](../images/policies/create-marketing-action-details.png)

L’azione appena creata viene visualizzata nella scheda **[!UICONTROL Marketing actions]** . È ora possibile utilizzare l&#39;azione di marketing durante la creazione di nuovi criteri di utilizzo dei dati ](#create-policy).[

![](../images/policies/created-marketing-action.png)

## Modificare o eliminare un’azione di marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>Puoi modificare solo le azioni di marketing personalizzate definite dalla tua organizzazione. Le azioni di marketing definite dall’Adobe non possono essere modificate o eliminate.

Nell’area di lavoro **[!UICONTROL Policies]**, seleziona la scheda **[!UICONTROL Marketing actions]** per visualizzare un elenco delle azioni di marketing disponibili definite da Adobe e dalla tua organizzazione. Seleziona un’azione di marketing personalizzata dall’elenco, quindi utilizza i campi forniti nella sezione di destra per modificare i dettagli dell’azione di marketing.

![](../images/policies/edit-marketing-action.png)

Se l’azione di marketing non è utilizzata da alcun criterio di utilizzo esistente, puoi eliminarla selezionando **[!UICONTROL Delete marketing action]**.

>[!NOTE]
>
>Se si tenta di eliminare un&#39;azione di marketing utilizzata da un criterio esistente, viene visualizzato un messaggio di errore che indica che il tentativo di eliminazione non è riuscito.

![](../images/policies/delete-marketing-action.png)

## Passaggi successivi

Questo documento fornisce una panoramica sulla gestione dei criteri di utilizzo dei dati nell’ interfaccia utente di [!DNL Experience Platform] . Per i passaggi su come gestire i criteri utilizzando [!DNL Policy Service API], consulta la [guida per gli sviluppatori](../api/getting-started.md). Per informazioni su come applicare i criteri di utilizzo dei dati, vedere la [panoramica sull&#39;applicazione dei criteri](../enforcement/overview.md).

Il video seguente illustra come utilizzare i criteri di utilizzo nell’ interfaccia utente [!DNL Experience Platform] :

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
