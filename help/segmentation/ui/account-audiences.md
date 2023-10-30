---
title: Pubblico dell’account
description: Scopri come creare e utilizzare i tipi di pubblico dell’account per eseguire il targeting dei profili dell’account nelle destinazioni a valle.
badgeLimitedAvailability: label="Disponibilità limitata" type="Caution"
badgeB2B: label="Edizione B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 047930d6-939f-4418-bbcb-8aafd2cf43ba
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# Pubblico dell’account

>[!AVAILABILITY]
>
>I tipi di pubblico dell’account sono disponibili solo in [Edizione B2B di Real-time Customer Data Platform](../../rtcdp/b2b-overview.md). Inoltre, la funzionalità di pubblico dell’account è attualmente in **disponibilità limitata**. Contatta l’Assistenza clienti Adobe o il tuo rappresentante Adobe per richiedere l’accesso a questa funzionalità.

Con la segmentazione dell’account, Adobe Experience Platform ti consente di rendere l’esperienza di segmentazione del marketing completamente semplice e sofisticata, dal pubblico basato sulle persone a quello basato sull’account.

I tipi di pubblico dell’account possono essere utilizzati come input per le destinazioni basate su account, consentendoti di eseguire il targeting delle persone all’interno di tali account nei servizi a valle. Ad esempio, puoi utilizzare tipi di pubblico basati sull’account per recuperare i record di tutti gli account che lo fanno **non** disporre di informazioni di contatto per qualsiasi persona con il titolo di Chief Operating Officer (COO) o Chief Marketing Officer (CMO).

## Terminologia {#terminology}

Prima di iniziare a utilizzare i tipi di pubblico dell’account, esamina le differenze tra i diversi tipi di pubblico:

- **Pubblico dell’account**: un pubblico di tipo account è un pubblico che viene creato con **account** dati del profilo. I dati del profilo account possono essere utilizzati per creare tipi di pubblico mirati alle persone negli account a valle. Per ulteriori informazioni sui profili dell’account, consulta [panoramica del profilo account](../../rtcdp/accounts/account-profile-overview.md).
- **Pubblico persone**: un pubblico di tipo Persone è un pubblico che viene creato con **cliente** dati del profilo. I dati del profilo cliente possono essere utilizzati per creare tipi di pubblico mirati alla clientela della tua azienda. Per ulteriori informazioni sui profili dei clienti, consulta [Panoramica del profilo cliente in tempo reale](../../profile/home.md).
- **Pubblico potenziale**: un pubblico potenziale è un pubblico che viene creato con **potenziale cliente** dati del profilo. I dati del profilo del potenziale cliente possono essere utilizzati per creare tipi di pubblico da utenti non autenticati. Per ulteriori informazioni sui profili potenziali, consulta la sezione [panoramica del profilo di prospect](../../profile/ui/prospect-profile.md).

## Accedere ad {#access}

Per accedere ai tipi di pubblico dell’account, seleziona **[!UICONTROL Tipi di pubblico]** nel **[!UICONTROL Account]** sezione.

![Il pulsante Tipi di pubblico è evidenziato nella sezione Account.](../images/ui/account-audiences/select.png)

Il [!UICONTROL Sfoglia] viene visualizzata una pagina con un elenco di tutti i tipi di pubblico dell’account per l’organizzazione.

![Vengono visualizzati i tipi di pubblico dell’account appartenenti all’organizzazione.](../images/ui/account-audiences/browse.png)

Questa vista elenca informazioni sul pubblico, tra cui nome, conteggio dei profili, origine, stato del ciclo di vita, data di creazione e data dell’ultimo aggiornamento.

## Creare un pubblico {#create}

Per creare un pubblico di tipo account, seleziona **[!UICONTROL Creare un pubblico]** il [!UICONTROL Sfoglia] pagina.

![Il [!UICONTROL Creare un pubblico] nella pagina di navigazione del pubblico dell’account.](../images/ui/account-audiences/select-create-audience.png)

Viene visualizzato il Generatore di segmenti. Gli attributi dell’account vengono visualizzati sulla barra di navigazione a sinistra.

![Viene visualizzato il Generatore di segmenti. Vengono visualizzati solo gli attributi.](../images/ui/account-audiences/segment-builder.png)

Durante la creazione del pubblico dell’account, tieni presente che gli eventi sono elencati in **[!UICONTROL Persone]**, anziché essere la propria scheda, in quanto questi attributi sono associati alle persone.

![La posizione in cui trovare gli eventi, che si trova all’interno del [!UICONTROL Persone] cartella, viene evidenziato.](../images/ui/account-audiences/attributes.png)

Per ulteriori informazioni sull’utilizzo del Generatore di segmenti, consulta la sezione [Guida dell’interfaccia utente di Segment Builder](./segment-builder.md).

## Attiva pubblico {#activate}

>[!NOTE]
>
>Solo un numero limitato di destinazioni supporta i tipi di pubblico dell’account. Prima di continuare, assicurati che la destinazione da attivare supporti i tipi di pubblico dell&#39;account.

Dopo aver creato il pubblico del tuo account, puoi attivarlo in altri servizi a valle.

Seleziona il pubblico da attivare, seguito da **[!UICONTROL Attiva nella destinazione]**.

![Il [!UICONTROL Attiva nella destinazione] nel menu Azioni rapide per il pubblico selezionato.](../images/ui/account-audiences/activate.png)

Il [!UICONTROL Attiva destinazione] viene visualizzata. Per ulteriori informazioni sul processo di attivazione, comprese le destinazioni supportate e i dettagli sulle mappature dei campi, leggi [attivare il pubblico dell’account](/help/destinations/ui/activate-account-audiences.md) esercitazione.

## Passaggi successivi {#next-steps}

Dopo aver letto questa guida, ora hai una migliore comprensione di come creare e utilizzare i tipi di pubblico del tuo account in Adobe Experience Platform. Per scoprire come utilizzare altri tipi di pubblico in Platform, leggi la sezione [Guida dell’interfaccia utente di Segmentation Service](./overview.md).
