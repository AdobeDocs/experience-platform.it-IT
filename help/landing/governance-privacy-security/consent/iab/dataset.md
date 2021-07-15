---
keywords: Experience Platform;home;IAB;IAB 2.0;consenso;consenso
solution: Experience Platform
title: Creare set di dati per l’acquisizione dei dati di consenso IAB TCF 2.0
topic-legacy: privacy events
description: Questo documento fornisce passaggi per impostare i due set di dati necessari per raccogliere i dati di consenso IAB TCF 2.0.
exl-id: 36b2924d-7893-4c55-bc33-2c0234f1120e
source-git-commit: 9b75a69cc6e31ea0ad77048a6ec1541df2026f27
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 0%

---

# Creare set di dati per l’acquisizione dei dati di consenso IAB TCF 2.0

Affinché Adobe Experience Platform possa elaborare i dati di consenso dei clienti in conformità a IAB [!DNL Transparency & Consent Framework] (TCF) 2.0, tali dati devono essere inviati ai set di dati i cui schemi contengono campi di consenso TCF 2.0.

In particolare, per acquisire i dati di consenso TCF 2.0 sono necessari due set di dati:

* Un set di dati basato sulla classe [!DNL XDM Individual Profile], abilitato per l’utilizzo in [!DNL Real-time Customer Profile].
* Un set di dati basato sulla classe [!DNL XDM ExperienceEvent] .

>[!IMPORTANT]
>
>Platform applica solo le stringhe TCF raccolte nel set di dati di profilo individuale. Anche se è ancora necessario un set di dati ExperienceEvent per creare un datastream come parte di questo flusso di lavoro, è sufficiente inserire i dati nel set di dati del profilo. Il set di dati ExperienceEvent può ancora essere utilizzato se desideri tenere traccia degli eventi di modifica del consenso nel tempo, ma questi valori non vengono utilizzati in quando si impone l’attivazione dei segmenti.

Questo documento descrive i passaggi necessari per impostare questi due set di dati. Per una panoramica dell’intero flusso di lavoro per configurare le operazioni relative ai dati della piattaforma per TCF 2.0, consulta la [panoramica sulla conformità IAB TCF 2.0](./overview.md).

## Prerequisiti

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Experience Data Model (XDM)](../../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM.
* [Servizio](../../../../identity-service/home.md) Adobe Experience Platform Identity: Consente di collegare le identità dei clienti da diverse origini dati tra dispositivi e sistemi.
   * [Namespace](../../../../identity-service/namespaces.md) di identità: I dati di identità cliente devono essere forniti in uno spazio dei nomi di identità specifico riconosciuto dal servizio Identity.
* [Profilo](../../../../profile/home.md) cliente in tempo reale: Utilizza  [!DNL Identity Service] per creare in tempo reale profili cliente dettagliati dai set di dati. [!DNL Real-time Customer Profile] richiama i dati dal Data Lake e persiste i profili dei clienti nel proprio archivio dati separato.

## Gruppi di campi TCF 2.0 {#field-groups}

Il gruppo di campi di schema [!UICONTROL IAB TCF 2.0 Consent] fornisce i campi di consenso dei clienti richiesti per il supporto TCF 2.0. Sono disponibili due versioni di questo gruppo di campi: uno compatibile con la classe [!DNL XDM Individual Profile] e l&#39;altro con la classe [!DNL XDM ExperienceEvent].

Le sezioni seguenti illustrano la struttura di ciascuno di questi gruppi di campi, compresi i dati attesi durante l’acquisizione.

### Gruppo di campi del profilo {#profile-field-group}

Per gli schemi basati su [!DNL XDM Individual Profile], il gruppo di campi [!UICONTROL Consent] IAB TCF 2.0 fornisce un singolo campo di tipo mappa, `identityPrivacyInfo`, che mappa le identità dei clienti alle loro preferenze di consenso TCF. Questo gruppo di campi deve essere incluso in uno schema basato su record abilitato per Profilo cliente in tempo reale per consentire l’applicazione automatica.

Per ulteriori informazioni sulla struttura e sul caso d’uso, consulta la [guida di riferimento](../../../../xdm/field-groups/profile/iab.md) per questo gruppo di campi .

### Gruppo di campi evento {#event-field-group}

Se desideri tenere traccia degli eventi di modifica del consenso nel tempo, puoi aggiungere il gruppo di campi [!UICONTROL Consent] IAB TCF 2.0 allo schema [!UICONTROL XDM ExperienceEvent] .

Se non prevedi di tenere traccia degli eventi di modifica del consenso nel tempo, non devi includere questo gruppo di campi nello schema dell’evento. Quando si applicano automaticamente i valori di consenso TCF, in Experience Platform vengono utilizzate solo le informazioni di consenso più recenti acquisite nel gruppo di campi [profilo](#profile-field-group). I valori di consenso acquisiti dagli eventi non partecipano ai flussi di lavoro di implementazione automatica.

Per ulteriori informazioni sulla struttura e sul caso d’uso, consulta la [guida di riferimento](../../../../xdm/field-groups/event/iab.md) per questo gruppo di campi.

## Creare schemi di consenso dei clienti {#create-schemas}

Per creare set di dati che acquisiscono i dati di consenso, devi prima creare schemi XDM su cui basare tali set di dati.

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Schemi]** nel menu di navigazione a sinistra per aprire l’area di lavoro [!UICONTROL Schemi]. Da qui, segui i passaggi descritti nelle sezioni seguenti per creare ogni schema richiesto.

>[!NOTE]
>
>Se disponi di schemi XDM esistenti che desideri utilizzare per acquisire i dati di consenso, puoi modificarli invece di crearne di nuovi. Tuttavia, se uno schema esistente è stato abilitato per l’utilizzo in Profilo cliente in tempo reale, la sua identità principale non può essere un campo direttamente identificabile che non è consentito utilizzare nella pubblicità basata su interessi, ad esempio un indirizzo e-mail. Consulta il tuo consulente legale se non sei sicuro di quali campi siano soggetti a restrizioni.
>
>Inoltre, quando si modificano gli schemi esistenti, è possibile apportare solo modifiche aggiuntive (non rivoluzionarie). Per ulteriori informazioni, consulta la sezione sui [principi dell&#39;evoluzione dello schema](../../../../xdm/schema/composition.md#evolution) .

### Creare uno schema di consenso del profilo {#profile-schema}

Seleziona **[!UICONTROL Crea schema]**, quindi scegli **[!UICONTROL Profilo individuale XDM]** dal menu a discesa.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Aggiungi gruppi di campi]**, che consente di iniziare subito ad aggiungere gruppi di campi allo schema. Da qui, seleziona **[!UICONTROL IAB TCF 2.0 Consent]** dall&#39;elenco. Facoltativamente, puoi utilizzare la barra di ricerca per limitare i risultati per individuare più facilmente il gruppo di campi. Una volta selezionato il gruppo di campi, selezionare **[!UICONTROL Aggiungi gruppi di campi]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

L’area di lavoro viene visualizzata nuovamente, mostrando che il campo `identityPrivacyInfo` è stato aggiunto alla struttura dello schema.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

Prima di aggiungere altri campi allo schema, seleziona il campo principale per visualizzare **[!UICONTROL Proprietà dello schema]** nella barra a destra, dove puoi fornire un nome e una descrizione per lo schema.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-profile.png)

