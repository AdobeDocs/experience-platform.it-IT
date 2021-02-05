---
keywords: Experience Platform ;home;IAB;IAB 2.0;consenso;consenso
solution: Experience Platform
title: Creazione di set di dati per l'acquisizione dei dati di consenso IAB TCF 2.0
topic: privacy events
description: Questo documento fornisce i passaggi per impostare i due insiemi di dati richiesti per la raccolta dei dati di consenso IAB TCF 2.0.
translation-type: tm+mt
source-git-commit: b0af9d49f6cfe50f6dff745dfac174dbaa76d070
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 0%

---


# Creazione di set di dati per l&#39;acquisizione dei dati di consenso IAB TCF 2.0

Affinché Adobe Experience Platform possa elaborare i dati di consenso dei clienti in conformità allo IAB [!DNL Transparency & Consent Framework] (TCF) 2.0, tali dati devono essere inviati a insiemi di dati i cui schemi contengono campi di consenso TCF 2.0.

In particolare, per acquisire i dati di consenso di TCF 2.0 sono necessari due set di dati:

* Un dataset basato sulla classe [!DNL XDM Individual Profile], abilitato per l&#39;uso in [!DNL Real-time Customer Profile].
* Un dataset basato sulla classe [!DNL XDM ExperienceEvent].

Questo documento fornisce i passaggi per impostare questi due insiemi di dati per la raccolta dei dati di consenso IAB TCF 2.0. Per una panoramica del flusso di lavoro completo per configurare le operazioni dei dati della piattaforma per TCF 2.0, fare riferimento alla [panoramica sulla conformità IAB TCF 2.0](./overview.md).

## Prerequisiti

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Experience Data Model (XDM)](../../../../xdm/home.md): Il framework standard con cui  [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../xdm/schema/composition.md) dello schema: Informazioni sui blocchi di base degli schemi XDM.
* [Servizio](../../../../identity-service/home.md) identità Adobe Experience Platform: Consente di collegare le identità dei clienti da origini dati diverse tra dispositivi e sistemi.
   * [Spazi dei nomi](../../../../identity-service/namespaces.md) di identità: I dati di identità del cliente devono essere forniti in uno specifico namespace di identità riconosciuto da Servizio identità.
* [Profilo](../../../../profile/home.md) cliente in tempo reale: Consente  [!DNL Identity Service] di creare profili cliente dettagliati dai set di dati in tempo reale. [!DNL Real-time Customer Profile] estrae i dati dal Data Lake e persiste nei profili dei clienti nel proprio archivio dati separato.

## [!UICONTROL Privacy Details] struttura di miscelazione  {#structure}

Il mixin [!UICONTROL Privacy Details] fornisce i campi di consenso dei clienti richiesti per il supporto di TCF 2.0. Esistono due versioni di questo mixin: uno compatibile con la classe [!DNL XDM Individual Profile] e l&#39;altro con la classe [!DNL XDM ExperienceEvent].

Le sezioni seguenti illustrano la struttura di ciascuna di queste miscele, compresi i dati che si aspettano durante l&#39;assimilazione.

### Mixin profilo {#profile-mixin}

Per gli schemi basati su [!DNL XDM Individual Profile], il mixin [!UICONTROL Privacy Details] fornisce un campo di tipo mappa singolo, `xdm:identityPrivacyInfo`, che associa le identità dei clienti alle loro preferenze di consenso TCF. Il seguente JSON è un esempio del tipo di dati previsto `xdm:identityPrivacyInfo` al momento dell&#39;assimilazione dei dati:

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

Come illustrato nell&#39;esempio, ogni chiave a livello principale di `xdm:identityPrivacyInfo` corrisponde a uno spazio dei nomi di identità riconosciuto da Servizio identità. A sua volta, ogni proprietà namespace deve avere almeno una sottoproprietà la cui chiave corrisponda al valore di identità corrispondente del cliente per tale spazio nomi. In questo esempio, il cliente è identificato con un ID Experience Cloud  (`ECID`) di `13782522493631189`.

