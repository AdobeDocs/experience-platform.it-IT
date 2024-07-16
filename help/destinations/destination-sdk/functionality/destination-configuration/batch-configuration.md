---
description: Scopri come configurare le impostazioni di esportazione dei file per le destinazioni create con Destination SDK.
title: Configurazione batch
exl-id: 0ffbd558-a83c-4c3d-b4fc-b6f7a23a163a
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 2%

---

# Configurazione batch {#batch-configuration}

Utilizza le opzioni di configurazione batch in Destination SDK per consentire agli utenti di personalizzare i nomi dei file esportati e configurare la pianificazione dell’esportazione in base alle loro preferenze.

Quando crei destinazioni basate su file tramite Destination SDK, puoi configurare la denominazione file predefinita e le pianificazioni di esportazione, oppure puoi dare agli utenti la possibilità di configurare queste impostazioni dall’interfaccia utente di Platform. Ad esempio, puoi configurare comportamenti quali:

* Includere informazioni specifiche nel nome del file, ad esempio ID pubblico, ID destinazione o informazioni personalizzate.
* Consente agli utenti di personalizzare la denominazione dei file dall’interfaccia utente di Platform.
* Configura le esportazioni di file in modo che avvengano a intervalli di tempo impostati.
* Definisci le opzioni di denominazione dei file e di personalizzazione della pianificazione di esportazione che gli utenti possono visualizzare nell’interfaccia utente di Platform.

Le impostazioni di configurazione batch fanno parte della configurazione di destinazione per le destinazioni basate su file.

Per capire dove questo componente si inserisce in un&#39;integrazione creata con Destination SDK, consulta il diagramma nella documentazione delle [opzioni di configurazione](../configuration-options.md) oppure consulta la guida su come [utilizzare Destination SDK per configurare una destinazione basata su file](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

È possibile configurare le impostazioni di denominazione ed esportazione dei file tramite l&#39;endpoint `/authoring/destinations`. Consulta le seguenti pagine di riferimento API per esempi dettagliati di chiamate API, in cui puoi configurare i componenti mostrati in questa pagina.

* [Creare una configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aggiornare una configurazione di destinazione](../../authoring-api/destination-configuration/update-destination-configuration.md)

Questo articolo descrive tutte le opzioni di configurazione batch supportate che puoi utilizzare per la tua destinazione e mostra cosa vedranno i clienti nell’interfaccia utente di Platform.

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Consulta la tabella seguente per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina.

| Tipo di integrazione | Supporta la funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | No |
| Integrazioni basate su file (batch) | Sì |

## Parametri supportati {#supported-parameters}

I valori impostati qui vengono visualizzati nel passaggio [Pianifica esportazione pubblico](../../../ui/activate-batch-profile-destinations.md#scheduling) del flusso di lavoro di attivazione delle destinazioni basate su file.

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
   "segmentGroupingEnabled": true
   }
```

| Parametro | Tipo | Descrizione |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Booleano | Imposta su `true` per consentire ai clienti di specificare quali attributi di profilo sono obbligatori. Il valore predefinito è `false`. Per ulteriori informazioni, vedere [Attributi obbligatori](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `allowDedupeKeyFieldSelection` | Booleano | Impostare su `true` per consentire ai clienti di specificare le chiavi di deduplicazione. Il valore predefinito è `false`.  Per ulteriori informazioni, vedere [Chiavi di deduplicazione](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |
| `defaultExportMode` | Enumerazione | Definisce la modalità di esportazione predefinita del file. Valori supportati:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> Il valore predefinito è `DAILY_FULL_EXPORT`. Consulta la [documentazione sull&#39;attivazione batch](../../../ui/activate-batch-profile-destinations.md#scheduling) per informazioni dettagliate sulla pianificazione delle esportazioni di file. |
| `allowedExportModes` | Elenco | Definisce le modalità di esportazione dei file disponibili per i clienti. Valori supportati:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Elenco | Definisce la frequenza di esportazione dei file disponibile per i clienti. Valori supportati:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Enumerazione | Definisce la frequenza di esportazione predefinita dei file. Valori supportati:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> Il valore predefinito è `DAILY`. |
| `defaultStartTime` | Stringa | Definisce l&#39;ora di inizio predefinita per l&#39;esportazione del file. Utilizza il formato file a 24 ore. Il valore predefinito è &quot;00:00&quot;. |
| `filenameConfig.allowedFilenameAppendOptions` | Stringa | *Richiesto*. Elenco delle macro di nomi file disponibili tra cui gli utenti possono scegliere. Questo determina quali elementi vengono aggiunti ai nomi dei file esportati (ID pubblico, nome organizzazione, data e ora di esportazione e altri). Quando si imposta `defaultFilename`, assicurarsi di evitare la duplicazione delle macro. <br><br>Valori supportati: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Indipendentemente dall&#39;ordine in cui si definiscono le macro, l&#39;interfaccia utente di Experience Platform le visualizzerà sempre nell&#39;ordine presentato qui. <br><br> Se `defaultFilename` è vuoto, l&#39;elenco `allowedFilenameAppendOptions` deve contenere almeno una macro. |
| `filenameConfig.defaultFilenameAppendOptions` | Stringa | *Richiesto*. Macro dei nomi di file predefiniti preselezionate che gli utenti possono deselezionare.<br><br> Le macro in questo elenco sono un sottoinsieme di quelle definite in `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | Stringa | *Facoltativo*. Definisce le macro dei nomi di file predefiniti per i file esportati. Non possono essere sovrascritti dagli utenti. <br><br>Qualsiasi macro definita da `allowedFilenameAppendOptions` verrà aggiunta dopo le macro `defaultFilename`. <br><br>Se `defaultFilename` è vuoto, definire almeno una macro in `allowedFilenameAppendOptions`. |
| `segmentGroupingEnabled` | Booleano | Definisce se i tipi di pubblico attivati devono essere esportati in uno o più file, in base al criterio di unione [del pubblico](../../../../profile/merge-policies/overview.md). Valori supportati: <ul><li>`true`: esporta un file per criterio di unione.</li><li>`false`: esporta un file per pubblico, indipendentemente dal criterio di unione. Questo è il comportamento predefinito. È possibile ottenere lo stesso risultato omettendo completamente questo parametro.</li></ul> |

