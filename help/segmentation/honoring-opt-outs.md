---
keywords: ' Experience Platform;home;argomenti popolari;opt-out;Segmentazione;servizio segmentazione;servizio di segmentazione;onorare opt-out;opt-out;opt-out;opt-out;'
solution: Experience Platform
title: Rispetto delle richieste di rifiuto nei segmenti
topic: overview
description: 'Adobe Experience Platform consente ai clienti di inviare richieste di rifiuto relative all''utilizzo e all''archiviazione dei loro dati all''interno del profilo cliente in tempo reale]. Queste richieste di rinuncia fanno parte dell''accordo sulla tutela della privacy dei consumatori (CCPA) della California, che conferisce ai residenti della California il diritto di accedere ai propri dati personali ed eliminarli e di sapere se i loro dati personali sono venduti o divulgati (e a chi). '
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---


# Rispetto delle richieste di rifiuto nei segmenti

Adobe Experience Platform consente ai clienti di inviare richieste di rifiuto relative all&#39;utilizzo e all&#39;archiviazione dei dati entro [!DNL Real-time Customer Profile]. Queste richieste di rifiuto fanno parte dell&#39; [!DNL California Consumer Privacy Act] (CCPA), che conferisce ai residenti della California il diritto di accedere ai propri dati personali ed eliminarli e di sapere se i loro dati personali sono venduti o divulgati (e a chi).

Una volta che un cliente ha rinunciato, è importante che l&#39;organizzazione rispetti tali rinunce quando genera audience per attività di marketing. Questo documento descrive importanti dettagli relativi al rispetto delle richieste di rifiuto.

## Introduzione

Per soddisfare le richieste di rifiuto è necessario conoscere i vari servizi [!DNL Adobe Experience Platform] coinvolti. Prima di utilizzare le richieste di rifiuto, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Real-time Customer Profile]](../profile/home.md): Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Consente di creare segmenti di pubblico dai  [!DNL Real-time Customer Profile] dati.
- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Il framework standardizzato tramite il quale la piattaforma organizza i dati sull&#39;esperienza cliente.
- [[!DNL Adobe Experience Platform Privacy Service]](../privacy-service/home.md): Consente alle organizzazioni di automatizzare la conformità alle normative sulla privacy dei dati che riguardano i dati dei clienti all&#39;interno  [!DNL Platform].

## Mixine di rinunce

Per soddisfare le richieste di rifiuto CCPA, uno degli schemi che fa parte dello schema unione deve contenere i campi di rinuncia [!DNL Experience Data Model] (XDM) necessari. Esistono due mixin che possono essere utilizzati per aggiungere campi di rinuncia a uno schema, ciascuno dei quali è trattato in modo più dettagliato nelle sezioni seguenti:

