---
title: Elimina record
description: Scopri come eliminare i record nell’interfaccia utente di Adobe Experience Platform.
badgeBeta: label="Beta" type="Informative"
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 9981f35732b041a92c5a371e727a8facb6636cf5
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 8%

---

# Elimina record {#record-delete}

Utilizza l&#39;area di lavoro [[!UICONTROL Ciclo di vita dati]](./overview.md) per eliminare i record in Adobe Experience Platform in base alle loro identità primarie. Questi record possono essere associati a singoli consumatori o a qualsiasi altra entità inclusa nel grafico delle identità.

>[!IMPORTANT]
> 
>La funzionalità di eliminazione dei record è attualmente disponibile in Beta ed è disponibile solo in una **versione limitata**. Non è disponibile per tutti i clienti. Le richieste di cancellazione dei record sono disponibili solo per le organizzazioni nella versione limitata.
> 
> 
>Le eliminazioni di record devono essere utilizzate per la pulizia dei dati, la rimozione di dati anonimi o la minimizzazione dei dati. Sono **not** da utilizzare per le richieste di diritti degli interessati (conformità) in relazione alle normative sulla privacy come il Regolamento generale sulla protezione dei dati (RGPD). Per tutti i casi di utilizzo di conformità, utilizzare [Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

## Prerequisiti {#prerequisites}

L’eliminazione dei record richiede una buona conoscenza del funzionamento dei campi di identità in Experience Platform. In particolare, devi conoscere i valori dello spazio dei nomi delle identità delle entità di cui desideri eliminare i record, a seconda del set di dati (o dei set di dati) da cui li stai eliminando.

Per ulteriori informazioni sulle identità in Platform, consulta la seguente documentazione:

* [Servizio Adobe Experience Platform Identity](../../identity-service/home.md): collega le identità tra dispositivi e sistemi, collegando i set di dati in base ai campi di identità definiti dagli schemi XDM a cui sono conformi.
* [Spazi dei nomi di identità](../../identity-service/features/namespaces.md): gli spazi dei nomi di identità definiscono i diversi tipi di informazioni di identità che possono riferirsi a una singola persona e sono un componente obbligatorio per ogni campo di identità.
* [Profilo cliente in tempo reale](../../profile/home.md): utilizza i grafici delle identità per fornire profili di consumatori unificati basati su dati aggregati provenienti da più origini, aggiornati quasi in tempo reale.
* [Experience Data Model (XDM)](../../xdm/home.md): fornisce definizioni e strutture standard per i dati di Platform tramite l&#39;utilizzo di schemi. Tutti i set di dati di Platform sono conformi a uno schema XDM specifico e lo schema definisce quali campi sono identità.
* [Campi identità](../../xdm/ui/fields/identity.md): scopri come viene definito un campo identità in uno schema XDM.

## Creare una richiesta {#create-request}

Per avviare il processo, seleziona **[!UICONTROL Ciclo di vita dati]** nell&#39;area di navigazione a sinistra dell&#39;interfaccia utente di Platform. Viene visualizzata l&#39;area di lavoro [!UICONTROL Richieste del ciclo di vita dei dati]. Quindi, seleziona **[!UICONTROL Crea richiesta]** dalla pagina principale nell&#39;area di lavoro.

![L&#39;area di lavoro [!UICONTROL Richieste del ciclo di vita dei dati] con [!UICONTROL Crea richiesta] selezionata.](../images/ui/record-delete/create-request-button.png)

Viene visualizzato il flusso di lavoro per la creazione delle richieste. Per impostazione predefinita, l&#39;opzione **[!UICONTROL Elimina record]** è selezionata nella sezione **[!UICONTROL Azione richiesta]**. Lascia selezionata questa opzione.

>[!IMPORTANT]
> 
>Per migliorare l’efficienza e ridurre i costi delle operazioni relative ai set di dati, le organizzazioni che sono state spostate nel formato Delta possono eliminare i dati dal servizio Identity, dal profilo cliente in tempo reale e dal data lake. Questo tipo di utente viene definito delta-migrato. Gli utenti delle organizzazioni con migrazione differita possono scegliere di eliminare i record da un singolo set di dati o da tutti. Gli utenti di organizzazioni che non sono stati sottoposti a migrazione delta non possono eliminare selettivamente i record da un singolo set di dati o da tutti i set di dati, come illustrato nell’immagine seguente. In questo caso, passare alla sezione [Fornisci identità](#provide-identities) della guida.

![Il flusso di lavoro per la creazione delle richieste con l&#39;opzione [!UICONTROL Elimina record] selezionata ed evidenziata.](../images/ui/record-delete/delete-record.png)

## Seleziona set di dati {#select-dataset}

Il passaggio successivo consiste nel determinare se eliminare record da un singolo set di dati o da tutti i set di dati. Se questa opzione non è disponibile, passare alla sezione [Specificare le identità](#provide-identities) della guida.

Nella sezione **[!UICONTROL Dettagli record]**, utilizza il pulsante di scelta per selezionare tra un set di dati specifico e tutti i set di dati. Se si sceglie **[!UICONTROL Seleziona set di dati]**, procedere con la selezione dell&#39;icona del database (![Icona del database](../images/ui/record-delete/database-icon.png)) per aprire una finestra di dialogo contenente un elenco dei set di dati disponibili. Seleziona il set di dati desiderato dall&#39;elenco seguito da **[!UICONTROL Fine]**.

![Finestra di dialogo [!UICONTROL Seleziona set di dati] con un set di dati selezionato ed evidenziato [!UICONTROL Fine].](../images/ui/record-delete/select-dataset.png)

Per eliminare record da tutti i set di dati, selezionare **[!UICONTROL Tutti i set di dati]**.

![Finestra di dialogo [!UICONTROL Seleziona set di dati] con l&#39;opzione [!UICONTROL Tutti i set di dati] selezionata.](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>Se si seleziona l&#39;opzione **[!UICONTROL Tutti i set di dati]**, l&#39;operazione di eliminazione potrebbe richiedere più tempo e non risultare in un&#39;eliminazione accurata dei record.

## Fornire identità {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Spazio dei nomi identità"
>abstract="Uno spazio dei nomi identità è un attributo che collega un record al profilo di un consumatore in Experience Platform. Il campo spazio dei nomi identità per un set di dati è definito dallo schema su cui si basa il set di dati. In questa colonna è necessario specificare il tipo (o spazio dei nomi) per lo spazio dei nomi identità del record, ad esempio `email` per gli indirizzi e-mail e `ecid` per gli Experience Cloud ID. Per ulteriori informazioni, consulta la guida all’interfaccia utente del ciclo di vita dei dati."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Valore dell’identità primaria"
>abstract="In questa colonna è necessario specificare il valore per lo spazio dei nomi identità del record, che deve corrispondere al tipo di identità specificato nella colonna a sinistra. Se il tipo di spazio dei nomi identità è `email`, il valore deve corrispondere all’indirizzo e-mail del record. Per ulteriori informazioni, consulta la guida all’interfaccia utente del ciclo di vita dei dati."

Quando si eliminano i record, è necessario fornire informazioni sull&#39;identità in modo che il sistema possa determinare quali record devono essere eliminati. Per qualsiasi set di dati in Platform, i record vengono eliminati in base al campo **spazio dei nomi identità** definito dallo schema del set di dati.

Come tutti i campi di identità in Platform, uno spazio dei nomi di identità è composto da due elementi: un **tipo** (a volte indicato come spazio dei nomi di identità) e un **valore**. Il tipo di identità fornisce contesto su come il campo identifica un record (ad esempio un indirizzo e-mail). Il valore rappresenta l&#39;identità specifica di un record per quel tipo, ad esempio `jdoe@example.com` per il tipo di identità `email`. I campi più comuni utilizzati come identità includono informazioni sull’account, ID dispositivo e ID cookie.

>[!TIP]
>
>Se non conosci lo spazio dei nomi delle identità per un particolare set di dati, puoi trovarlo nell’interfaccia utente di Platform. Nell&#39;area di lavoro **[!UICONTROL Set di dati]** selezionare il set di dati in questione dall&#39;elenco. Nella pagina dei dettagli del set di dati, passa il cursore sul nome dello schema del set di dati nella barra a destra. Lo spazio dei nomi dell’identità viene visualizzato insieme al nome e alla descrizione dello schema.
>
>![Dashboard dei set di dati con un set di dati selezionato e una finestra di dialogo schema aperta dal pannello dei dettagli del set di dati. L&#39;ID primario del set di dati è evidenziato.](../images/ui/record-delete/dataset-primary-identity.png)

Se elimini record da un singolo set di dati, tutte le identità fornite devono avere lo stesso tipo, in quanto un set di dati può avere un solo spazio dei nomi delle identità. Se elimini da tutti i set di dati, puoi includere più tipi di identità in quanto set di dati diversi possono avere identità primarie diverse.

Esistono due opzioni per fornire le identità quando si eliminano i record:

* [Caricare un file JSON](#upload-json)
* [Immetti manualmente i valori di identità primaria](#manual-identity)

### Caricare un file JSON {#upload-json}

Per caricare un file JSON, puoi trascinarlo e rilasciarlo nell&#39;area fornita, oppure selezionare **[!UICONTROL Scegli i file]** da sfogliare e selezionare dalla directory locale.

![Il flusso di lavoro per la creazione delle richieste con l&#39;interfaccia Scegli file e trascina per caricare i file JSON è evidenziato.](../images/ui/record-delete/upload-json.png)

Il file JSON deve essere formattato come un array di oggetti, ogni oggetto che rappresenta un’identità.

```json
[
  {
    "namespaceCode": "email",
    "value": "jdoe@example.com"
  },
  {
    "namespaceCode": "email",
    "value": "san.gray@example.com"
  }
]
```

| Proprietà | Descrizione |
| --- | --- |
| `namespaceCode` | Il tipo di identità. |
| `value` | Il valore dell’identità primaria come indicato dal tipo. |

Una volta caricato il file, puoi continuare a [inviare la richiesta](#submit).

### Immetti manualmente le identità {#manual-identity}

Per immettere le identità manualmente, selezionare **[!UICONTROL Aggiungi identità]**.

![Il flusso di lavoro per la creazione delle richieste con l&#39;opzione [!UICONTROL Aggiungi identità] evidenziata.](../images/ui/record-delete/add-identity.png)

Vengono visualizzati i controlli che consentono di immettere le identità una alla volta. In **[!UICONTROL spazio dei nomi identità]**, utilizza il menu a discesa per selezionare il tipo di identità. In **[!UICONTROL Valore identità primaria]**, fornire il valore dello spazio dei nomi identità per il record.

![Il flusso di lavoro per la creazione di richieste con un campo di identità aggiunto manualmente.](../images/ui/record-delete/identity-added.png)

Per aggiungere altre identità, selezionare l&#39;icona più (![A icona più.](../images/ui/record-delete/plus-icon.png)) accanto a una delle righe oppure selezionare **[!UICONTROL Aggiungi identità]**.

![Flusso di lavoro per la creazione di richieste con l&#39;icona più e l&#39;icona Aggiungi identità evidenziate.](../images/ui/record-delete/more-identities.png)

## Inviare la richiesta {#submit}

Dopo aver aggiunto le identità alla richiesta, in **[!UICONTROL Impostazioni richiesta]**, fornisci un nome e una descrizione facoltativa per la richiesta prima di selezionare **[!UICONTROL Invia]**.

>[!IMPORTANT]
> 
>Esistono limiti diversi per il numero totale di eliminazioni di record di identità univoci che possono essere inviate ogni mese. Questi limiti sono basati sul contratto di licenza. Le organizzazioni che hanno acquistato tutte le edizioni di Adobe Real-time Customer Data Platform o Adobe Journey Optimizer possono inviare fino a 100.000 record di identità eliminati ogni mese. Le organizzazioni che hanno acquistato **Adobe Healthcare Shield** o **Adobe Privacy &amp; Security Shield** possono inviare fino a 600.000 record di identità eliminati ogni mese.<br>Una richiesta di eliminazione di un singolo record tramite l&#39;interfaccia utente consente di inviare contemporaneamente 10.000 ID. Il metodo [API per eliminare i record](../api/workorder.md#create) consente di inviare contemporaneamente 100.000 ID.<br>È consigliabile inviare il maggior numero possibile di ID per richiesta, fino al limite di ID. Quando intendi eliminare un volume elevato di ID, devi evitare di inviare un volume basso o un singolo ID per richiesta di cancellazione del record.

![I campi [!UICONTROL Name] e [!UICONTROL Description] dell&#39;impostazione della richiesta sono evidenziati da [!UICONTROL Submit].](../images/ui/record-delete/submit.png)

Viene visualizzata una finestra di dialogo [!UICONTROL Conferma richiesta] per indicare che le identità non possono essere recuperate una volta eliminate. Seleziona **[!UICONTROL Invia]** per confermare l&#39;elenco di identità di cui desideri eliminare i dati.

![Finestra di dialogo [!UICONTROL Conferma richiesta].](../images/ui/record-delete/confirm-request.png)

Dopo l&#39;invio della richiesta, viene creato un ordine di lavoro che viene visualizzato nella scheda [!UICONTROL Record] dell&#39;area di lavoro [!UICONTROL Ciclo di vita dei dati]. Da qui è possibile monitorare lo stato dell&#39;ordine di lavoro durante l&#39;elaborazione della richiesta.

>[!NOTE]
>
>Per informazioni dettagliate sull&#39;elaborazione delle eliminazioni dei record dopo l&#39;esecuzione, consultare la sezione della panoramica relativa a [timeline e trasparenza](../home.md#record-delete-transparency).

![Scheda [!UICONTROL Record] dell&#39;area di lavoro [!UICONTROL Ciclo di vita dati] con la nuova richiesta evidenziata.](../images/ui/record-delete/request-log.png)

## Passaggi successivi

Questo documento illustra come eliminare i record nell’interfaccia utente di Experience Platform. Per informazioni su come eseguire altre attività di gestione del ciclo di vita dei dati nell&#39;interfaccia utente, fare riferimento alla [Panoramica dell&#39;interfaccia utente del ciclo di vita dei dati](./overview.md).

Per informazioni su come eliminare i record utilizzando l&#39;API di igiene dei dati, consulta la [guida dell&#39;endpoint dell&#39;ordine di lavoro](../api/workorder.md).
