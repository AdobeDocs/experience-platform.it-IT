---
keywords: Experience Platform;home;argomenti popolari;opt-out;segmentazione;servizio di segmentazione;servizio di segmentazione;onorare le rinunce;opt-out;opt-out;opt-out; opt-out;
solution: Experience Platform
title: Rispetto delle richieste di rinuncia nei segmenti
topic: ' - Panoramica'
description: 'Adobe Experience Platform consente ai clienti di inviare richieste di rinuncia relative all’utilizzo e all’archiviazione dei propri dati all’interno di Profilo cliente in tempo reale]. Queste richieste di rinuncia fanno parte del California Consumer Privacy Act (CCPA), che conferisce ai residenti della California il diritto di accedere e cancellare i loro dati personali e di sapere se i loro dati personali vengono venduti o divulgati (e a chi). '
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---


# Rispetto delle richieste di rinuncia nei segmenti

Adobe Experience Platform consente ai clienti di inviare richieste di rinuncia relative all’utilizzo e all’archiviazione dei propri dati all’interno di [!DNL Real-time Customer Profile]. Queste richieste di rinuncia fanno parte del [!DNL California Consumer Privacy Act] (CCPA), che conferisce ai residenti della California il diritto di accedere e cancellare i propri dati personali e di sapere se i propri dati personali vengono venduti o divulgati (e a chi).

Una volta che un cliente ha rinunciato, è importante che la tua organizzazione onori tali rinunce quando genera tipi di pubblico per attività di marketing. Questo documento descrive importanti dettagli relativi al rispetto delle richieste di rinuncia.

## Introduzione

Il rispetto delle richieste di rinuncia richiede una comprensione dei vari servizi [!DNL Adobe Experience Platform] coinvolti. Prima di lavorare con le richieste di rinuncia, controlla la documentazione per i seguenti servizi:

- [[!DNL Real-time Customer Profile]](../profile/home.md): Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Ti consente di creare segmenti di pubblico dai  [!DNL Real-time Customer Profile] dati.
- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Il framework standardizzato tramite il quale Platform organizza i dati sulla customer experience.
- [[!DNL Adobe Experience Platform Privacy Service]](../privacy-service/home.md): Consente alle organizzazioni di automatizzare la conformità alle normative sulla privacy dei dati che coinvolgono i dati dei clienti all&#39;interno di  [!DNL Platform].

## Mixins di rinuncia

Per soddisfare le richieste di rinuncia CCPA, uno degli schemi che fa parte dello schema di unione deve contenere i campi di rinuncia [!DNL Experience Data Model] (XDM) necessari. Esistono due mixin che possono essere utilizzati per aggiungere campi di rinuncia a uno schema, ciascuno dei quali è trattato in modo più dettagliato nelle sezioni seguenti:

