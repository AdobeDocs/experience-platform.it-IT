---
description: Scopri come configurare le impostazioni di esportazione dei file per le destinazioni create con Destination SDK.
title: Configurazione batch
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 4%

---


# Configurazione batch {#batch-configuration}

Utilizza le opzioni di configurazione batch nella Destination SDK per consentire agli utenti di personalizzare i nomi dei file esportati e di configurare la pianificazione dell’esportazione in base alle loro preferenze.

Quando crei destinazioni basate su file tramite Destination SDK, puoi configurare le pianificazioni predefinite per la denominazione dei file e l’esportazione oppure offrire agli utenti la possibilità di configurare queste impostazioni dall’interfaccia utente di Platform. Ad esempio, puoi configurare comportamenti come:

* Includere informazioni specifiche nel nome del file, ad esempio ID segmento, ID destinazione o informazioni personalizzate.
* Consente agli utenti di personalizzare la denominazione dei file dall’interfaccia utente di Platform.
* Configurare le esportazioni di file in modo che si verifichino a intervalli di tempo impostati.
* Definisci le opzioni di denominazione dei file ed esportazione per la personalizzazione della pianificazione che gli utenti possono visualizzare nell’interfaccia utente di Platform.

Le impostazioni di configurazione batch fanno parte della configurazione di destinazione per le destinazioni basate su file.

Per capire dove si trova questo componente in un’integrazione creata con Destination SDK, consulta il diagramma nella sezione [opzioni di configurazione](../configuration-options.md) documentazione o consulta la guida su come [utilizzare Destination SDK per configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Puoi configurare la denominazione dei file ed esportare le impostazioni di pianificazione tramite `/authoring/destinations` punto finale. Per esempi dettagliati sulle chiamate API , consulta le pagine di riferimento API seguenti dove puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md)

Questo articolo descrive tutte le opzioni di configurazione batch supportate che puoi utilizzare per la tua destinazione e mostra cosa vedranno i clienti nell’interfaccia utente di Platform.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina, consulta la tabella seguente.

| Tipo di integrazione | Supporta funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | No |
| Integrazioni basate su file (batch) | Sì |

## Parametri supportati {#supported-parameters}

