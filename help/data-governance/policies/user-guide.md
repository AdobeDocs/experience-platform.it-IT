---
keywords: Experience Platform;home;argomenti comuni;governance dei dati;guida utente per i criteri di utilizzo dei dati
solution: Experience Platform
title: Gestire i criteri di utilizzo dei dati nell’interfaccia utente
topic-legacy: policies
description: La governance dei dati di Adobe Experience Platform offre un’interfaccia utente che consente di creare e gestire i criteri di utilizzo dei dati. Questo documento fornisce una panoramica delle azioni che è possibile eseguire nell'area di lavoro Criteri nell'interfaccia utente di Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---

# Gestire i criteri di utilizzo dei dati nell’interfaccia utente

La governance dei dati di Adobe Experience Platform offre un’interfaccia utente che consente di creare e gestire i criteri di utilizzo dei dati. Questo documento fornisce una panoramica delle azioni che è possibile eseguire nel **Criteri** nell&#39;area di lavoro [!DNL Experience Platform] interfaccia utente.

>[!IMPORTANT]
>
>Per impostazione predefinita, tutti i criteri di utilizzo dei dati (inclusi i criteri principali forniti da Adobe) sono disabilitati. Affinché un singolo criterio possa essere preso in considerazione per l&#39;applicazione, è necessario abilitare manualmente tale criterio. Vedi la sezione su [attivazione dei criteri](#enable) per informazioni su come eseguire questa operazione nell’interfaccia utente di .

## Prerequisiti

Questa guida richiede una buona comprensione dei seguenti elementi [!DNL Experience Platform] concetti:

- [Governance dei dati](../home.md)
- [Criteri di utilizzo dei dati](./overview.md)

## Visualizza criteri esistenti {#view-policies}

In [!DNL Experience Platform] Interfaccia utente, seleziona **[!UICONTROL Criteri]** per aprire **[!UICONTROL Criteri]** workspace. In **[!UICONTROL Sfoglia]** puoi visualizzare un elenco dei criteri disponibili, incluse le etichette associate, le azioni di marketing e lo stato.

![](../images/policies/browse-policies.png)

