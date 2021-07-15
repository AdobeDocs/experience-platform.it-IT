---
keywords: Experience Platform;home;argomenti popolari;opt-out;segmentazione;servizio di segmentazione;servizio di segmentazione;onorare le rinunce;opt-out;opt-out;opt-out;consenso;condivisione;raccogliere;
solution: Experience Platform
title: Rispetto del consenso nei segmenti
topic-legacy: overview
description: Scopri come rispettare le preferenze di consenso dei clienti per la raccolta e la condivisione di dati personali nelle operazioni sui segmenti.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: bd312024a1a3fb6da840a38d6e9d19fcbd6eab5a
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Rispettare il consenso nei segmenti

Le normative legali sulla privacy, come il [!DNL California Consumer Privacy Act] (CCPA), offrono ai consumatori il diritto di negare il consenso alla raccolta o alla condivisione dei propri dati personali con terze parti. Adobe Experience Platform fornisce componenti XDM (Experience Data Model) standard destinati a acquisire queste preferenze di consenso dei clienti nei dati del profilo cliente in tempo reale.

Se un cliente ha ritirato o rifiutato il consenso per la condivisione dei propri dati personali, è importante che la tua organizzazione rispetta tale preferenza durante la generazione di tipi di pubblico per attività di marketing. Questo documento descrive come integrare i valori di consenso dei clienti nelle definizioni dei segmenti utilizzando l’interfaccia utente di Experience Platform.

## Introduzione

Il rispetto dei valori di consenso dei clienti richiede una comprensione dei vari servizi [!DNL Adobe Experience Platform] coinvolti. Prima di avviare questa esercitazione, accertati di avere familiarità con i seguenti servizi:

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Il framework standardizzato tramite il quale Platform organizza i dati sulla customer experience.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Ti consente di creare segmenti di pubblico dai  [!DNL Real-time Customer Profile] dati.

## Campi dello schema di consenso

Per rispettare i consensi e le preferenze del cliente, uno degli schemi che fa parte dello schema di unione [!UICONTROL Profilo individuale XDM] deve contenere il gruppo di campi standard **[!UICONTROL Consensi e preferenze]**.

Per informazioni dettagliate sulla struttura e sul caso d&#39;uso previsto per ciascuno degli attributi forniti dal gruppo di campi, consulta la guida di riferimento [consensi e preferenze](../xdm/field-groups/profile/consents.md). Per istruzioni dettagliate su come aggiungere un gruppo di campi a uno schema, consulta la [Guida all’interfaccia utente XDM](../xdm/ui/resources/schemas.md#add-field-groups) .

Una volta aggiunto il gruppo di campi a uno [schema abilitato per il profilo](../xdm/ui/resources/schemas.md#profile) e i relativi campi sono stati utilizzati per acquisire i dati di consenso dall’applicazione di esperienza, puoi utilizzare gli attributi di consenso raccolti nelle regole del segmento.

## Gestione del consenso nella segmentazione

Per evitare che i profili di rinuncia siano inclusi nei segmenti, è necessario aggiungere campi speciali ai segmenti esistenti e includerli durante la creazione di nuovi segmenti.

I passaggi seguenti mostrano come aggiungere i campi appropriati per due tipi di flag di rinuncia:

1. [!UICONTROL Raccolta dati]
1. [!UICONTROL Condividi dati]

>[!NOTE]
>
>Mentre questa guida si concentra sui due flag di rinuncia di cui sopra, puoi configurare i segmenti in modo da includere anche segnali di consenso aggiuntivi. La [guida di riferimento per i consensi e le preferenze](../xdm/field-groups/profile/consents.md) fornisce ulteriori informazioni su ciascuna di queste opzioni e sui relativi casi d&#39;uso previsti.

Durante la creazione di un segmento nell&#39;interfaccia utente, in **[!UICONTROL Attributi]**, passa a **[!UICONTROL Profilo individuale XDM]**, quindi seleziona **[!UICONTROL Consensi e preferenze]**. Da qui puoi vedere le opzioni per **[!UICONTROL Raccolta dati]** e **[!UICONTROL Condividi dati]**.

![](./images/opt-outs/consents.png)

Inizia selezionando la categoria **[!UICONTROL Raccolta dati]** , quindi trascina **[!UICONTROL Valore di scelta]** nel generatore di segmenti. Quando aggiungi l’attributo al segmento, puoi specificare i [valori di consenso](../xdm/field-groups/profile/consents.md#choice-values) che devono essere inclusi o esclusi.

![](./images/opt-outs/consent-values.png)

Un approccio consiste nell’escludere i clienti che hanno rinunciato alla raccolta dei dati. A questo scopo, imposta l&#39;operatore su **[!UICONTROL non è uguale a]** e scegli i seguenti valori:

* **[!UICONTROL No (rinuncia)]**
* **[!UICONTROL Predefinito di No (rinuncia)]**
* **[!UICONTROL Sconosciuto]**  (se si presume che il consenso venga rifiutato se non si conosce)

![](./images/opt-outs/collect.png)

Alla voce **[!UICONTROL Attributi]** nella barra a sinistra, torna alla sezione **[!UICONTROL Consensi e preferenze]**, quindi seleziona **[!UICONTROL Condividi dati]**. Trascina il valore **[!UICONTROL Choice Value]** corrispondente nell&#39;area di lavoro e seleziona gli stessi valori del valore di scelta [!UICONTROL Data Collection]. Assicurati che tra i due attributi sia stabilita una relazione **[!UICONTROL Or]** .

![](./images/opt-outs/share.png)

Con i valori di consenso **[!UICONTROL Raccolta dati]** e **[!UICONTROL Condividi dati]** aggiunti al segmento, tutti i clienti che hanno rinunciato all’utilizzo dei propri dati verranno esclusi dal pubblico risultante. Da qui, puoi continuare a personalizzare la definizione del segmento prima di selezionare **[!UICONTROL Salva]** per completare il processo.

## Passaggi successivi

Seguendo questa esercitazione, dovresti ora avere una migliore comprensione di come rispettare i consensi e le preferenze dei clienti durante la creazione di segmenti in Experience Platform.

Per ulteriori informazioni sulla gestione del consenso in Platform, consulta la seguente documentazione:

* [Elaborazione del consenso tramite lo standard Adobe](../landing/governance-privacy-security/consent/adobe/overview.md)
* [Elaborazione del consenso tramite lo standard IAB TCF 2.0](../landing/governance-privacy-security/consent/iab/overview.md)