---
title: Elimina record
description: Scopri come eliminare i record nell’interfaccia utente di Adobe Experience Platform.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
hide: true
hidefromtoc: true
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 10%

---

# Elimina record

Il [[!UICONTROL Igiene dei dati] workspace](./overview.md) nell’interfaccia utente di Adobe Experience Platform consente di eliminare i record che partecipano al servizio Identity e al profilo cliente in tempo reale. Questi record possono essere associati a singoli consumatori o a qualsiasi altra entità inclusa nel grafico delle identità.

>[!IMPORTANT]
>
>Le richieste di cancellazione dei record sono disponibili solo per le organizzazioni che hanno acquistato **Schermo sanitario Adobe**.
>
>
>Le eliminazioni di record devono essere utilizzate per la pulizia dei dati, la rimozione di dati anonimi o la minimizzazione dei dati. Sono **non** da utilizzare per le richieste di diritti degli interessati (conformità) relative a normative sulla privacy come il Regolamento generale sulla protezione dei dati (RGPD). Per tutti i casi di utilizzo di conformità, utilizza [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) invece.

## Prerequisiti

L’eliminazione dei record richiede una buona conoscenza del funzionamento dei campi di identità in Experience Platform. In particolare, è necessario conoscere i valori di identità primari delle entità di cui si desidera eliminare i record, a seconda del set di dati (o dei set di dati) da cui li si sta eliminando.

Per ulteriori informazioni sulle identità in Platform, consulta la seguente documentazione:

* [Servizio Adobe Experience Platform Identity](../../identity-service/home.md): collega le identità tra dispositivi e sistemi, collegando i set di dati in base ai campi di identità definiti dagli schemi XDM a cui si conformano.
   * [Spazi dei nomi delle identità](../../identity-service/namespaces.md): gli spazi dei nomi di identità definiscono i diversi tipi di informazioni di identità che possono riferirsi a una singola persona e sono un componente obbligatorio per ogni campo di identità.
* [Profilo cliente in tempo reale](../../profile/home.md): sfrutta i grafici di identità per fornire profili di consumatori unificati basati su dati aggregati provenienti da più origini, aggiornati in tempo quasi reale.
* [Experience Data Model (XDM)](../../xdm/home.md): fornisce definizioni e strutture standard per i dati di Platform tramite l’utilizzo di schemi. Tutti i set di dati di Platform sono conformi a uno schema XDM specifico e lo schema definisce quali campi sono identità.
   * [Campi di identità](../../xdm/ui/fields/identity.md): scopri come viene definito un campo di identità in uno schema XDM.

## Crea una nuova richiesta

Per avviare il processo, seleziona **[!UICONTROL Crea richiesta]** dalla pagina principale nell’area di lavoro.

![Immagine che mostra [!UICONTROL Crea richiesta] pulsante selezionato](../images/ui/record-delete/create-request-button.png)

Viene visualizzata la finestra di dialogo per la creazione della richiesta. Per impostazione predefinita, il **[!UICONTROL Elimina consumatore]** è selezionata sotto il **[!UICONTROL Azione richiesta]** sezione. Lascia selezionata questa opzione.

![Immagine che mostra l’opzione Elimina consumatore selezionata nella finestra di dialogo di creazione](../images/ui/record-delete/consumer-action.png)

## Seleziona set di dati

Sotto **[!UICONTROL Dettagli consumatore]** sezione, il passaggio successivo consiste nel determinare se eliminare record da un singolo set di dati o da tutti i set di dati.

Se si sceglie **[!UICONTROL Seleziona set di dati]**, selezionare l&#39;icona del database (![Immagine dell&#39;icona del database](../images/ui/record-delete/database-icon.png)) e viene visualizzata una finestra di dialogo che consente di selezionare il set di dati desiderato dall’elenco.

![Immagine che mostra la finestra di dialogo per la selezione del set di dati](../images/ui/record-delete/select-dataset.png)

Se desideri eliminare record da tutti i set di dati, seleziona **[!UICONTROL Tutti i set di dati]**.