{style="table-layout:auto"}

## Configurazione del nome file {#file-name-configuration}

Utilizzare le macro di configurazione dei nomi di file per definire i nomi di file esportati da includere. Le macro nella tabella seguente descrivono gli elementi trovati nell&#39;interfaccia utente nella schermata [configurazione nome file](../../../ui/activate-batch-profile-destinations.md#file-names).

>[!TIP]
> 
>È consigliabile includere sempre la macro `SEGMENT_ID` nei nomi dei file esportati. Poiché gli ID segmento sono univoci, includerli nel nome file è il modo migliore per garantire che anche i nomi dei file siano univoci.

| Macro | Etichetta interfaccia utente | Descrizione | Esempio |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Destinazione] | Nome della destinazione nell’interfaccia utente. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL ID segmento] | ID pubblico univoco generato dalla piattaforma | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Nome segmento] | Nome del pubblico definito dall&#39;utente | Abbonato VIP |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL ID destinazione] | ID univoco generato dalla piattaforma dell’istanza di destinazione | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Nome destinazione] | Nome definito dall&#39;utente dell&#39;istanza di destinazione. | La mia destinazione Advertising 2022 |
| `ORGANIZATION_NAME` | [!UICONTROL Nome organizzazione] | Nome dell’organizzazione del cliente in Adobe Experience Platform. | Nome organizzazione |
| `SANDBOX_NAME` | [!UICONTROL Nome Sandbox] | Nome della sandbox utilizzato dal cliente. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Data e ora] | `DATETIME` e `TIMESTAMP` definiscono entrambi quando il file è stato generato, ma in formati diversi. <br><br><ul><li>`DATETIME` utilizza il seguente formato: YYYYMMDD_HHMMSS.</li><li>`TIMESTAMP` utilizza il formato Unix a 10 cifre. </li></ul> `DATETIME` e `TIMESTAMP` si escludono a vicenda e non possono essere utilizzati contemporaneamente. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Testo personalizzato] | Testo personalizzato definito dall&#39;utente da includere nel nome del file. Impossibile utilizzare in `defaultFilename`. | My_Custom_Text |
| `TIMESTAMP` | [!UICONTROL Data e ora] | Timestamp a 10 cifre dell’ora in cui è stato generato il file, in formato Unix. | 1652131584 |
| `MERGE_POLICY_ID` | [!UICONTROL ID criterio di unione] | ID del [criterio di unione](../../../../profile/merge-policies/overview.md) utilizzato per generare il pubblico esportato. Utilizzare questa macro quando si raggruppano i tipi di pubblico esportati in file in base al criterio di unione. Utilizzare questa macro insieme a `segmentGroupingEnabled:true`. | e8591fdb-2873-4b12-b63e-15275b1c1439 |
| `MERGE_POLICY_NAME` | [!UICONTROL Nome criterio di unione] | Nome del [criterio di unione](../../../../profile/merge-policies/overview.md) utilizzato per generare il pubblico esportato. Utilizzare questa macro quando si raggruppano i tipi di pubblico esportati in file in base al criterio di unione. Utilizzare questa macro insieme a `segmentGroupingEnabled:true`. | Il mio criterio di unione personalizzato |

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

![Immagine dell&#39;interfaccia utente che mostra la schermata di configurazione del nome file con le macro preselezionate](../../assets/functionality/destination-configuration/file-name-configuration.png)

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, sarai in grado di comprendere meglio come configurare la denominazione dei file e le pianificazioni di esportazione per le destinazioni basate su file.

Per ulteriori informazioni sugli altri componenti di destinazione, consulta i seguenti articoli:

* [Configurazione autenticazione cliente](customer-authentication.md)
* [Autorizzazione OAuth2](oauth2-authorization.md)
* [Campi dati cliente](customer-data-fields.md)
* [Attributi dell’interfaccia utente](ui-attributes.md)
* [Configurazione dello schema](schema-configuration.md)
* [Configurazione dello spazio dei nomi dell’identità](identity-namespace-configuration.md)
* [Configurazioni di mappatura supportate](supported-mapping-configurations.md)
* [Consegna della destinazione](destination-delivery.md)
* [Configurazione dei metadati del pubblico](audience-metadata-configuration.md)
* [Criterio di aggregazione](aggregation-policy.md)
* [Qualifiche del profilo storico](historical-profile-qualifications.md)