Selezionare un criterio elencato per visualizzarne la descrizione e il tipo. Se è selezionato un criterio personalizzato, vengono visualizzati controlli aggiuntivi per modificare, eliminare o [attiva/disattiva il criterio](#enable).

![](../images/policies/policy-details.png)

## Creare un criterio personalizzato {#create-policy}

Per creare un nuovo criterio di utilizzo dati personalizzato, selezionare **[!UICONTROL Crea criterio]** nell&#39;angolo in alto a destra del **[!UICONTROL Sfoglia]** nella scheda **[!UICONTROL Criteri]** workspace.

![](../images/policies/create-policy-button.png)

La **[!UICONTROL Crea criterio]** viene visualizzato il flusso di lavoro . Per iniziare, fornisci un nome e una descrizione per il nuovo criterio.

![](../images/policies/create-policy-description.png)

Quindi, seleziona le etichette di utilizzo dei dati su cui verrà basato il criterio. Quando selezioni più etichette, ti viene data la possibilità di scegliere se i dati devono contenere tutte le etichette o solo una di esse per applicare il criterio. Seleziona **[!UICONTROL Successivo]** una volta finito.

![](../images/policies/add-labels.png)

La **[!UICONTROL Selezionare le azioni di marketing]** viene visualizzato il passaggio . Scegli le azioni di marketing appropriate dall’elenco fornito, quindi seleziona **[!UICONTROL Successivo]** per continuare.

>[!NOTE]
>
>Quando selezioni più azioni di marketing, il criterio le interpreta come una regola &quot;OR&quot;. In altre parole, la politica si applica se **qualsiasi** delle azioni di marketing selezionate vengono eseguite.

![](../images/policies/add-marketing-actions.png)

La **[!UICONTROL Revisione]** viene visualizzato un passaggio che consente di esaminare i dettagli del nuovo criterio prima di crearlo. Una volta effettuato il completamento, seleziona **[!UICONTROL Fine]** per creare il criterio.

![](../images/policies/policy-review.png)

La **[!UICONTROL Sfoglia]** viene visualizzata nuovamente la scheda , che ora elenca i criteri appena creati nello stato &quot;Bozza&quot;. Per abilitare il criterio, consulta la sezione successiva.

![](../images/policies/created-policy.png)

## Attivare o disattivare un criterio {#enable}

Per impostazione predefinita, tutti i criteri di utilizzo dei dati (inclusi i criteri principali forniti da Adobe) sono disabilitati. Affinché un singolo criterio possa essere preso in considerazione per l’implementazione, devi abilitare manualmente tale criterio tramite l’API o l’interfaccia utente.

Puoi abilitare o disabilitare i criteri dalla **[!UICONTROL Sfoglia]** nella scheda **[!UICONTROL Criteri]** workspace. Seleziona un criterio personalizzato dall’elenco per visualizzarne i dettagli a destra. Sotto **[!UICONTROL Stato]**, seleziona il pulsante di attivazione o disattivazione del criterio.

![](../images/policies/enable-policy.png)

## Visualizzare le azioni di marketing {#view-marketing-actions}

In **[!UICONTROL Criteri]** area di lavoro, seleziona **[!UICONTROL Azioni di marketing]** per visualizzare un elenco delle azioni di marketing disponibili definite da Adobe e dalla tua organizzazione.

![](../images/policies/marketing-actions.png)

## Creare un’azione di marketing {#create-marketing-action}

Per creare una nuova azione di marketing personalizzata, seleziona **[!UICONTROL Crea azione di marketing]** nell&#39;angolo in alto a destra del **[!UICONTROL Azioni di marketing]** nella scheda **[!UICONTROL Criteri]** workspace.

![](../images/policies/create-marketing-action.png)

La **[!UICONTROL Crea azione di marketing]** viene visualizzata la finestra di dialogo . Immetti un nome e una descrizione per l’azione di marketing, quindi seleziona **[!UICONTROL Crea]**.

![](../images/policies/create-marketing-action-details.png)

L’azione appena creata viene visualizzata nella **[!UICONTROL Azioni di marketing]** scheda . Ora puoi utilizzare l’azione di marketing quando [creazione di nuovi criteri di utilizzo dei dati](#create-policy).

![](../images/policies/created-marketing-action.png)

## Modificare o eliminare un’azione di marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>Puoi modificare solo le azioni di marketing personalizzate definite dalla tua organizzazione. Le azioni di marketing definite dall’Adobe non possono essere modificate o eliminate.

In **[!UICONTROL Criteri]** area di lavoro, seleziona **[!UICONTROL Azioni di marketing]** per visualizzare un elenco delle azioni di marketing disponibili definite da Adobe e dalla tua organizzazione. Seleziona un’azione di marketing personalizzata dall’elenco, quindi utilizza i campi forniti nella sezione di destra per modificare i dettagli dell’azione di marketing.

![](../images/policies/edit-marketing-action.png)

Se l’azione di marketing non è utilizzata da alcun criterio di utilizzo esistente, puoi eliminarla selezionando **[!UICONTROL Elimina azione di marketing]**.

>[!NOTE]
>
>Se si tenta di eliminare un&#39;azione di marketing utilizzata da un criterio esistente, viene visualizzato un messaggio di errore che indica che il tentativo di eliminazione non è riuscito.

![](../images/policies/delete-marketing-action.png)

## Passaggi successivi

Questo documento fornisce una panoramica sulla gestione dei criteri di utilizzo dei dati in [!DNL Experience Platform] Interfaccia utente. Per i passaggi su come gestire i criteri tramite la [!DNL Policy Service API], vedi [guida per sviluppatori](../api/getting-started.md). Per informazioni su come applicare i criteri di utilizzo dei dati, consulta [panoramica sull&#39;applicazione della politica](../enforcement/overview.md).

Il video seguente fornisce una dimostrazione di come utilizzare i criteri di utilizzo in [!DNL Experience Platform] Interfaccia utente:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
