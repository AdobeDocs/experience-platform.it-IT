---
keywords: Experience Platform;home;IAB;IAB 2.0;consenso;consenso
solution: Experience Platform
title: Creare set di dati per l’acquisizione dei dati di consenso IAB TCF 2.0
topic-legacy: privacy events
description: Questo documento fornisce passaggi per impostare i due set di dati necessari per raccogliere i dati di consenso IAB TCF 2.0.
exl-id: 36b2924d-7893-4c55-bc33-2c0234f1120e
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 0%

---

# Creare set di dati per l’acquisizione dei dati di consenso IAB TCF 2.0

Affinché Adobe Experience Platform possa elaborare i dati di consenso dei clienti in conformità a IAB [!DNL Transparency & Consent Framework] (TCF) 2.0, tali dati devono essere inviati ai set di dati i cui schemi contengono campi di consenso TCF 2.0.

In particolare, per acquisire i dati di consenso TCF 2.0 sono necessari due set di dati:

* Un set di dati basato sulla classe [!DNL XDM Individual Profile], abilitato per l’utilizzo in [!DNL Real-time Customer Profile].
* Un set di dati basato sulla classe [!DNL XDM ExperienceEvent] .

Questo documento fornisce passaggi per impostare questi due set di dati per raccogliere i dati di consenso IAB TCF 2.0. Per una panoramica dell’intero flusso di lavoro per configurare le operazioni relative ai dati della piattaforma per TCF 2.0, consulta la [panoramica sulla conformità IAB TCF 2.0](./overview.md).

