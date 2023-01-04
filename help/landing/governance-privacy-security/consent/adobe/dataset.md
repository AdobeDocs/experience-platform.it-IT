---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Configurare un set di dati per acquisire dati di consenso e preferenza
topic-legacy: getting started
description: Scopri come configurare uno schema e un set di dati Experience Data Model (XDM) per acquisire i dati di consenso e preferenza in Adobe Experience Platform.
exl-id: 61ceaa2a-c5ac-43f5-b118-502bdc432234
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---

# Configurare un set di dati per acquisire dati di consenso e preferenza

Affinché Adobe Experience Platform possa elaborare i dati di consenso o preferenza dei clienti, questi devono essere inviati a un set di dati il cui schema contiene campi relativi ai consensi e ad altre autorizzazioni. In particolare, questo set di dati deve essere basato su [!DNL XDM Individual Profile] e abilitata per l&#39;uso in [!DNL Real-Time Customer Profile].

Questo documento fornisce passaggi per la configurazione di un set di dati per elaborare i dati di consenso in Experience Platform. Per una panoramica dell’intero flusso di lavoro per l’elaborazione dei dati di consenso/preferenza in Platform, consulta la [panoramica dell&#39;elaborazione del consenso](./overview.md).

>[!IMPORTANT]
>
>Gli esempi in questa guida utilizzano un set standardizzato di campi per rappresentare i valori del consenso del cliente, come definito dalla [[!UICONTROL Dettagli su consenso e preferenza] gruppo di campi schema](../../../../xdm/field-groups/profile/consents.md). La struttura di questi campi è intesa a fornire un modello di dati efficiente che copra molti casi d’uso comuni per la raccolta del consenso.
>
>Tuttavia, puoi anche definire gruppi di campi personalizzati per rappresentare il consenso in base ai tuoi modelli di dati. Consulta il tuo team legale per ottenere l’approvazione per un modello di dati di consenso adatto alle tue esigenze aziendali, in base alle seguenti opzioni:
>
>* Gruppo di campi di consenso standardizzato
>* Un gruppo di campi di consenso personalizzato creato dalla tua organizzazione
>* Combinazione del gruppo di campi di consenso standardizzato e dei campi aggiuntivi forniti da un gruppo di campi di consenso personalizzato


## Prerequisiti

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Experience Data Model (XDM)](../../../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM.
* [Profilo cliente in tempo reale](../../../../profile/home.md): Consolida i dati dei clienti provenienti da fonti diverse in una visualizzazione completa e unificata, offrendo al tempo stesso un account utilizzabile e con marca temporale per ogni interazione con il cliente.

>[!IMPORTANT]
>
>Questa esercitazione presuppone che tu conosca il [!DNL Profile] schema in Platform che desideri utilizzare per acquisire informazioni sugli attributi del cliente. Indipendentemente dal metodo utilizzato per raccogliere i dati di consenso, questo schema deve essere [abilitato per il profilo cliente in tempo reale](../../../../xdm/ui/resources/schemas.md#profile). Inoltre, l&#39;identità principale dello schema non può essere un campo direttamente identificabile che non è consentito utilizzare nella pubblicità basata sugli interessi, ad esempio un indirizzo e-mail. Consulta il tuo consulente legale se non sei sicuro di quali campi siano soggetti a restrizioni.

## [!UICONTROL Dettagli su consenso e preferenza] struttura del gruppo di campi {#structure}

La [!UICONTROL Dettagli su consenso e preferenza] gruppo di campi fornisce campi di consenso standardizzati a uno schema. Attualmente, questo gruppo di campi è compatibile solo con schemi basati su [!DNL XDM Individual Profile] classe.

Il gruppo di campi fornisce un singolo campo di tipo oggetto, `consents`, le cui sottoproprietà acquisiscono un set di campi di consenso standardizzati. Il seguente JSON è un esempio del tipo di dati `consents` si aspetta in seguito all’acquisizione dei dati:

```json
{
  "consents": {
    "collect": {
      "val": "y",
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "idSpecific": {
      "email": {
        "jdoe@example.com": {
          "marketing": {
            "email": {
              "val": "n"
            }
          }
        }
      }
    }
  },
  "metadata": {
    "time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>Per ulteriori informazioni sulla struttura e il significato delle sottoproprietà in `consents`, consulta la panoramica sul [[!UICONTROL Dettagli su consenso e preferenza] gruppo di campi](../../../../xdm/field-groups/profile/consents.md).

## Aggiungi i gruppi di campi richiesti al tuo [!DNL Profile] schema {#add-field-group}

Per raccogliere i dati di consenso utilizzando lo standard Adobe, è necessario disporre di uno schema abilitato per il profilo che contenga i due gruppi di campi seguenti:

* [!UICONTROL Dettagli su consenso e preferenza]
* [!UICONTROL IdentityMap] (richiesto se per inviare i segnali di consenso si utilizza Platform Web o Mobile SDK)

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Schemi]** nel menu di navigazione a sinistra, seleziona il **[!UICONTROL Sfoglia]** per visualizzare un elenco degli schemi esistenti. Da qui, seleziona il nome del [!DNL Profile]schema abilitato a cui si desidera aggiungere campi di consenso. Le schermate di questa sezione utilizzano lo schema &quot;Membri fedeltà&quot; generato nel [esercitazione sulla creazione dello schema](../../../../xdm/tutorials/create-schema-ui.md) come esempio.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-schema.png)

>[!TIP]
>
>È possibile utilizzare le funzionalità di ricerca e filtro dell&#39;area di lavoro per semplificare lo schema. Consulta la guida su [esplorazione delle risorse XDM](../../../../xdm/ui/explore.md) per ulteriori informazioni.

La [!DNL Schema Editor] viene visualizzata la struttura dello schema nell&#39;area di lavoro. Sul lato sinistro dell’area di lavoro, seleziona **[!UICONTROL Aggiungi]** in **[!UICONTROL Gruppi di campi]** sezione .

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-field-group.png)

La **[!UICONTROL Aggiungi gruppo di campi]** viene visualizzata la finestra di dialogo . Da qui, seleziona **[!UICONTROL Dettagli su consenso e preferenza]** dall&#39;elenco. Facoltativamente, puoi utilizzare la barra di ricerca per limitare i risultati per individuare più facilmente il gruppo di campi.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-group-dialog.png)

Quindi, trova il **[!UICONTROL IdentityMap]** gruppo di campi dall’elenco e selezionalo. Una volta elencati entrambi i gruppi di campi nella barra a destra, seleziona **[!UICONTROL Aggiungi gruppi di campi]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/identitymap.png)

L&#39;area di lavoro viene visualizzata nuovamente, mostrando che la `consents` e `identityMap` i campi sono stati aggiunti alla struttura dello schema. Se hai bisogno di ulteriori campi di consenso e preferenza non acquisiti dal gruppo di campi standard, consulta la sezione appendice su [aggiunta di campi di consenso e preferenza personalizzati allo schema](#custom-consent). In caso contrario, seleziona **[!UICONTROL Salva]** per finalizzare le modifiche allo schema.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/save-schema.png)

>[!IMPORTANT]
>
>Se crei un nuovo schema o ne modifichi uno esistente che non è stato abilitato per il profilo, devi [abilitare lo schema per il profilo](../../../../xdm/ui/resources/schemas.md#profile) prima del salvataggio.

Se lo schema modificato viene utilizzato dalla [!UICONTROL Set di dati del profilo] specificato nel datastream dell’SDK per web di Platform, tale set di dati ora includerà i nuovi campi di consenso. Ora puoi tornare alla sezione [guida all’elaborazione del consenso](./overview.md#merge-policies) per continuare il processo di configurazione di Experience Platform per elaborare i dati di consenso. Se non hai creato un set di dati per questo schema, segui i passaggi della sezione successiva.

## Creare un set di dati basato sullo schema di consenso {#dataset}

Dopo aver creato uno schema con i campi di consenso, devi creare un set di dati che in ultima analisi acquisirà i dati di consenso dei clienti. Questo set di dati deve essere abilitato per [!DNL Real-Time Customer Profile].

Per iniziare, seleziona **[!UICONTROL Set di dati]** nel menu di navigazione a sinistra, seleziona **[!UICONTROL Creare un set di dati]** nell&#39;angolo in alto a destra.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/create-dataset.png)

Nella pagina successiva, seleziona **[!UICONTROL Creare un set di dati dallo schema]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/from-schema.png)

La **[!UICONTROL Creare un set di dati dallo schema]** viene visualizzato il flusso di lavoro, a partire dalla **[!UICONTROL Seleziona schema]** passo. Nell’elenco fornito, individua uno degli schemi di consenso creati in precedenza. Facoltativamente, puoi utilizzare la barra di ricerca per limitare i risultati e individuare più facilmente lo schema. Seleziona il pulsante di scelta accanto allo schema desiderato, quindi seleziona **[!UICONTROL Successivo]** per continuare.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-dataset-schema.png)

La **[!UICONTROL Configurare il set di dati]** viene visualizzato il passaggio . Fornisci un nome e una descrizione univoci e facilmente identificabili per il set di dati prima di selezionarli **[!UICONTROL Fine]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/dataset-details.png)

Viene visualizzata la pagina dei dettagli per il set di dati appena creato. Se il set di dati è basato sullo schema delle serie temporali, il processo è completo. Se il set di dati è basato sullo schema del record, il passaggio finale del processo consiste nell’abilitare il set di dati per l’utilizzo in [!DNL Real-Time Customer Profile].

Nella barra a destra, seleziona la **[!UICONTROL Profilo]** alternare.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/profile-toggle.png)

Infine, seleziona **[!UICONTROL Abilita]** nel percorso di conferma per abilitare lo schema per [!DNL Profile].

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/enable-dataset.png)

Il set di dati viene ora salvato e abilitato per l’utilizzo in [!DNL Profile]. Se prevedi di utilizzare Platform Web SDK per inviare i dati di consenso a Profilo, devi selezionare questo set di dati come [!UICONTROL Set di dati del profilo] quando si configura il [datastream](../../../../edge/datastreams/overview.md).

## Passaggi successivi

Seguendo questa esercitazione hai aggiunto i campi di consenso a un [!DNL Profile]schema abilitato, il cui set di dati verrà utilizzato per acquisire i dati di consenso tramite l’SDK per web di Platform o per l’acquisizione diretta XDM.

Ora puoi tornare alla sezione [panoramica dell&#39;elaborazione del consenso](./overview.md#merge-policies) per continuare a configurare Experience Platform per l’elaborazione dei dati di consenso.

## Appendice

La sezione seguente contiene informazioni aggiuntive sulla creazione di un set di dati per acquisire i dati di consenso e preferenza dei clienti.

### Aggiungere campi di consenso e preferenza personalizzati allo schema {#custom-consent}

Se devi acquisire segnali di consenso aggiuntivi al di fuori di quelli rappresentati dallo standard [!UICONTROL Dettagli su consenso e preferenza] gruppo di campi, puoi utilizzare componenti XDM personalizzati per migliorare lo schema dei consensi in base a specifiche esigenze aziendali. Questa sezione descrive i principi di base su come personalizzare lo schema del consenso per acquisire questi segnali in Profilo.

>[!IMPORTANT]
>
>Gli SDK per web e dispositivi mobili di Platform non supportano campi personalizzati nei loro comandi di modifica del consenso. Attualmente l’unico modo per acquisire i campi di consenso personalizzati in Profilo è tramite [ingestione in batch](../../../../ingestion/batch-ingestion/overview.md) o [connessione sorgente](../../../../sources/home.md).

Si consiglia vivamente di utilizzare il [!UICONTROL Dettagli su consenso e preferenza] gruppo di campi come linea di base per la struttura dei dati di consenso e aggiungi altri campi in base alle esigenze, anziché tentare di creare l’intera struttura da zero.

Per aggiungere campi personalizzati alla struttura di un gruppo di campi standard, è innanzitutto necessario creare un gruppo di campi personalizzato. Dopo l’aggiunta della [!UICONTROL Dettagli su consenso e preferenza] gruppo di campi nello schema, seleziona il **più (+)** nella **[!UICONTROL Gruppi di campi]** , quindi seleziona **[!UICONTROL Crea nuovo gruppo di campi]**. Fornire un nome e una descrizione facoltative per il gruppo di campi, quindi selezionare **[!UICONTROL Aggiungi gruppo di campi]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field-group.png)

La [!DNL Schema Editor] viene visualizzato nuovamente con il nuovo gruppo di campi personalizzati selezionato nella barra a sinistra. Nell’area di lavoro sono visualizzati controlli che consentono di aggiungere campi personalizzati alla struttura dello schema. Per aggiungere un nuovo campo di consenso o preferenza, seleziona la **più (+)** accanto all’icona `consents` oggetto.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field.png)

All’interno del campo viene visualizzato un nuovo campo `consents` oggetto. Poiché si aggiunge un campo personalizzato a un oggetto XDM standard, il nuovo campo viene creato sotto un oggetto con namespace nell’ID tenant.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/nested-tenantId.png)

Nella barra a destra sotto **[!UICONTROL Proprietà campo]**, fornisci un nome e una descrizione per il campo. Quando si selezionano i campi **[!UICONTROL Tipo]**, devi utilizzare il tipo di dati standard appropriato per un campo di autorizzazione o preferenza personalizzato:

* [[!UICONTROL Campo di consenso generico]](../../../../xdm/data-types/consent-field.md)
* [[!UICONTROL Campo preferenza marketing generico]](../../../../xdm/data-types/marketing-field.md)
* [[!UICONTROL Campo preferenza marketing generico con sottoscrizioni]](../../../../xdm/data-types/marketing-field-subscriptions.md)
* [[!UICONTROL Campo preferenza personalizzazione generica]](../../../../xdm/data-types/personalization-field.md)

Al termine, seleziona **[!UICONTROL Applica]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-properties.png)

Il campo di consenso o preferenza viene aggiunto alla struttura dello schema. Tieni presente che [!UICONTROL Percorso] visualizzato nella barra a destra contiene `_tenantId` spazio dei nomi. Questo spazio dei nomi deve essere incluso ogni volta che si fa riferimento al percorso di questo campo nelle operazioni sui dati.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-added.png)

Per continuare ad aggiungere i campi di consenso e preferenza richiesti, procedi come indicato sopra. Al termine, seleziona **[!UICONTROL Salva]** per confermare le modifiche.

Se non hai creato un set di dati per questo schema, continua alla sezione in [creazione di un set di dati](#dataset).
