---
keywords: Experience Platform;guida utente;ia clienti;argomenti popolari;controlli di accesso;creare un modello;
solution: Experience Platform
feature: Customer AI
title: Controllo dell’accesso per IA per l’analisi dei clienti
description: Questo documento fornisce informazioni sul controllo degli accessi basato su attributi per IA per l’analisi dei clienti.
exl-id: 02e3b6a4-304a-4ac4-b07c-010531101feb
source-git-commit: f28558d5939607cabf449cbc03b7e0f5406f6326
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---

# Controllo dell’accesso basato su attributi in Customer AI

>[!IMPORTANT]
>
>Il controllo degli accessi basato su attributi è attualmente disponibile solo in una versione limitata.

[Il controllo dell&#39;accesso basato su attributi](../../../access-control/abac/overview.md) è una funzionalità di Adobe Experience Platform che consente agli amministratori di controllare l&#39;accesso a oggetti specifici e/o funzionalità basate su attributi. Gli attributi possono essere metadati aggiunti a un oggetto, ad esempio un’etichetta aggiunta a un campo o a un segmento dello schema. Un amministratore definisce i criteri di accesso che includono attributi per gestire le autorizzazioni di accesso degli utenti.

Questa funzionalità consente di etichettare i campi dello schema Experience Data Model (XDM) con etichette che definiscono gli ambiti di utilizzo organizzativi o dei dati. Parallelamente, gli amministratori possono utilizzare l’interfaccia di amministrazione di utenti e ruoli per definire i criteri di accesso relativi ai campi dello schema XDM e gestire in modo migliore l’accesso concesso a utenti o gruppi di utenti (utenti interni, esterni o di terze parti). Inoltre, il controllo dell’accesso basato su attributi consente agli amministratori di gestire l’accesso a segmenti specifici.

Tramite il controllo degli accessi basato su attributi, gli amministratori dell’organizzazione possono controllare l’accesso degli utenti sia ai dati personali sensibili (SPD) che alle informazioni personali (PII) in tutti i flussi di lavoro e le risorse di Platform. Gli amministratori possono definire ruoli utente con accesso solo a campi e dati specifici che corrispondono a tali campi.

A causa del controllo dell’accesso basato su attributi, alcuni campi e funzionalità avrebbero accesso limitato e non sarebbero disponibili per alcuni modelli di servizio di IA per l’analisi dei clienti. Alcuni esempi includono &quot;Identity&quot;, &quot;Score Definition&quot; e &quot;Clone&quot;.

![Area di lavoro di IA per l&#39;analisi dei clienti con i campi limitati dei risultati del modello di servizio evidenziati.](../images/user-guide/unavailable-functionalities.png)

Nella parte superiore dell&#39;area di lavoro di IA per l&#39;analisi dei clienti **pagina approfondimenti**, i dettagli nella barra laterale, nella definizione del punteggio, nell&#39;identità e negli attributi del profilo mostrano tutti &quot;Accesso limitato&quot;.

![Area di lavoro di IA per l&#39;analisi dei clienti con i campi con restrizioni dello schema evidenziati.](../images/user-guide/access-restricted.png)

Quando si visualizzano in anteprima i set di dati con schema con restrizioni nella pagina **[!UICONTROL Crea flusso di lavoro modello]**, viene visualizzato un avviso che informa che [!UICONTROL A causa di restrizioni di accesso, alcune informazioni non vengono visualizzate nell&#39;anteprima del set di dati.]

![Area di lavoro di IA per l&#39;analisi dei clienti con i campi con restrizioni dei set di dati di anteprima ed evidenziati i risultati dello schema con restrizioni.](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

Dopo aver creato un modello con informazioni limitate e aver proceduto al passaggio **[!UICONTROL Definisci obiettivo]**, nella parte superiore viene visualizzato un avviso: [!UICONTROL A causa di restrizioni di accesso, alcune informazioni non vengono visualizzate nella configurazione.]

![Area di lavoro di IA per l&#39;analisi dei clienti con i campi limitati dei risultati del modello di servizio evidenziati.](../images/user-guide/information-not-displayed-save-and-exit.png)

Quando si utilizza il controllo degli accessi, i privilegi **Visualizza IA per l&#39;analisi dei clienti** e **Gestisci IA per l&#39;analisi dei clienti** concedono l&#39;accesso a diverse funzionalità di IA per l&#39;analisi dei clienti. L&#39;autorizzazione **Gestisci IA per l&#39;analisi dei clienti** ti consente di **creare**,**aggiornare**, **eliminare**, **abilitare** o **disabilitare** un modello, mentre **Visualizza IA per l&#39;analisi dei clienti** ti consente di leggerlo o visualizzarlo. Le azioni **create**, **update** e **delete** vengono registrate nei registri di controllo.

Consulta la documentazione per scoprire [come assegnare le autorizzazioni per il controllo degli accessi](../../../access-control/home.md) o come [utilizzare i registri di audit per monitorare gli accessi e l&#39;attività](../../../landing/governance-privacy-security/audit-logs/overview.md).

## Passaggi successivi

La lettura di questa guida ti ha introdotto i principi fondamentali del controllo degli accessi in [!DNL Experience Platform]. È ora possibile passare alla [guida utente per il controllo degli accessi](../overview.md) per i passaggi dettagliati su come utilizzare [!DNL Admin Console] per creare profili di prodotto e assegnare autorizzazioni per [!DNL Platform].