## Prerequisiti

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Experience Data Model (XDM)](../../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM.
* [Servizio](../../../../identity-service/home.md) Adobe Experience Platform Identity: Consente di collegare le identità dei clienti da diverse origini dati tra dispositivi e sistemi.
   * [Namespace](../../../../identity-service/namespaces.md) di identità: I dati di identità cliente devono essere forniti in uno spazio dei nomi di identità specifico riconosciuto dal servizio Identity.
* [Profilo](../../../../profile/home.md) cliente in tempo reale: Utilizza  [!DNL Identity Service] per creare in tempo reale profili cliente dettagliati dai set di dati. [!DNL Real-time Customer Profile] richiama i dati dal Data Lake e persiste i profili dei clienti nel proprio archivio dati separato.

## [!UICONTROL Privacy Details] struttura del gruppo di campi  {#structure}

Il gruppo di campi dello schema [!UICONTROL Privacy Details] fornisce i campi di consenso dei clienti richiesti per il supporto TCF 2.0. Sono disponibili due versioni di questo gruppo di campi: uno compatibile con la classe [!DNL XDM Individual Profile] e l&#39;altro con la classe [!DNL XDM ExperienceEvent].

Le sezioni seguenti illustrano la struttura di ciascuno di questi gruppi di campi, compresi i dati attesi durante l’acquisizione.

### Gruppo di campi del profilo {#profile-field-group}

Per gli schemi basati su [!DNL XDM Individual Profile], il gruppo di campi [!UICONTROL Privacy Details] fornisce un singolo campo di tipo mappa, `xdm:identityPrivacyInfo`, che mappa le identità dei clienti alle loro preferenze di consenso TCF. Il seguente JSON è un esempio del tipo di dati che `xdm:identityPrivacyInfo` prevede durante l’inserimento dei dati:

```json
{
  "xdm:identityPrivacyInfo": {
      "ECID": {
        "13782522493631189": {
          "xdm:identityIABConsent": {
            "xdm:consentTimestamp": "2020-04-11T05:05:05Z",
            "xdm:consentString": {
              "xdm:consentStandard": "IAB TCF",
              "xdm:consentStandardVersion": "2.0",
              "xdm:consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
              "xdm:gdprApplies": true,
              "xdm:containsPersonalData": false
            }
          }
        }
      }
    }
}
```

Come illustrato nell’esempio, ogni chiave a livello principale di `xdm:identityPrivacyInfo` corrisponde a uno spazio dei nomi di identità riconosciuto dal servizio Identity. A sua volta, ogni proprietà dello spazio dei nomi deve avere almeno una sottoproprietà la cui chiave corrisponde al valore di identità corrispondente del cliente per tale spazio dei nomi. In questo esempio, il cliente è identificato con un valore ID Experience Cloud (`ECID`) di `13782522493631189`.

>[!NOTE]
>
>Sebbene l’esempio precedente utilizzi una singola coppia di namespace/valori per rappresentare l’identità del cliente, puoi aggiungere altre chiavi per altri namespace e ogni namespace può avere più valori di identità, ciascuno con il proprio set di preferenze di consenso TCF.

All&#39;interno dell&#39;oggetto valore identity si trova un singolo campo, `xdm:identityIABConsent`. Questo oggetto acquisisce i valori di consenso TCF del cliente per lo spazio dei nomi e il valore dell&#39;identità specificati. Le sottoproprietà contenute in questo campo sono elencate di seguito:

| Proprietà | Descrizione |
| --- | --- |
| `xdm:consentTimestamp` | Una marca temporale [ISO 8601](https://www.ietf.org/rfc/rfc3339.txt) di quando i valori di consenso TCF sono cambiati. |
| `xdm:consentString` | Un oggetto contenente i dati di consenso aggiornati del cliente e altre informazioni contestuali. Per informazioni sulle proprietà secondarie obbligatorie di questo oggetto, consulta la sezione sulle [proprietà della stringa di consenso](#consent-string) . |

### Gruppo di campi evento {#event-field-group}

Per gli schemi basati su [!DNL XDM ExperienceEvent], il gruppo di campi [!UICONTROL Privacy Details] fornisce un singolo campo di tipo matrice: `xdm:consentStrings`. Ogni elemento in questa matrice deve essere un oggetto che contiene le proprietà necessarie per una stringa di consenso TCF, simile al campo `xdm:consentString` nel gruppo di campi del profilo. Per ulteriori informazioni su queste proprietà secondarie, consulta la sezione [successiva](#consent-string).

```json
{
  "xdm:consentStrings": [
    {
      "xdm:consentStandard": "IAB TCF",
      "xdm:consentStandardVersion": "2.0",
      "xdm:consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
      "xdm:gdprApplies": true,
      "xdm:containsPersonalData": false
    }
  ]
}
```

### Proprietà della stringa di consenso {#consent-string}

Entrambe le versioni del gruppo di campi [!UICONTROL Privacy Details] richiedono almeno un oggetto che acquisisca i campi necessari che descrivano la stringa di consenso TCF per il cliente. Queste proprietà sono spiegate di seguito:

| Proprietà | Descrizione |
| --- | --- |
| `xdm:consentStandard` | Il framework di consenso a cui si applicano i dati. Per la conformità TCF, il valore deve essere `IAB TCF`. |
| `xdm:consentStandardVersion` | Numero di versione del framework di consenso indicato da `xdm:consentStandard`. Per la conformità a TCF 2.0, il valore deve essere `2.0`. |
| `xdm:consentStringValue` | Stringa di consenso generata dalla piattaforma di gestione dei consensi (CMP) in base alle impostazioni selezionate del cliente. |
| `xdm:gdprApplies` | Un valore booleano che indica se il RGPD è applicabile o meno a questo cliente. Il valore deve essere impostato su `true` per consentire l’applicazione di TCF 2.0. Valori predefiniti in `true` se non sono inclusi. |
| `xdm:containsPersonalData` | Un valore booleano che indica se l’aggiornamento del consenso contiene o meno dati personali. Valori predefiniti in `false` se non sono inclusi. |

## Creare schemi di consenso dei clienti {#create-schemas}

Per creare set di dati che acquisiscano i dati di consenso, devi prima creare schemi XDM su cui basare tali set di dati.

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Schemas]** nel menu di navigazione a sinistra per aprire l’area di lavoro [!UICONTROL Schemas]. Da qui, segui i passaggi descritti nelle sezioni seguenti per creare ogni schema richiesto.

>[!NOTE]
>
>Se disponi di schemi XDM esistenti che desideri utilizzare per acquisire i dati di consenso, puoi modificarli invece di crearne di nuovi. Tuttavia, se uno schema esistente è stato abilitato per l’utilizzo in Profilo cliente in tempo reale, la sua identità principale non può essere un campo direttamente identificabile che non è consentito utilizzare nella pubblicità basata su interessi, ad esempio un indirizzo e-mail. Consulta il tuo consulente legale se non sei sicuro di quali campi siano soggetti a restrizioni.
>
>Inoltre, quando si modificano gli schemi esistenti, è possibile apportare solo modifiche aggiuntive (non rivoluzionarie). Per ulteriori informazioni, consulta la sezione sui [principi dell&#39;evoluzione dello schema](../../../../xdm/schema/composition.md#evolution) .

### Creare uno schema di consenso basato su record {#profile-schema}

Nell’area di lavoro **[!UICONTROL Schemas]**, seleziona **[!UICONTROL Create schema]**, quindi scegli **[!UICONTROL XDM Individual Profile]** dal menu a discesa.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

Viene visualizzata la sezione [!DNL Schema Editor] che mostra la struttura dello schema nell’area di lavoro. Utilizza la barra a destra per fornire un nome e una descrizione per lo schema, quindi seleziona **[!UICONTROL Add]** nella sezione **[!UICONTROL Field groups]** sul lato sinistro dell’area di lavoro.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-profile.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Add field groups]**. Da qui, seleziona **[!UICONTROL Privacy Details]** dall’elenco. Facoltativamente, puoi utilizzare la barra di ricerca per limitare i risultati per individuare più facilmente il gruppo di campi. Una volta selezionato il gruppo di campi, selezionare **[!UICONTROL Add field groups]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

L’area di lavoro viene visualizzata nuovamente, mostrando che il campo `identityPrivacyInfo` è stato aggiunto alla struttura dello schema.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

Da qui, ripeti i passaggi precedenti per aggiungere i seguenti gruppi di campi aggiuntivi allo schema:

* [!UICONTROL IdentityMap]
* [!UICONTROL Data capture region for Profile]
* [!UICONTROL Demographic Details]
* [!UICONTROL Personal Contact Details]

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-all-field-groups.png)

Se stai modificando uno schema esistente che è già stato abilitato per l&#39;utilizzo in [!DNL Real-time Customer Profile], seleziona **[!UICONTROL Save]** per confermare le modifiche prima di passare alla sezione relativa alla creazione di un set di dati in base allo schema di consenso](#dataset). [ Se stai creando un nuovo schema, continua a seguire i passaggi descritti nella sottosezione seguente.

#### Abilita lo schema da utilizzare in [!DNL Real-time Customer Profile]

Affinché Platform possa associare i dati di consenso ricevuti a profili cliente specifici, è necessario che lo schema di consenso sia abilitato per l’utilizzo in [!DNL Real-time Customer Profile].

>[!NOTE]
>
>Lo schema di esempio mostrato in questa sezione utilizza il relativo campo `identityMap` come identità principale. Se desideri impostare un altro campo come identità principale, accertati di utilizzare un identificatore indiretto come un ID cookie e non un campo direttamente identificabile che non è possibile utilizzare nella pubblicità basata su interessi, ad esempio un indirizzo e-mail. Consulta il tuo consulente legale se non sei sicuro di quali campi siano soggetti a restrizioni.
>
>I passaggi su come impostare un campo di identità principale per uno schema si trovano nell&#39;esercitazione [creazione dello schema](../../../../xdm/tutorials/create-schema-ui.md#identity-field).

Per abilitare lo schema per [!DNL Profile], seleziona il nome dello schema nella barra a sinistra per aprire la finestra di dialogo **[!UICONTROL Schema properties]** nella barra a destra. Da qui, seleziona il pulsante di attivazione/disattivazione **[!UICONTROL Profile]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

Viene visualizzato un puntatore che indica un&#39;identità principale mancante. Seleziona la casella di controllo per utilizzare un&#39;identità principale alternativa, in quanto l&#39;identità principale sarà contenuta nel campo `identityMap` .

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

Infine, seleziona **[!UICONTROL Save]** per confermare le modifiche.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### Creare uno schema di consenso basato su serie temporali {#event-schema}

Nell’area di lavoro **[!UICONTROL Schemas]**, seleziona **[!UICONTROL Create schema]**, quindi scegli **[!UICONTROL XDM ExperienceEvent]** dal menu a discesa.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

Viene visualizzata la sezione [!DNL Schema Editor] che mostra la struttura dello schema nell’area di lavoro. Utilizza la barra a destra per fornire un nome e una descrizione per lo schema, quindi seleziona **[!UICONTROL Add]** nella sezione **[!UICONTROL Field groups]** sul lato sinistro dell’area di lavoro.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-event.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Add field groups]**. Da qui, seleziona **[!UICONTROL Privacy Details]** dall’elenco. Facoltativamente, puoi utilizzare la barra di ricerca per limitare i risultati per individuare più facilmente il gruppo di campi. Dopo aver selezionato un gruppo di campi, selezionare **[!UICONTROL Add field groups]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

L’area di lavoro viene visualizzata nuovamente, mostrando che la matrice `consentStrings` è stata aggiunta alla struttura dello schema.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

Da qui, ripeti i passaggi precedenti per aggiungere i seguenti gruppi di campi aggiuntivi allo schema:

* [!UICONTROL IdentityMap]
* [!UICONTROL Environment Details]
* [!UICONTROL Web Details]
* [!UICONTROL Implementation Details]

Una volta aggiunti i gruppi di campi, terminare selezionando **[!UICONTROL Save]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-field-groups.png)