- [Privacy](#profile-privacy) profilo: Utilizzato per acquisire tipi di rinuncia diversi (generali o vendite/condivisione).
- [Dettagli](#profile-preferences-details) preferenze profilo: Utilizzato per acquisire le richieste di rifiuto per canali XDM specifici.

Per istruzioni dettagliate su come aggiungere un mixin a uno schema, fare riferimento alla sezione &quot;Add a mixin&quot; nella seguente documentazione XDM:
- [Esercitazione](../xdm/api/getting-started.md) sulle API del Registro di sistema dello schema.: Creazione di uno schema tramite l&#39;API del Registro di sistema dello schema.
- [Esercitazione](../xdm/tutorials/create-schema-ui.md) sull&#39;Editor di schema: Creazione di uno schema tramite l&#39;interfaccia utente della piattaforma.

Di seguito è riportata un&#39;immagine di esempio con i mixin di rinuncia aggiunti a uno schema nell&#39;interfaccia utente:

![](images/opt-outs/opt-out-mixins-user-interface.png)

La struttura di ciascun mixin, nonché una descrizione dei campi che contribuiscono allo schema, sono descritti più dettagliatamente nelle sezioni seguenti.

### [!DNL Profile Privacy] {#profile-privacy}

Il mixin [!DNL Profile Privacy] consente di acquisire due tipi di richieste di disattivazione CCPA da parte dei clienti:

1. Rifiuto generale
2. Rinuncia alla vendita/condivisione

![](images/opt-outs/profile-privacy.png)

Il mixin [!DNL Profile Privacy] contiene i campi seguenti:

- Rifiuto privacy (`privacyOptOuts`): Un array contenente un elenco di oggetti di rinuncia.
- Tipo di rifiuto (`optOutType`): Tipo di rifiuto. Questo campo è un enum con due possibili valori:
   - Rifiuto generale (`general_opt_out`)
   - Rinuncia alla condivisione delle vendite (`sales_sharing_opt_out`)
- Valore rifiuto (`optOutValue`): Lo stato attivo della rinuncia, noto anche come valore del segnale di rifiuto, in base al tipo di rifiuto specificato. Questo campo è un enum con quattro possibili valori:
   - Non fornito (`not_provided`): Non è stata fornita una richiesta di rifiuto.
   - Verifica in sospeso (`pending`): La richiesta di rifiuto è in attesa di verifica.
   - Rifiuto (`out`): Il cliente ha rinunciato.
   - Consenso (`in`): Il cliente ha acconsentito.
- Timestamp rifiuto (`timestamp`): Timestamp del segnale di rifiuto ricevuto.

Per visualizzare l&#39;intera struttura del mixin [!DNL Profile Privacy], fare riferimento all&#39; [archivio GitHub pubblico XDM](https://github.com/adobe/xdm/blob/master/schemas/context/profile-privacy.schema.json) o visualizzare l&#39;anteprima del mixin utilizzando l&#39;interfaccia utente della piattaforma.

### [!DNL Profile Preferences Details] {#profile-preferences-details}

Il mixin [!DNL Profile Preferences Details] contiene diversi campi che rappresentano le preferenze per i profili dei clienti (ad esempio il formato e-mail, la lingua preferita e il fuso orario). Uno dei campi inclusi in questo mixin, OptInOut (`optInOut`), consente di impostare i valori di rifiuto per i singoli canali.

![](images/opt-outs/profile-preferences-details.png)

Il mixin [!DNL Profile Preferences Details] contiene i seguenti campi relativi alle opzioni di rifiuto:

- OptInOut (`optInOut`): Un oggetto in cui ogni chiave rappresenta un URI valido e noto per un canale di comunicazione e lo stato attivo della rinuncia per ciascun canale. Ogni canale può avere uno dei quattro valori possibili:
   - Non fornito (`not_provided`): Per questo canale non è stata fornita una richiesta di rifiuto.
   - Verifica in sospeso (`pending`): La richiesta di rifiuto per questo canale è in attesa di verifica.
   - Rifiuto (`out`): Il cliente ha rinunciato a questo canale.
   - Consenso (`in`): Il cliente ha scelto questo canale.
- Rifiuto globale (`globalOptout`): Un valore booleano che, se impostato su true, imposta una sostituzione di rifiuto globale per il profilo. Il valore predefinito per questo campo è false.

L&#39;esempio JSON riportato di seguito evidenzia come l&#39;oggetto OptInOut possa acquisire più segnali di rifiuto per diversi canali di comunicazione:

```json
{
  "xdm:optInOut": {
    "https://ns.adobe.com/xdm/channels/email": "pending",
    "https://ns.adobe.com/xdm/channels/phone": "out",
    "https://ns.adobe.com/xdm/channels/sms": "in",
    "https://ns.adobe.com/xdm/channels/fax": "not_provided",
    "https://ns.adobe.com/xdm/channels/direct-mail": "not_provided",
    "https://ns.adobe.com/xdm/channels/apns": "not_provided",
    "xdm:globalOptout": false
  }
}
```

Per visualizzare l&#39;intera struttura del mixin Dettagli preferenze profilo, visitate il [repository GitHub pubblico XDM](https://github.com/adobe/xdm/blob/master/schemas/context/profile-preferences-details.schema.json) o visualizzate l&#39;anteprima del mixin utilizzando l&#39;interfaccia [!DNL Platform].

## Gestione delle opzioni di rifiuto nella segmentazione

Per garantire che i profili contrassegnati con flag di rifiuto CCPA non siano inclusi nei segmenti, è necessario aggiungere campi speciali ai segmenti esistenti o includerli durante la creazione del segmento.

Le sezioni seguenti mostrano come aggiungere i campi appropriati per i due tipi di flag di rifiuto:
1. Rifiuto generale
2. Rinuncia alla vendita/condivisione

### Rifiuto generale

[!DNL Segmentation] rispetta automaticamente tutti i profili contenenti il flag &quot;[!UICONTROL General Opt-Out]&quot;, il che significa che tali profili non saranno inclusi nel pubblico o nelle esportazioni per impostazione predefinita. Tuttavia, è consigliabile aggiungere i campi appropriati per garantire che i profili di rinuncia non siano inclusi nelle attività di audience e marketing.

Questo può essere fatto utilizzando l&#39;interfaccia utente aggiungendo gli attributi **[!UICONTROL Privacy Opt-Outs]**. In questo caso, il segmento è impostato per includere solo coloro che hanno acconsentito (ovvero non hanno un flag generale di rifiuto sul profilo). A tal fine, è necessario dichiarare che &quot;[!UICONTROL Opt-Out Type]&quot; è uguale a &quot;[!UICONTROL General Opt-Out]&quot; e che &quot;[!UICONTROL Opt-Out Value]&quot; è uguale a &quot;[!UICONTROL Opt-in]&quot;.

![](images/opt-outs/segment-general-opt-out.png)

### Rinuncia alla vendita/condivisione

Se un utente ha un flag di rinuncia alla vendita/condivisione impostato sul suo profilo, questo profilo non deve più essere utilizzato per la creazione di segmenti o per le attività di marketing. Per assicurarsi che questo flag sia rispettato, &quot;[!UICONTROL Opt-Out Type]&quot; deve essere uguale a &quot;[!UICONTROL Sales Sharing Opt-Out]&quot; e &quot;[!UICONTROL Opt-Out Value]&quot; deve essere uguale a &quot;[!UICONTROL Opt-in]&quot;.

![](images/opt-outs/segment-sales-sharing-opt-out.png)

<!-- ### Overriding default exclusions

In some instances, such as building a segment of people who have opted out, it may be necessary to override the default exclusion of opted-out profiles. This override can be done via the API or in the Segment Builder user interface. -->

## Passaggi successivi

Per ulteriori informazioni sulla segmentazione, compreso l&#39;utilizzo delle definizioni dei segmenti e delle audience tramite l&#39;API e l&#39;interfaccia utente, si prega di iniziare leggendo la [panoramica sulla segmentazione](./home.md).

Per saperne di più sulla privacy dei dati all&#39;interno di [!DNL Platform], incluso il modo in cui [!DNL Privacy Service] facilita la conformità automatica alle normative sulla privacy legali e organizzative, fare riferimento alla documentazione su [[!DNL Privacy Service]](../privacy-service/home.md).
