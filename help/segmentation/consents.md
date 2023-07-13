---
solution: Experience Platform
title: Rispetto del consenso nei segmenti
description: Scopri come rispettare le preferenze di consenso del cliente per la raccolta e la condivisione di dati personali nelle operazioni dei segmenti.
exl-id: fe851ce3-60db-4984-a73c-f9c5964bfbad
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

# Rispetto del consenso nei segmenti

>[!NOTE]
>
>Questa guida spiega come rispettare i consensi in **definizioni dei segmenti**.

Normative legali sulla privacy come [!DNL California Consumer Privacy Act] (CCPA) conferiscono ai consumatori il diritto di rinunciare alla raccolta o alla condivisione dei propri dati personali con terze parti. Adobe Experience Platform fornisce componenti Experience Data Model (XDM) standard che hanno lo scopo di acquisire queste preferenze di consenso del cliente nei dati del profilo cliente in tempo reale.

Se un cliente ha revocato o negato il consenso alla condivisione dei propri dati personali, è importante che la tua organizzazione rispetti tale preferenza durante la generazione di tipi di pubblico per le attività di marketing. Questo documento descrive come integrare i valori di consenso dei clienti nelle definizioni dei segmenti utilizzando l’interfaccia utente di Experience Platform.

## Introduzione

Rispettare i valori di consenso dei clienti richiede una comprensione dei vari [!DNL Adobe Experience Platform] servizi interessati. Prima di iniziare questo tutorial, assicurati di avere familiarità con i seguenti servizi:

* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): framework standardizzato tramite il quale Platform organizza i dati sull’esperienza del cliente.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): consente di creare tipi di pubblico da [!DNL Real-Time Customer Profile] dati.

## Campi schema di consenso

Per rispettare i consensi e le preferenze del cliente, uno degli schemi che fa parte del tuo [!UICONTROL Profilo individuale XDM] lo schema di unione deve contenere il gruppo di campi standard **[!UICONTROL Consensi e preferenze]**.

Per informazioni dettagliate sulla struttura e sul caso di utilizzo previsto di ciascuno degli attributi forniti dal gruppo di campi, vedi [guida di riferimento su consensi e preferenze](../xdm/field-groups/profile/consents.md). Per istruzioni dettagliate su come aggiungere un gruppo di campi a uno schema, consulta [Guida all’interfaccia utente XDM](../xdm/ui/resources/schemas.md#add-field-groups).

Dopo l’aggiunta del gruppo di campi a un [Schema abilitato per il profilo](../xdm/ui/resources/schemas.md#profile) e i relativi campi sono stati utilizzati per acquisire i dati sul consenso dall’applicazione experience, puoi utilizzare gli attributi di consenso raccolti nelle regole del segmento.

## Gestione del consenso nella segmentazione

Per garantire che i profili di rinuncia non siano inclusi nelle definizioni dei segmenti, è necessario aggiungere campi speciali alle definizioni dei segmenti esistenti e includerli durante la creazione di nuove definizioni dei segmenti.

I passaggi seguenti mostrano come aggiungere i campi appropriati per due tipi di flag di rinuncia:

1. [!UICONTROL Raccolta dati]
1. [!UICONTROL Condividi dati]

>[!NOTE]
>
>Mentre questa guida si concentra sui due flag di rinuncia di cui sopra, puoi configurare le definizioni dei segmenti per incorporare anche segnali di consenso aggiuntivi. Il [guida di riferimento su consensi e preferenze](../xdm/field-groups/profile/consents.md) fornisce ulteriori informazioni su ciascuna di queste opzioni e sui casi d’uso previsti.

Durante la creazione di una definizione di segmento nell’interfaccia utente, in **[!UICONTROL Attributi]**, passa a **[!UICONTROL Profilo individuale XDM]**, quindi seleziona **[!UICONTROL Consensi e preferenze]**. Da qui puoi vedere le opzioni per **[!UICONTROL Raccolta dati]** e **[!UICONTROL Condividi dati]**.

![](./images/opt-outs/consents.png)

Per iniziare, seleziona la **[!UICONTROL Raccolta dati]** categoria, quindi trascina **[!UICONTROL Valore scelta]** nel generatore di segmenti. Quando aggiungi l’attributo alla definizione del segmento, puoi specificare [valori di consenso](../xdm/field-groups/profile/consents.md#choice-values) che devono essere inclusi o esclusi.

![](./images/opt-outs/consent-values.png)

Un approccio consiste nell’escludere tutti i clienti che hanno rinunciato alla raccolta dei loro dati. A questo scopo, imposta l’operatore su **[!UICONTROL non è uguale a]** e scegliere i seguenti valori:

* **[!UICONTROL No (rinuncia)]**
* **[!UICONTROL Predefinito per No (rinuncia)]**
* **[!UICONTROL Sconosciuto]** (se si presume che il consenso sia stato negato, se non altrimenti noto)

![](./images/opt-outs/collect.png)

Sotto **[!UICONTROL Attributi]** nella barra a sinistra, torna a **[!UICONTROL Consensi e preferenze]** , quindi seleziona **[!UICONTROL Condividi dati]**. Trascina il corrispondente **[!UICONTROL Valore scelta]** nell’area di lavoro e seleziona gli stessi valori di quelli per [!UICONTROL Raccolta dati] valore di scelta. Assicurati che un’ **[!UICONTROL Oppure]** viene stabilita una relazione tra i due attributi.

![](./images/opt-outs/share.png)

Con entrambe le opzioni **[!UICONTROL Raccolta dati]** e **[!UICONTROL Condividi dati]** Se alla definizione del segmento sono stati aggiunti dei valori di consenso, tutti i clienti che hanno rinunciato all’utilizzo dei loro dati verranno esclusi dal pubblico risultante. Da qui, puoi continuare a personalizzare la definizione del segmento prima di selezionare **[!UICONTROL Salva]** per completare il processo.

## Passaggi successivi

Seguendo questa esercitazione, avrai una migliore comprensione di come rispettare i consensi e le preferenze del cliente durante la creazione delle definizioni dei segmenti in Experience Platform.

Per ulteriori informazioni sulla gestione del consenso in Platform, consulta la seguente documentazione:

* [Elaborazione del consenso utilizzando lo standard Adobe](../landing/governance-privacy-security/consent/adobe/overview.md)
* [Elaborazione del consenso utilizzando lo standard IAB TCF 2.0](../landing/governance-privacy-security/consent/iab/overview.md)