Dopo aver fornito un nome e una descrizione, seleziona **[!UICONTROL Aggiungi]** nella sezione **[!UICONTROL Gruppi di campi]** sul lato sinistro dell&#39;area di lavoro.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-profile.png)

Da qui, utilizza la finestra di dialogo per aggiungere i seguenti gruppi di campi aggiuntivi allo schema:

* [!UICONTROL IdentityMap]
* [!UICONTROL Area geografica di acquisizione dati per profilo]
* [!UICONTROL Dettagli demografici]
* [!UICONTROL Dati di contatto personali]

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-all-field-groups.png)

Se stai modificando uno schema esistente che è già stato abilitato per l&#39;utilizzo in [!DNL Real-time Customer Profile], seleziona **[!UICONTROL Salva]** per confermare le modifiche prima di passare alla sezione relativa alla creazione di un set di dati basato sullo schema di consenso](#dataset). [ Se stai creando un nuovo schema, continua a seguire i passaggi descritti nella sottosezione seguente.

#### Abilita lo schema da utilizzare in [!DNL Real-time Customer Profile]

Affinché Platform possa associare i dati di consenso ricevuti a profili cliente specifici, è necessario che lo schema di consenso sia abilitato per l’utilizzo in [!DNL Real-time Customer Profile].

>[!NOTE]
>
>Lo schema di esempio mostrato in questa sezione utilizza il relativo campo `identityMap` come identità principale. Se desideri impostare un altro campo come identità principale, accertati di utilizzare un identificatore indiretto come un ID cookie e non un campo direttamente identificabile che non è possibile utilizzare nella pubblicità basata su interessi, ad esempio un indirizzo e-mail. Consulta il tuo consulente legale se non sei sicuro di quali campi siano soggetti a restrizioni.
>
>I passaggi su come impostare un campo di identità principale per uno schema si trovano nell&#39;esercitazione [creazione dello schema](../../../../xdm/tutorials/create-schema-ui.md#identity-field).

Per abilitare lo schema per [!DNL Profile], seleziona il nome dello schema nella barra a sinistra per aprire la sezione **[!UICONTROL Proprietà schema]** . Da qui, seleziona il pulsante di attivazione/disattivazione **[!UICONTROL Profilo]** .

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