>[!NOTE]
>
>Anche se nell&#39;esempio precedente viene utilizzata una coppia di nomi/valori per rappresentare l&#39;identità del cliente, è possibile aggiungere ulteriori chiavi per altri spazi dei nomi, e ogni spazio dei nomi può avere più valori di identità, ciascuno con un proprio set di preferenze di consenso TCF.

All&#39;interno dell&#39;oggetto valore identità è presente un singolo campo, `xdm:identityIABConsent`. Questo oggetto acquisisce i valori di consenso TCF del cliente per lo spazio dei nomi e il valore dell&#39;identità specificati. Le proprietà secondarie contenute in questo campo sono elencate di seguito:

| Proprietà | Descrizione |
| --- | --- |
| `xdm:consentTimestamp` | Un timestamp [ISO 8601](https://www.ietf.org/rfc/rfc3339.txt) di quando i valori di consenso TCF sono cambiati. |
| `xdm:consentString` | Un oggetto contenente i dati di consenso aggiornati del cliente e altre informazioni contestuali. Vedere la sezione relativa alle proprietà della stringa di consenso [per informazioni sulle proprietà secondarie richieste per questo oggetto.](#consent-string) |

### Mixin evento {#event-mixin}

Per gli schemi basati su [!DNL XDM ExperienceEvent], il mixin [!UICONTROL Privacy Details] fornisce un singolo campo di tipo array: `xdm:consentStrings`. Ciascun elemento in questa matrice deve essere un oggetto che contiene le proprietà necessarie per una stringa di consenso TCF, simile al campo `xdm:consentString` nel mixin del profilo. Per ulteriori informazioni su queste proprietà secondarie, vedere la sezione [successiva](#consent-string).

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

### Consenso delle proprietà delle stringhe {#consent-string}

Entrambe le versioni del mixin [!UICONTROL Privacy Details] richiedono almeno un oggetto che acquisisca i campi necessari che descrivano la stringa di consenso TCF per il cliente. Queste proprietà sono spiegate di seguito:

| Proprietà | Descrizione |
| --- | --- |
| `xdm:consentStandard` | Quadro di consenso a cui si applicano i dati. Per la conformità TCF, il valore deve essere `IAB TCF`. |
| `xdm:consentStandardVersion` | Numero di versione del framework di autorizzazione indicato da `xdm:consentStandard`. Per garantire la conformità a TCF 2.0, il valore deve essere `2.0`. |
| `xdm:consentStringValue` | Stringa di consenso generata dalla piattaforma di gestione del consenso (CMP) in base alle impostazioni selezionate dal cliente. |
| `xdm:gdprApplies` | Un valore booleano che indica se il GDPR si applica o meno a questo cliente. Il valore deve essere impostato su `true` per consentire l&#39;applicazione di TCF 2.0. Il valore predefinito è `false` se non è incluso. |
| `xdm:containsPersonalData` | Valore booleano che indica se l&#39;aggiornamento del consenso contiene o meno dati personali. Il valore predefinito è `false` se non è incluso. |

## Creare schemi di consenso dei clienti {#create-schemas}

Per creare insiemi di dati che acquisiscano i dati di consenso, è innanzitutto necessario creare schemi XDM su cui basare tali set di dati.

Nell&#39;interfaccia utente della piattaforma, selezionare **[!UICONTROL Schemas]** nel menu di navigazione a sinistra per aprire l&#39;area di lavoro [!UICONTROL Schemas]. Da qui, seguite i passaggi descritti nelle sezioni seguenti per creare ogni schema richiesto.

>[!NOTE]
>
>Se disponete di schemi XDM esistenti che desiderate utilizzare per acquisire i dati di consenso, potete modificare tali schemi invece di crearne di nuovi. Tuttavia, se uno schema esistente è stato abilitato per l&#39;uso in Real-time Customer Profile, la sua identità primaria non può essere un campo direttamente identificabile che non può essere utilizzato nella pubblicità basata sugli interessi, ad esempio un indirizzo e-mail. Se non sei sicuro di quali campi siano soggetti a restrizioni, consulta il tuo consulente legale.
>
>Inoltre, durante la modifica degli schemi esistenti, è possibile apportare solo modifiche aggiuntive (senza interruzioni). Per ulteriori informazioni, vedere la sezione sui [principi dell&#39;evoluzione dello schema](../../../../xdm/schema/composition.md#evolution).

### Creare uno schema di consenso basato su record {#profile-schema}

Nell&#39;area di lavoro **[!UICONTROL Schemas]**, selezionare **[!UICONTROL Create schema]**, quindi scegliere **[!UICONTROL XDM Individual Profile]** dal menu a discesa.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

Viene visualizzata la [!DNL Schema Editor] che mostra la struttura dello schema nel quadro. Utilizzate la barra a destra per specificare un nome e una descrizione per lo schema, quindi selezionate **[!UICONTROL Add]** nella sezione **[!UICONTROL Mixins]** sul lato sinistro del quadro.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-mixin-profile.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Add mixin]**. Da qui, selezionare **[!UICONTROL Privacy Details]** dall&#39;elenco. Facoltativamente, potete utilizzare la barra di ricerca per limitare i risultati e individuare più facilmente il mixin. Dopo aver selezionato il mixin, selezionare **[!UICONTROL Add mixin]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

L&#39;area di lavoro viene visualizzata nuovamente, mostrando che il campo `identityPrivacyInfo` è stato aggiunto alla struttura dello schema.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

Da qui, ripeti i passaggi indicati sopra per aggiungere allo schema i seguenti mixin aggiuntivi:

* [!UICONTROL IdentityMap]
* [!UICONTROL Data capture region for Profile]
* [!UICONTROL Demographic Details]
* [!UICONTROL Personal Contact Details]

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-all-mixins.png)

Se si sta modificando uno schema esistente che è già stato abilitato per l&#39;uso in [!DNL Real-time Customer Profile], selezionare **[!UICONTROL Save]** per confermare le modifiche prima di saltare in avanti alla sezione in [creazione di un dataset basato sullo schema di consenso](#dataset). Se si sta creando un nuovo schema, continuare a seguire i passaggi descritti nella sottosezione seguente.

#### Abilitare lo schema da utilizzare in [!DNL Real-time Customer Profile]

Affinché la piattaforma possa associare i dati di consenso ricevuti a specifici profili cliente, lo schema di consenso deve essere abilitato per l&#39;uso in [!DNL Real-time Customer Profile].

>[!NOTE]
>
>Lo schema di esempio mostrato in questa sezione utilizza il relativo campo `identityMap` come identità primaria. Se desiderate impostare un altro campo come identità primaria, accertatevi di utilizzare un identificatore indiretto, come un ID cookie, e non un campo direttamente identificabile che non può essere utilizzato nella pubblicità basata sugli interessi, come un indirizzo e-mail. Se non sei sicuro di quali campi siano soggetti a restrizioni, consulta il tuo consulente legale.
>
>Per informazioni su come impostare un campo di identità principale per uno schema, vedere l&#39;esercitazione sulla creazione dello schema [](../../../../xdm/tutorials/create-schema-ui.md#identity-field).

Per abilitare lo schema per [!DNL Profile], selezionare il nome dello schema nella barra a sinistra per aprire la finestra di dialogo **[!UICONTROL Schema properties]** nella barra a destra. Da qui, selezionare il pulsante **[!UICONTROL Profile]** di attivazione/disattivazione.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

Viene visualizzato un puntatore che indica un&#39;identità primaria mancante. Selezionate la casella di controllo per utilizzare un&#39;identità primaria alternativa, in quanto l&#39;identità principale sarà contenuta nel campo `identityMap`.

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

Infine, selezionare **[!UICONTROL Save]** per confermare le modifiche.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### Crea uno schema di consenso basato su serie temporale {#event-schema}

Nell&#39;area di lavoro **[!UICONTROL Schemas]**, selezionare **[!UICONTROL Create schema]**, quindi scegliere **[!UICONTROL XDM ExperienceEvent]** dal menu a discesa.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

Viene visualizzata la [!DNL Schema Editor] che mostra la struttura dello schema nel quadro. Utilizzate la barra a destra per specificare un nome e una descrizione per lo schema, quindi selezionate **[!UICONTROL Add]** nella sezione **[!UICONTROL Mixins]** sul lato sinistro del quadro.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-mixin-event.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Add mixin]**. Da qui, selezionare **[!UICONTROL Privacy Details]** dall&#39;elenco. Facoltativamente, potete utilizzare la barra di ricerca per limitare i risultati e individuare più facilmente il mixin. Dopo aver scelto un mixin, selezionare **[!UICONTROL Add mixin]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

L&#39;area di lavoro viene visualizzata di nuovo, mostrando che l&#39;array `consentStrings` è stato aggiunto alla struttura dello schema.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

Da qui, ripeti i passaggi indicati sopra per aggiungere allo schema i seguenti mixin aggiuntivi:

* [!UICONTROL IdentityMap]
* [!UICONTROL Environment Details]
* [!UICONTROL Web Details]
* [!UICONTROL Implementation Details]

Una volta aggiunti i mixin, terminare selezionando **[!UICONTROL Save]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-mixins.png)