![Immagine che mostra [!UICONTROL Tutti i set di dati] opzione selezionata](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>Selezione del **[!UICONTROL Tutti i set di dati]** potrebbe richiedere più tempo e non consentire l&#39;eliminazione accurata dei record.

## Fornisci identità {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Identità primaria"
>abstract="Un’identità primaria è un attributo che collega un record al profilo di un consumatore in Experience Platform. Il campo di identità primaria per un set di dati è definito dallo schema su cui si basa il set di dati. In questa colonna è necessario specificare il tipo (o spazio dei nomi) per l’identità primaria del record, ad esempio `email` per gli indirizzi e-mail e `ecid` per gli Experience Cloud ID. Per ulteriori informazioni, consulta la guida all’interfaccia per l’igiene dei dati."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Valore identità"
>abstract="In questa colonna è necessario fornire il valore per l’identità primaria del record, che deve corrispondere al tipo di identità specificato nella colonna a sinistra. Se il tipo di identità primaria è `email`, il valore deve corrispondere all’indirizzo e-mail del record. Per ulteriori informazioni, consulta la guida all’interfaccia per l’igiene dei dati."

Quando si eliminano i record, è necessario fornire informazioni sull&#39;identità in modo che il sistema possa determinare quali record devono essere eliminati. Per qualsiasi set di dati in Platform, i record vengono eliminati in base al **identità primaria** campo definito dallo schema del set di dati.

Come tutti i campi di identità in Platform, un’identità primaria è composta da due elementi: **tipo** (talvolta denominati spazi dei nomi delle identità) e **valore**. Il tipo di identità fornisce contesto sul modo in cui il campo identifica un record (ad esempio un indirizzo e-mail) e il valore rappresenta l’identità specifica di un record per quel tipo (ad esempio, `jdoe@example.com` per `email` tipo di identità). I campi più comuni utilizzati come identità includono informazioni sull’account, ID dispositivo e ID cookie.

>[!TIP]
>
>Se non conosci l’identità primaria di un particolare set di dati, puoi trovarlo nell’interfaccia utente di Platform. In **[!UICONTROL Set di dati]** Workspace, seleziona il set di dati in questione dall’elenco. Nella pagina dei dettagli del set di dati, passa il cursore sul nome dello schema del set di dati nella barra a destra. L’identità primaria viene visualizzata insieme al nome e alla descrizione dello schema.
>
>![Immagine che mostra l’identità principale di un set di dati evidenziata nell’interfaccia utente](../images/ui/record-delete/dataset-primary-identity.png)

Se elimini record da un singolo set di dati, tutte le identità fornite devono avere lo stesso tipo, in quanto un set di dati può avere una sola identità primaria. Se elimini da tutti i set di dati, puoi includere più tipi di identità in quanto set di dati diversi possono avere identità primarie diverse.

Esistono due opzioni per fornire le identità quando si eliminano i record:

* [Caricare un file JSON](#upload-json)
* [Immetti manualmente i valori di identità](#manual-identity)

### Caricare un file JSON {#upload-json}

Per caricare un file JSON, puoi trascinarlo e rilasciarlo nell’area fornita, oppure selezionare **[!UICONTROL Scegli i file]** per sfogliare e selezionare dalla directory locale.

![Immagine che mostra i metodi per caricare JSON nell’interfaccia utente](../images/ui/record-delete/upload-json.png)

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
| `value` | Il valore di identità come indicato dal tipo. |

Una volta caricato il file, puoi continuare con [invia la richiesta](#submit).

### Immetti le identità manualmente {#manual-identity}

Per immettere manualmente le identità, seleziona **[!UICONTROL Aggiungi identità]**.

![Immagine che mostra [!UICONTROL Aggiungi identità] pulsante selezionato](../images/ui/record-delete/add-identity.png)

Vengono visualizzati i controlli che consentono di immettere le identità una alla volta. Sotto **[!UICONTROL Identità primaria]**, utilizza il menu a discesa per selezionare il tipo di identità. Sotto **[!UICONTROL Valore identità]**, fornisci il valore di identità primaria del record.

![Immagine che mostra un campo di identità aggiunto manualmente](../images/ui/record-delete/identity-added.png)

Per aggiungere altre identità, seleziona l’icona più (![Immagine dell&#39;icona più](../images/ui/record-delete/plus-icon.png)) accanto a una delle righe, oppure seleziona **[!UICONTROL Aggiungi identità]**.

![Immagine che mostra come aggiungere altre identità alla richiesta](../images/ui/record-delete/more-identities.png)

## Invia la richiesta (#submit)

Dopo aver aggiunto le identità alla richiesta, in **[!UICONTROL Impostazioni richiesta]**, fornisci un nome e una descrizione facoltativa per la richiesta prima di selezionare **[!UICONTROL Invia]**.

![Immagine che mostra [!UICONTROL Invia] pulsante selezionato](../images/ui/record-delete/submit.png)

Ti viene chiesto di confermare l’elenco delle identità di cui desideri eliminare i dati. Seleziona **[!UICONTROL Invia]** per confermare la selezione.

![Immagine che mostra la finestra di dialogo di conferma](../images/ui/record-delete/confirm-request.png)

Dopo l&#39;invio della richiesta, viene creato un ordine di lavoro che viene visualizzato nel [!UICONTROL Consumatore] scheda di [!UICONTROL Igiene dei dati] Workspace. Da qui è possibile monitorare lo stato dell&#39;ordine di lavoro durante l&#39;elaborazione della richiesta.

>[!NOTE]
>
>Consulta la sezione panoramica su [tempistiche e trasparenza](../home.md#record-delete-transparency) per informazioni dettagliate sulla modalità di elaborazione delle eliminazioni dei record dopo l&#39;esecuzione.

## Passaggi successivi

Questo documento illustra come eliminare i record nell’interfaccia utente di Experience Platform. Per informazioni su come eseguire altre attività di igiene dei dati nell’interfaccia utente, consulta [panoramica dell’interfaccia utente di igiene dei dati](./overview.md).

Per informazioni su come eliminare i record utilizzando l’API di igiene dei dati, consulta [guida dell’endpoint dell’ordine di lavoro](../api/workorder.md).