Viene visualizzato un puntatore che indica un&#39;identità principale mancante. Seleziona la casella di controllo per utilizzare un&#39;identità principale alternativa, in quanto l&#39;identità principale sarà contenuta nel campo `identityMap` .

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

Infine, seleziona **[!UICONTROL Salva]** per confermare le modifiche.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### Creare uno schema di consenso evento {#event-schema}

Nell&#39;area di lavoro **[!UICONTROL Schemi]**, seleziona **[!UICONTROL Crea schema]**, quindi scegli **[!UICONTROL XDM ExperienceEvent]** dal menu a discesa.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Aggiungi gruppi di campi]** . Da qui, seleziona **[!UICONTROL IAB TCF 2.0 Consent]** dall&#39;elenco. Facoltativamente, puoi utilizzare la barra di ricerca per limitare i risultati per individuare più facilmente il gruppo di campi. Dopo aver selezionato il gruppo di campi, selezionare **[!UICONTROL Aggiungi gruppi di campi]**.

>[!NOTE]
>
>L’inclusione di questo gruppo di campi nello schema dell’evento è necessaria solo se si prevede di tenere traccia degli eventi di modifica del consenso nel tempo. Se non desideri tenere traccia di questi eventi, puoi utilizzare uno schema evento senza questi campi al momento di configurare l’SDK per web.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

L’area di lavoro viene visualizzata nuovamente, mostrando che il campo `consentStrings` è stato aggiunto alla struttura dello schema.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

Prima di aggiungere altri campi allo schema, seleziona il campo principale per visualizzare **[!UICONTROL Proprietà dello schema]** nella barra a destra, dove puoi fornire un nome e una descrizione per lo schema.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-event.png)

Dopo aver fornito un nome e una descrizione, seleziona **[!UICONTROL Aggiungi]** nella sezione **[!UICONTROL Gruppi di campi]** sul lato sinistro dell&#39;area di lavoro.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-event.png)

Da qui, ripeti i passaggi precedenti per aggiungere i seguenti gruppi di campi aggiuntivi allo schema:

* [!UICONTROL IdentityMap]
* [!UICONTROL Dettagli dell&#39;ambiente]
* [!UICONTROL Dettagli Web]
* [!UICONTROL Dettagli di implementazione]

Una volta aggiunti i gruppi di campi, terminare selezionando **[!UICONTROL Salva]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-field-groups.png)

## Creare set di dati in base agli schemi di consenso {#datasets}

Per ciascuno degli schemi richiesti sopra descritti, devi creare un set di dati che in definitiva acquisirà i dati di consenso dei clienti. Il set di dati basato sullo schema del record deve essere abilitato per [!DNL Real-time Customer Profile], mentre il set di dati basato sullo schema delle serie temporali **non deve essere** abilitato.[!DNL Profile]

Per iniziare, seleziona **[!UICONTROL Set di dati]** nel menu di navigazione di sinistra, quindi seleziona **[!UICONTROL Crea set di dati]** nell&#39;angolo in alto a destra.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

Nella pagina successiva, seleziona **[!UICONTROL Crea set di dati da schema]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

Viene visualizzato il flusso di lavoro **[!UICONTROL Crea set di dati da schema]** , a partire dal passaggio **[!UICONTROL Seleziona schema]** . Nell’elenco fornito, individua uno degli schemi di consenso creati in precedenza. Facoltativamente, puoi utilizzare la barra di ricerca per limitare i risultati e individuare più facilmente lo schema. Seleziona il pulsante di scelta accanto allo schema desiderato, quindi seleziona **[!UICONTROL Avanti]** per continuare.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

Viene visualizzato il passaggio **[!UICONTROL Configura set di dati]** . Fornisci un nome e una descrizione univoci e facilmente identificabili per il set di dati prima di selezionare **[!UICONTROL Fine]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

Viene visualizzata la pagina dei dettagli per il set di dati appena creato. Se il set di dati è basato sullo schema delle serie temporali, il processo è completo. Se il set di dati è basato sullo schema dei record, il passaggio finale del processo consiste nell’abilitare il set di dati per l’utilizzo in [!DNL Real-time Customer Profile].

Nella barra a destra, seleziona l’opzione **[!UICONTROL Profilo]** , quindi seleziona **[!UICONTROL Abilita]** nel puntatore di conferma per abilitare lo schema per [!DNL Profile].

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

Per creare l’altro set di dati necessario per la conformità a TCF 2.0, segui nuovamente i passaggi indicati sopra.

## Passaggi successivi

Seguendo questa esercitazione, hai creato due set di dati che possono essere utilizzati per raccogliere i dati di consenso dei clienti:

* Un set di dati basato su record abilitato per l’utilizzo in Profilo cliente in tempo reale.
* Set di dati basato su serie temporale non abilitato per [!DNL Profile].

Ora puoi tornare alla [panoramica IAB TCF 2.0](./overview.md#merge-policies) per continuare il processo di configurazione di Platform per la conformità a TCF 2.0.