## Creazione di set di dati in base agli schemi di consenso {#datasets}

Per ciascuno degli schemi richiesti precedentemente descritti, è necessario creare un set di dati che acquisisca in ultima istanza i dati di consenso dei clienti. Il dataset basato sullo schema del record deve essere abilitato per [!DNL Real-time Customer Profile], mentre il dataset basato sullo schema delle serie temporali **non deve essere** abilitato [!DNL Profile].

Per iniziare, selezionare **[!UICONTROL Datasets]** nella navigazione a sinistra, quindi selezionare **[!UICONTROL Create dataset]** nell&#39;angolo in alto a destra.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

Nella pagina successiva, selezionare **[!UICONTROL Create dataset from schema]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

Viene visualizzato il flusso di lavoro **[!UICONTROL Create dataset from schema]**, a partire dal passaggio **[!UICONTROL Select schema]**. Nell&#39;elenco fornito, individuare uno degli schemi di consenso creati in precedenza. Facoltativamente, è possibile utilizzare la barra di ricerca per limitare i risultati e individuare più facilmente lo schema. Selezionare il pulsante di scelta accanto allo schema desiderato, quindi selezionare **[!UICONTROL Next]** per continuare.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

Viene visualizzato il passaggio **[!UICONTROL Configure dataset]**. Specificare un nome e una descrizione univoci e facilmente identificabili per il dataset prima di selezionare **[!UICONTROL Finish]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

Viene visualizzata la pagina dei dettagli per il set di dati appena creato. Se il dataset è basato sullo schema delle serie temporali, il processo è completo. Se il set di dati è basato sullo schema del record, il passo finale del processo è quello di abilitare il set di dati per l&#39;utilizzo in [!DNL Real-time Customer Profile].

Nella barra a destra, selezionate l&#39;interruttore **[!UICONTROL Profile]**, quindi selezionate **[!UICONTROL Enable]** nel puntatore di conferma per attivare lo schema per [!DNL Profile].

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

Per creare l&#39;altro set di dati necessario per la conformità a TCF 2.0, eseguite nuovamente i passaggi indicati sopra.

## Passaggi successivi

Seguendo questa esercitazione, hai creato due set di dati che ora possono essere utilizzati per raccogliere i dati di consenso dei clienti:

* Set basato su record abilitato per l&#39;uso in Real-time Customer Profile (Profilo cliente in tempo reale).
* Set basato su serie temporale non abilitato per [!DNL Profile].

È ora possibile tornare alla [panoramica IAB TCF 2.0](./overview.md#merge-policies) per continuare il processo di configurazione della piattaforma per la conformità a TCF 2.0.