## Crea set di dati in base agli schemi di consenso {#datasets}

Per ciascuno degli schemi richiesti sopra descritti, devi creare un set di dati che in definitiva acquisirà i dati di consenso dei clienti. Il set di dati basato sullo schema del record deve essere abilitato per [!DNL Real-time Customer Profile], mentre il set di dati basato sullo schema delle serie temporali **non deve essere** abilitato.[!DNL Profile]

Per iniziare, seleziona **[!UICONTROL Datasets]** nel menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Create dataset]** nell’angolo in alto a destra.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

Nella pagina successiva, seleziona **[!UICONTROL Create dataset from schema]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

Viene visualizzato il flusso di lavoro **[!UICONTROL Create dataset from schema]** a partire dal passaggio **[!UICONTROL Select schema]** . Nell’elenco fornito, individua uno degli schemi di consenso creati in precedenza. Facoltativamente, puoi utilizzare la barra di ricerca per limitare i risultati e individuare più facilmente lo schema. Seleziona il pulsante di scelta accanto allo schema desiderato, quindi seleziona **[!UICONTROL Next]** per continuare.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

Viene visualizzato il passaggio **[!UICONTROL Configure dataset]** . Fornisci un nome e una descrizione univoci e facilmente identificabili per il set di dati prima di selezionare **[!UICONTROL Finish]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

Viene visualizzata la pagina dei dettagli per il set di dati appena creato. Se il set di dati è basato sullo schema delle serie temporali, il processo è completo. Se il set di dati è basato sullo schema dei record, il passaggio finale del processo consiste nell’abilitare il set di dati per l’utilizzo in [!DNL Real-time Customer Profile].

Nella barra a destra, seleziona l’interruttore **[!UICONTROL Profile]**, quindi seleziona **[!UICONTROL Enable]** nel puntatore di conferma per abilitare lo schema per [!DNL Profile].

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

Per creare l’altro set di dati necessario per la conformità a TCF 2.0, segui nuovamente i passaggi indicati sopra.

## Passaggi successivi

Seguendo questa esercitazione, hai creato due set di dati che possono essere utilizzati per raccogliere i dati di consenso dei clienti:

* Un set di dati basato su record abilitato per l’utilizzo in Profilo cliente in tempo reale.
* Set di dati basato su serie temporale non abilitato per [!DNL Profile].

Ora puoi tornare alla [panoramica IAB TCF 2.0](./overview.md#merge-policies) per continuare il processo di configurazione di Platform per la conformità a TCF 2.0.
