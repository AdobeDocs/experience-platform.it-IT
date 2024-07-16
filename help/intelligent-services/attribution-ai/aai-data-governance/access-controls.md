---
keywords: Experience Platform;home;argomenti popolari;controllo degli accessi;adobe admin console
solution: Experience Platform
feature: Attribution AI
title: Controllo dell’accesso per le Attribution AI
description: Questo documento fornisce informazioni sul controllo degli accessi basato su attributi per Attribution AI.
exl-id: 3ed672bf-1fa6-4893-99e0-afc2b2179543
source-git-commit: f28558d5939607cabf449cbc03b7e0f5406f6326
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---

# Controllo degli accessi in Attribution AI

Il controllo degli accessi per Attribution AI viene fornito tramite Adobe Experience Platform in [Adobe Admin Console](https://adminconsole.adobe.com/). Questa funzionalità sfrutta i profili di prodotto di Admin Console, che collegano gli utenti con autorizzazioni e sandbox.

Per ulteriori informazioni sul controllo degli accessi, vedere la [panoramica sul controllo degli accessi](../../../access-control/home.md).

## Controllo degli accessi basato su attributi

>[!IMPORTANT]
>
>Il controllo degli accessi basato su attributi è attualmente disponibile solo in una versione limitata.

[Il controllo dell&#39;accesso basato su attributi](../../../access-control/abac/overview.md) è una funzionalità di Adobe Experience Platform che consente agli amministratori di controllare l&#39;accesso a oggetti specifici e/o funzionalità basate su attributi. Gli attributi possono essere metadati aggiunti a un oggetto, ad esempio un’etichetta aggiunta a un campo o a un segmento dello schema. Un amministratore definisce i criteri di accesso che includono attributi per gestire le autorizzazioni di accesso degli utenti.

Questa funzionalità consente di etichettare i campi dello schema Experience Data Model (XDM) con etichette che definiscono gli ambiti di utilizzo organizzativi o dei dati. Parallelamente, gli amministratori possono utilizzare l’interfaccia di amministrazione di utenti e ruoli per definire i criteri di accesso relativi ai campi dello schema XDM e gestire in modo migliore l’accesso concesso a utenti o gruppi di utenti (utenti interni, esterni o di terze parti). Inoltre, il controllo dell’accesso basato su attributi consente agli amministratori di gestire l’accesso a segmenti specifici.

Tramite il controllo degli accessi basato su attributi, gli amministratori possono controllare l’accesso degli utenti sia ai dati personali sensibili (SPD) che alle informazioni personali (PII) in tutti i flussi di lavoro e le risorse di Platform. Gli amministratori possono definire ruoli utente con accesso solo a campi e dati specifici che corrispondono a tali campi.

A causa del controllo degli accessi basato su attributi, alcuni campi e funzionalità potrebbero avere accesso limitato e non essere disponibili per alcuni modelli di servizio Attribution AI. Alcuni esempi includono &quot;Identity&quot;, &quot;Score Definition&quot; e &quot;Clone&quot;.

Nella parte superiore dell&#39;area di lavoro di Attribution AI **pagina approfondimenti**, i dettagli visualizzati nella barra laterale hanno accesso limitato.

![Area di lavoro Attribution AI con i campi schema con restrizioni evidenziati.](../images/user-guide/access-restricted.png)

Se si selezionano i set di dati con schemi con restrizioni nella pagina **[!UICONTROL Crea flusso di lavoro modello]**, accanto al nome del set di dati viene visualizzato un messaggio di avviso con il seguente messaggio: [!UICONTROL Le informazioni con restrizioni sono escluse].

![Area di lavoro di Attribution AI con i campi del set di dati con restrizioni evidenziati.](../images/user-guide/restricted-info-excluded.png)

Quando si visualizzano in anteprima i set di dati con schema con restrizioni nella pagina **[!UICONTROL Crea flusso di lavoro modello]**, viene visualizzato un avviso che informa che [!UICONTROL A causa di restrizioni di accesso, alcune informazioni non vengono visualizzate nell&#39;anteprima del set di dati.]

![Area di lavoro Attribution AI con i risultati dei campi dello schema con anteprima limitata evidenziati.](../images/user-guide/restricted-dataset-preview.png)

Dopo aver creato un modello con informazioni limitate e aver proceduto al passaggio **[!UICONTROL Definisci obiettivo]**, nella parte superiore viene visualizzato un avviso: [!UICONTROL A causa di restrizioni di accesso, alcune informazioni non vengono visualizzate nella configurazione.]

![Area di lavoro Attribution AI con i campi limitati dei risultati del modello evidenziati.](../images/user-guide/information-not-displayed-save-and-exit.png)

## Passaggi successivi

La lettura di questa guida ti ha introdotto i principi fondamentali del controllo degli accessi in [!DNL Experience Platform]. È ora possibile passare alla [guida utente per il controllo degli accessi](../overview.md) per i passaggi dettagliati su come utilizzare [!DNL Admin Console] per creare profili di prodotto e assegnare autorizzazioni per [!DNL Platform].