- [Privacy](#profile-privacy) profilo: Utilizzato per acquisire diversi tipi di rinuncia (generale o vendite/condivisione).
- [Dettagli](#profile-preferences-details) preferenze profilo: Utilizzato per acquisire richieste di rinuncia per canali XDM specifici.

Per istruzioni dettagliate su come aggiungere un mixin a uno schema, consulta la sezione &quot;Aggiungi un mixin&quot; nella seguente documentazione XDM:
- [Esercitazione API del Registro di sistema dello schema](../xdm/api/getting-started.md).: Creazione di uno schema tramite l’API del Registro di sistema dello schema.
- [Esercitazione](../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Creazione di uno schema tramite l’interfaccia utente di Platform.

Ecco un esempio di immagine che mostra i mixin di rinuncia aggiunti a uno schema nell’interfaccia utente:

![](images/opt-outs/opt-out-mixins-user-interface.png)

La struttura di ciascun mixin, nonché una descrizione dei campi che contribuiscono allo schema, sono descritte più dettagliatamente nelle sezioni seguenti.

### [!DNL Profile Privacy] {#profile-privacy}

Il mixin [!DNL Profile Privacy] consente di acquisire due tipi di richieste di rinuncia CCPA da parte dei clienti:

1. Rinuncia generale
2. Rinuncia alla vendita/condivisione

![](images/opt-outs/profile-privacy.png)

Il mixin [!DNL Profile Privacy] contiene i campi seguenti:

- Rinuncia alla privacy (`privacyOptOuts`): Matrice contenente un elenco di oggetti di rinuncia.
- Tipo di rinuncia (`optOutType`): Tipo di rinuncia. Questo campo è un enum con due possibili valori:
   - Rinuncia generale (`general_opt_out`)
   - Rinuncia alla condivisione delle vendite (`sales_sharing_opt_out`)
- Valore di rinuncia (`optOutValue`): Lo stato attivo della rinuncia, noto anche come valore del segnale di rinuncia, in base al tipo di rinuncia specificato. Questo campo è un enum con quattro possibili valori:
   - Non fornito (`not_provided`): Non è stata fornita una richiesta di rinuncia.
   - Verifica in sospeso (`pending`): La richiesta di rinuncia è in attesa di verifica.
   - Rinuncia (`out`): Il cliente ha rinunciato.
   - Consenso (`in`): Il cliente ha acconsentito.
- Timestamp rinuncia (`timestamp`): Timestamp del segnale di rinuncia ricevuto.

Per visualizzare l’intera struttura del mixin [!DNL Profile Privacy], consulta l’ [archivio GitHub pubblico XDM](https://github.com/adobe/xdm/blob/master/schemas/context/profile-privacy.schema.json) o visualizza l’anteprima del mixin tramite l’interfaccia utente di Platform.

### [!DNL Profile Preferences Details] {#profile-preferences-details}

Il mixin [!DNL Profile Preferences Details] fornisce diversi campi che rappresentano le preferenze per i profili dei clienti (ad esempio il formato e-mail, la lingua preferita e il fuso orario). Uno dei campi inclusi in questo mixin, OptInOut (`optInOut`), consente di impostare i valori di rinuncia per i singoli canali.

![](images/opt-outs/profile-preferences-details.png)

Il mixin [!DNL Profile Preferences Details] contiene i seguenti campi relativi alle rinunce:

- OptInOut (`optInOut`): Un oggetto in cui ogni chiave rappresenta un URI valido e noto per un canale di comunicazione e lo stato attivo della rinuncia per ciascun canale. Ogni canale può avere uno dei quattro valori possibili:
   - Non fornito (`not_provided`): Per questo canale non è stata fornita una richiesta di rinuncia.
   - Verifica in sospeso (`pending`): La richiesta di rinuncia per questo canale è in attesa di verifica.
   - Rinuncia (`out`): Il cliente ha rinunciato a questo canale.
   - Consenso (`in`): Il cliente ha acconsentito a questo canale.
- Rinuncia globale (`globalOptout`): Valore booleano che, se impostato su true, imposta un override di rinuncia globale per il profilo. Il valore predefinito per questo campo è false.

L&#39;esempio JSON riportato di seguito evidenzia come l&#39;oggetto OptInOut può acquisire più segnali di rinuncia per diversi canali di comunicazione:

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

Per visualizzare l&#39;intera struttura del mixin Dettagli preferenze profilo, visita l&#39; [archivio GitHub pubblico XDM](https://github.com/adobe/xdm/blob/master/schemas/context/profile-preferences-details.schema.json) o visualizza l&#39;anteprima del mixin utilizzando l&#39;interfaccia utente [!DNL Platform].

## Gestione delle rinunce nella segmentazione

Per evitare che i profili contrassegnati con i flag di rinuncia CCPA siano inclusi nei segmenti, è necessario aggiungere campi speciali ai segmenti esistenti o includerli durante la creazione dei segmenti.

Le sezioni seguenti mostrano come aggiungere i campi appropriati per i due tipi di flag di rinuncia:
1. Rinuncia generale
2. Rinuncia alla vendita/condivisione

### Rinuncia generale

[!DNL Segmentation] rispetta automaticamente tutti i profili contenenti il flag &quot;[!UICONTROL General Opt-Out]&quot;, il che significa che tali profili non saranno inclusi per impostazione predefinita nei tipi di pubblico o nelle esportazioni. Tuttavia, è consigliabile aggiungere i campi appropriati per garantire che i profili di rinuncia non siano inclusi nelle attività di pubblico e marketing.

Puoi eseguire questa operazione utilizzando l’interfaccia utente aggiungendo gli attributi **[!UICONTROL Privacy Opt-Outs]** . In questo caso, il segmento è impostato per includere solo coloro che hanno acconsentito (ovvero non hanno un flag generale di rinuncia sul profilo). Questo viene fatto dichiarando che &quot;[!UICONTROL Opt-Out Type]&quot; è uguale a &quot;[!UICONTROL General Opt-Out]&quot; e &quot;[!UICONTROL Opt-Out Value]&quot; è uguale a &quot;[!UICONTROL Opt-in]&quot;.

![](images/opt-outs/segment-general-opt-out.png)

### Rinuncia alla vendita/condivisione

Se un utente ha un flag di rinuncia alle vendite/condivisione impostato sul proprio profilo, questo profilo non deve più essere utilizzato per alcuna attività di creazione o marketing di segmenti. Per rispettare questo flag, &quot;[!UICONTROL Opt-Out Type]&quot; deve essere uguale a &quot;[!UICONTROL Sales Sharing Opt-Out]&quot; e &quot;[!UICONTROL Opt-Out Value]&quot; deve essere uguale a &quot;[!UICONTROL Opt-in]&quot;.

![](images/opt-outs/segment-sales-sharing-opt-out.png)

<!-- ### Overriding default exclusions

In some instances, such as building a segment of people who have opted out, it may be necessary to override the default exclusion of opted-out profiles. This override can be done via the API or in the Segment Builder user interface. -->

## Passaggi successivi

Per ulteriori informazioni sulla segmentazione, compreso il lavoro con le definizioni dei segmenti e i tipi di pubblico tramite l’API e l’interfaccia utente, per favore, inizia leggendo la [panoramica sulla segmentazione](./home.md).

Per ulteriori informazioni sulla privacy dei dati all&#39;interno di [!DNL Platform], incluso in che modo [!DNL Privacy Service] aiuta a facilitare la conformità automatica alle normative legali e organizzative sulla privacy, fai riferimento alla documentazione su [[!DNL Privacy Service]](../privacy-service/home.md).
