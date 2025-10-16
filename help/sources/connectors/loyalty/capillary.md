---
title: Panoramica degli eventi di streaming capillare
description: Scopri come inviare dati da Capillary ad Experience Platform.
badge: Beta
exl-id: 3b8eb2f6-3b4a-4b91-89d4-b6d9027c6ab4
source-git-commit: 428aed259343f56a2bf493b40ff2388340fffb7b
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# [!DNL Capillary Streaming Events]

>[!AVAILABILITY]
>
>L&#39;origine [!DNL Capillary Streaming Events] è in versione beta. Leggi i [termini e condizioni](../../home.md#terms-and-conditions) nella panoramica delle origini per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta.

[!DNL Capillary Technologies] è una piattaforma di fidelizzazione e coinvolgimento leader, affidabile da oltre 300 marchi in tutto il mondo. Utilizza l&#39;origine [!DNL Capillary Streaming Events] per consentire alla tua azienda di trasferire in streaming i profili dei clienti, i dati sulla fedeltà e gli eventi transazionali da [!DNL Capillary] a Adobe Experience Platform. Connetti l&#39;origine [!DNL Capillary] per abilitare la personalizzazione in tempo reale, la segmentazione avanzata del pubblico e l&#39;orchestrazione omnicanale delle campagne.

Integrando [!DNL Capillary] con Experience Platform, è possibile:

* Sincronizza **punti fedeltà, livelli e premi** in tempo reale.
* Invia **dati transazionali** ad Experience Platform per l&#39;analisi e l&#39;attivazione.
* Sfrutta Real-Time CDP, Experience Platform e Adobe Journey Optimizer per la segmentazione, l’orchestrazione del percorso e la personalizzazione.

## Prerequisiti

Prima di connettere [!DNL Capillary] a Adobe Experience Platform, assicurati di disporre dei seguenti elementi:

* Un **ID organizzazione Adobe** valido e l&#39;accesso a una sandbox Experience Platform abilitata.
* Per connettere l&#39;account **[!UICONTROL ad Experience Platform, è necessario che per l&#39;account siano abilitate le autorizzazioni]** Visualizza origini **[!UICONTROL e]** Gestisci origini[!DNL Capillary]. Contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie. Per ulteriori informazioni, leggere la [guida all&#39;interfaccia utente per il controllo degli accessi](../../../access-control/ui/overview.md).

### Crea uno schema

È necessario creare uno schema Experience Data Model (XDM) per descrivere un set di dati che può memorizzare i possibili campi e tipi di dati che verranno inviati da [!DNL Capillary].

1. Accedi a Adobe Experience Platform e accedi ad Experience Platform tramite l’accesso dell’organizzazione.
2. Nel pannello di navigazione a sinistra, seleziona **[!UICONTROL Schemi]** per aprire l&#39;area di lavoro [!UICONTROL Schemi].
3. Seleziona **[!UICONTROL Crea schema]** nell&#39;angolo superiore destro.
4. Nella finestra di dialogo per la creazione dello schema, scegli tra **[!UICONTROL Creazione manuale]** (Aggiungi tu stesso campi e gruppi di campi) o **[!UICONTROL Creazione assistita da ML]** (Carica un file CSV e utilizza l&#39;apprendimento automatico per generare uno schema consigliato).
5. Scegli una classe base per lo schema (ad esempio XDM Individual Profile, XDM ExperienceEvent o Altro). Se selezioni **[!UICONTROL Altro]**, puoi scegliere tra le classi personalizzate o standard disponibili.
6. Immetti un nome e una descrizione descrittivi per lo schema.
7. Utilizza l’Editor schema per: aggiungere gruppi di campi (blocchi di campi riutilizzabili), definire singoli campi (personalizzare nomi, tipi di dati e opzioni) e, facoltativamente, creare tipi di dati o gruppi di campi personalizzati se quelli esistenti non soddisfano le tue esigenze.
8. Rivedi la struttura dello schema nell’area di lavoro. Seleziona **[!UICONTROL Fine]** per creare lo schema.
9. (Facoltativo) Modifica i campi, aggiungi le descrizioni e regola i gruppi di campi in base alle esigenze nell’Editor di schema.

Per istruzioni dettagliate su come creare uno schema XDM, consulta la guida in [creazione di uno schema tramite l&#39;editor schema](../../../xdm/tutorials/create-schema-ui.md).

### Creare un set di dati

Successivamente, devi creare un set di dati che faccia riferimento allo schema appena creato.

1. Nell&#39;interfaccia utente di Experience Platform, seleziona [!UICONTROL Set di dati] nell&#39;area di navigazione a sinistra per aprire l&#39;area di lavoro [!UICONTROL Set di dati].
2. Seleziona **[!UICONTROL Crea set di dati]** in alto a destra.
3. Nelle opzioni di creazione, seleziona **[!UICONTROL Crea set di dati dallo schema]**.
4. Dall’elenco, cerca e seleziona lo schema XDM creato in precedenza. Dopo aver individuato lo schema, seleziona **[!UICONTROL Avanti]**.
5. Immetti un nome univoco e descrittivo per il set di dati.
6. Facoltativamente, aggiungi una descrizione che consenta agli utenti futuri di identificare il set di dati.
7. Seleziona **[!UICONTROL Fine]** per creare il set di dati.

Per istruzioni dettagliate su come creare un set di dati, consulta la [guida dell&#39;interfaccia utente dei set di dati](../../../catalog/datasets/user-guide.md).

## Connetti [!DNL Capillary Streaming Events] ad Experience Platform

Dopo aver completato la configurazione dei prerequisiti per [!DNL Capillary], leggi l&#39;[[!DNL Capillary Streaming Events] esercitazione dell&#39;interfaccia utente](../../tutorials/ui/create/loyalty/capillary.md) per scoprire come collegare il tuo account e inviare dati da [!DNL Capillary] ad Experience Platform.