I valori impostati vengono visualizzati nella variabile [Esportazione di segmenti programmata](../../../ui/activate-batch-profile-destinations.md#scheduling) passaggio del flusso di lavoro di attivazione delle destinazioni basate su file .

```json
"batchConfig":{
   "allowMandatoryFieldSelection":true,
   "allowDedupeKeyFieldSelection":true,
   "defaultExportMode":"DAILY_FULL_EXPORT",
   "allowedExportMode":[
      "DAILY_FULL_EXPORT",
      "FIRST_FULL_THEN_INCREMENTAL"
   ],
   "allowedScheduleFrequency":[
      "DAILY",
      "EVERY_3_HOURS",
      "EVERY_6_HOURS",
      "EVERY_8_HOURS",
      "EVERY_12_HOURS",
      "ONCE"
   ],
   "defaultFrequency":"DAILY",
   "defaultStartTime":"00:00",
   "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
   }
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Booleano | Imposta su `true` per consentire ai clienti di specificare quali attributi di profilo sono obbligatori. Il valore predefinito è `false`. Vedi [Attributi obbligatori](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes) per ulteriori informazioni. |
| `allowDedupeKeyFieldSelection` | Booleano | Imposta su `true` per consentire ai clienti di specificare le chiavi di deduplicazione. Il valore predefinito è `false`.  Vedi [Chiavi di deduplicazione](../../../ui/activate-batch-profile-destinations.md#deduplication-keys) per ulteriori informazioni. |
| `defaultExportMode` | Enum | Definisce la modalità di esportazione predefinita dei file. Valori supportati:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> Il valore predefinito è `DAILY_FULL_EXPORT`. Consulta la sezione [documentazione di attivazione batch](../../../ui/activate-batch-profile-destinations.md#scheduling) per informazioni sulla pianificazione delle esportazioni dei file. |
| `allowedExportModes` | Elenco | Definisce le modalità di esportazione dei file disponibili per i clienti. Valori supportati:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Elenco | Definisce la frequenza di esportazione del file disponibile per i clienti. Valori supportati:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Enum | Definisce la frequenza di esportazione predefinita del file.Valori supportati:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> Il valore predefinito è `DAILY`. |
| `defaultStartTime` | Stringa | Definisce l&#39;ora di inizio predefinita per l&#39;esportazione del file. Utilizza il formato file 24 ore su 24. Il valore predefinito è &quot;00:00&quot;. |
| `filenameConfig.allowedFilenameAppendOptions` | Stringa | *Obbligatorio*. Elenco delle macro dei nomi file disponibili tra cui gli utenti possono scegliere. Questo determina quali elementi vengono aggiunti ai nomi di file esportati (ID segmento, nome organizzazione, data e ora dell’esportazione e altri). Quando si imposta `defaultFilename`, evitare di duplicare le macro. <br><br>Valori supportati: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Indipendentemente dall’ordine in cui vengono definite le macro, l’interfaccia utente Experience Platform le visualizza sempre nell’ordine indicato qui. <br><br> Se `defaultFilename` è vuoto, il `allowedFilenameAppendOptions` L&#39;elenco deve contenere almeno una macro. |
| `filenameConfig.defaultFilenameAppendOptions` | Stringa | *Obbligatorio*. Macro con nome file predefinito preselezionate che gli utenti possono deselezionare.<br><br> Le macro di questo elenco sono un sottoinsieme di quelle definite in `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | Stringa | *Facoltativo*. Definisce le macro dei nomi file predefiniti per i file esportati. Questi non possono essere sovrascritti dagli utenti. <br><br>Qualsiasi macro definita da `allowedFilenameAppendOptions` viene aggiunto dopo il `defaultFilename` macro. <br><br>Se `defaultFilename` è vuoto, è necessario definire almeno una macro in `allowedFilenameAppendOptions`. |

{style="table-layout:auto"}

## Configurazione del nome file {#file-name-configuration}

Utilizzare le macro di configurazione del nome file per definire i nomi di file esportati da includere. Le macro nella tabella seguente descrivono gli elementi presenti nell’interfaccia utente di [configurazione del nome file](../../../ui/activate-batch-profile-destinations.md#file-names) schermo.

>[!TIP]
> 
>Come best practice, includi sempre `SEGMENT_ID` nei nomi dei file esportati. Gli ID dei segmenti sono univoci, pertanto includerli nel nome del file è il modo migliore per garantire che anche i nomi dei file siano univoci.

| Macro | Etichetta dell’interfaccia utente | Descrizione | Esempio |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Destinazione] | Nome della destinazione nell’interfaccia utente. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL ID segmento] | ID segmento univoco generato dalla piattaforma | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Nome segmento] | Nome del segmento definito dall’utente | Sottoscrittore VIP |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL ID destinazione] | ID univoco generato dalla piattaforma dell’istanza di destinazione | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Nome destinazione] | Nome definito dall&#39;utente dell&#39;istanza di destinazione. | La mia destinazione pubblicitaria 2022 |
| `ORGANIZATION_NAME` | [!UICONTROL Nome organizzazione] | Nome dell&#39;organizzazione del cliente in Adobe Experience Platform. | Nome organizzazione |
| `SANDBOX_NAME` | [!UICONTROL Nome sandbox] | Nome della sandbox utilizzata dal cliente. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Data e ora] | `DATETIME` e `TIMESTAMP` entrambi definiscono quando è stato generato il file, ma in formati diversi. <br><br><ul><li>`DATETIME` utilizza il formato seguente: YYYMMDD_HHMMSS.</li><li>`TIMESTAMP` utilizza il formato Unix a 10 cifre. </li></ul> `DATETIME` e `TIMESTAMP` si escludono a vicenda e non possono essere utilizzati contemporaneamente. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Testo personalizzato] | Testo personalizzato definito dall’utente da includere nel nome del file. Non può essere utilizzato in `defaultFilename`. | Testo_Personalizzato |
| `TIMESTAMP` | [!UICONTROL Data e ora] | Timestamp a 10 cifre dell’ora in cui è stato generato il file, in formato Unix. | 1652131584 |

{style="table-layout:auto"}

### Esempio di configurazione del nome file

L’esempio di configurazione seguente mostra la corrispondenza tra la configurazione utilizzata nella chiamata API e le opzioni visualizzate nell’interfaccia utente.

```json
"filenameConfig":{
   "allowedFilenameAppendOptions":[
      "CUSTOM_TEXT",
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilenameAppendOptions":[
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilename": "%DESTINATION%"
}
```

![Immagine dell’interfaccia utente che mostra la schermata di configurazione del nome file con macro preselezionate](../../assets/functionality/destination-configuration/file-name-configuration.png)

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, dovresti avere una migliore comprensione di come configurare la denominazione dei file e le pianificazioni di esportazione per le destinazioni basate su file.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Configurazione dell’autenticazione cliente](customer-authentication.md)
* [Autenticazione OAuth2](oauth2-authentication.md)
* [Campi dati cliente](customer-data-fields.md)
* [Attributi dell&#39;interfaccia utente](ui-attributes.md)
* [Configurazione dello schema](schema-configuration.md)
* [Configurazione dello spazio dei nomi identità](identity-namespace-configuration.md)
* [Configurazioni di mappatura supportate](supported-mapping-configurations.md)
* [Consegna delle destinazioni](destination-delivery.md)
* [Configurazione dei metadati del pubblico](audience-metadata-configuration.md)
* [Criteri di aggregazione](aggregation-policy.md)
* [Qualifiche di profilo storiche](historical-profile-qualifications.md)