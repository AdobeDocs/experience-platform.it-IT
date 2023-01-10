---
keywords: Experience Platform;home;argomenti popolari;opt-out;segmentazione;servizio di segmentazione;servizio di segmentazione;onorare le rinunce;opt-out;opt-out;opt-out;consenso;condivisione;raccogliere;
solution: Experience Platform
title: Rispetto del consenso nei segmenti
description: Scopri come rispettare le preferenze di consenso dei clienti per la raccolta e la condivisione di dati personali nelle operazioni sui segmenti.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Rispettare il consenso nei segmenti

Norme legali sulla privacy come [!DNL California Consumer Privacy Act] (CCPA) dare ai consumatori il diritto di rinunciare alla raccolta o alla condivisione di dati personali con terzi. Adobe Experience Platform fornisce componenti XDM (Experience Data Model) standard destinati a acquisire queste preferenze di consenso dei clienti nei dati del profilo cliente in tempo reale.

Se un cliente ha ritirato o rifiutato il consenso per la condivisione dei propri dati personali, è importante che la tua organizzazione rispetta tale preferenza durante la generazione di tipi di pubblico per attività di marketing. Questo documento descrive come integrare i valori di consenso dei clienti nelle definizioni dei segmenti utilizzando l’interfaccia utente di Experience Platform.

## Introduzione

Il rispetto dei valori di consenso dei clienti richiede una comprensione dei vari [!DNL Adobe Experience Platform] servizi interessati. Prima di avviare questa esercitazione, accertati di avere familiarità con i seguenti servizi:

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Il framework standardizzato tramite il quale Platform organizza i dati sulla customer experience.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Consente di creare segmenti di pubblico da [!DNL Real-Time Customer Profile] dati.

## Campi dello schema di consenso

Per rispettare i consensi e le preferenze del cliente, uno degli schemi che fa parte del tuo [!UICONTROL Profilo individuale XDM] lo schema unione deve contenere il gruppo di campi standard **[!UICONTROL Consensi e preferenze]**.

Per informazioni dettagliate sulla struttura e sul caso d’uso previsto di ciascuno degli attributi forniti dal gruppo di campi, consulta la [guida di riferimento a consenso e preferenze](../xdm/field-groups/profile/consents.md). Per istruzioni dettagliate su come aggiungere un gruppo di campi a uno schema, consulta [Guida all’interfaccia utente XDM](../xdm/ui/resources/schemas.md#add-field-groups).

Una volta aggiunto il gruppo di campi a un [Schema abilitato per il profilo](../xdm/ui/resources/schemas.md#profile) e i relativi campi sono stati utilizzati per acquisire i dati di consenso dall’applicazione di esperienza, puoi utilizzare gli attributi di consenso raccolti nelle regole del segmento.

## Gestione del consenso nella segmentazione

Per evitare che i profili di rinuncia siano inclusi nei segmenti, è necessario aggiungere campi speciali ai segmenti esistenti e includerli durante la creazione di nuovi segmenti.

I passaggi seguenti mostrano come aggiungere i campi appropriati per due tipi di flag di rinuncia:

1. [!UICONTROL Raccolta dati]
1. [!UICONTROL Condividi dati]

>[!NOTE]
>
>Mentre questa guida si concentra sui due flag di rinuncia di cui sopra, puoi configurare i segmenti in modo da includere anche segnali di consenso aggiuntivi. La [guida di riferimento a consenso e preferenze](../xdm/field-groups/profile/consents.md) fornisce ulteriori informazioni su ciascuna di queste opzioni e sui relativi casi d’uso previsti.

Durante la creazione di un segmento nell’interfaccia utente, in **[!UICONTROL Attributi]**, passa a **[!UICONTROL Profilo individuale XDM]**, quindi seleziona **[!UICONTROL Consensi e preferenze]**. Da qui puoi vedere le opzioni per **[!UICONTROL Raccolta dati]** e **[!UICONTROL Condividi dati]**.

![](./images/opt-outs/consents.png)

Inizia selezionando la **[!UICONTROL Raccolta dati]** categoria , quindi trascina **[!UICONTROL Valore di scelta]** nel generatore di segmenti. Quando aggiungi l’attributo al segmento, puoi specificare la variabile [valori di consenso](../xdm/field-groups/profile/consents.md#choice-values) che devono essere inclusi o esclusi.

![](./images/opt-outs/consent-values.png)

Un approccio consiste nell’escludere i clienti che hanno rinunciato alla raccolta dei dati. A questo scopo, imposta l’operatore su **[!UICONTROL è diverso da]** e scegli i seguenti valori:

* **[!UICONTROL No (rinuncia)]**
* **[!UICONTROL Predefinito di No (rinuncia)]**
* **[!UICONTROL Sconosciuto]** (se si presume che il consenso sia negato se non altrimenti noto)

![](./images/opt-outs/collect.png)

Sotto **[!UICONTROL Attributi]** nella barra a sinistra, torna alla **[!UICONTROL Consensi e preferenze]** , quindi seleziona **[!UICONTROL Condividi dati]**. Trascina il corrispondente **[!UICONTROL Valore di scelta]** nell’area di lavoro e selezionare gli stessi valori per [!UICONTROL Raccolta dati] valore di scelta. Assicurati che **[!UICONTROL Oppure]** la relazione è stabilita tra i due attributi.

![](./images/opt-outs/share.png)

Con entrambi i **[!UICONTROL Raccolta dati]** e **[!UICONTROL Condividi dati]** i valori di consenso aggiunti al segmento, verranno esclusi dal pubblico risultante tutti i clienti che hanno rinunciato all’utilizzo dei loro dati. Da qui, puoi continuare a personalizzare la definizione del segmento prima di selezionare **[!UICONTROL Salva]** per completare il processo.

## Passaggi successivi

Seguendo questa esercitazione, dovresti ora avere una migliore comprensione di come rispettare i consensi e le preferenze dei clienti durante la creazione di segmenti in Experience Platform.

Per ulteriori informazioni sulla gestione del consenso in Platform, consulta la seguente documentazione:

* [Elaborazione del consenso tramite lo standard Adobe](../landing/governance-privacy-security/consent/adobe/overview.md)
* [Elaborazione del consenso tramite lo standard IAB TCF 2.0](../landing/governance-privacy-security/consent/iab/overview.md)