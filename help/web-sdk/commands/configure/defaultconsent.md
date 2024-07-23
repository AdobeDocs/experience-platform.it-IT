---
title: defaultConsent
description: Imposta il metodo predefinito di raccolta dei consensi per la proprietà web.
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 5%

---


# `defaultConsent`

La proprietà `defaultConsent` determina la modalità di gestione del consenso alla raccolta dati prima di chiamare il comando [`setConsent`](../setconsent.md). Questa proprietà è utile quando non desideri raccogliere accidentalmente dati da individui residenti in aree in cui è richiesto il consenso prima di raccogliere i dati.

Per impostazione predefinita, gli utenti hanno acconsentito a tutte le finalità e l’SDK web è autorizzato a eseguire le attività seguenti:

* Invia dati a e dai server di Adobe.
* Leggi e scrivi cookie o elementi di archiviazione web.

Se gli utenti rinunciano a tutte le attività, l’SDK Web non esegue alcuna di queste attività.

La proprietà `defaultConsent` supporta tre valori:

* **`in`**: la raccolta dati procede come di consueto, fino a quando l&#39;utente non rinuncia.
* **`out`**: i dati vengono eliminati definitivamente fino al consenso dell&#39;utente.
* **`pending`**: i dati vengono archiviati localmente finché l&#39;utente non acconsente utilizzando il comando [`setConsent`](../setconsent.md). Quando il consenso predefinito per lo scopo generale è impostato su `pending`, il tentativo di eseguire comandi che dipendono dalle preferenze di consenso dell&#39;utente (ad esempio, il comando [`sendEvent`](../sendevent/overview.md)) fa sì che il comando venga accodato nell&#39;SDK Web. I comandi in coda vengono elaborati solo dopo aver comunicato le preferenze di consenso dell’utente all’SDK per web.

>[!NOTE]
>
> I dati di consenso non persistono tra i caricamenti di pagina.

Se un visitatore non rientra nella giurisdizione del Regolamento generale sulla protezione dei dati (RGPD), il consenso predefinito può essere impostato su `in`. Per i visitatori all&#39;interno della giurisdizione del RGPD il consenso predefinito potrebbe essere impostato su `pending`. La piattaforma di gestione del consenso (CMP) è in grado di rilevare l&#39;area geografica del cliente e fornire il flag `gdprApplies` a IAB TCF 2.0. Questo flag può essere utilizzato per impostare il consenso predefinito.

Se non desideri raccogliere gli eventi che si sono verificati prima che le preferenze di consenso dell&#39;utente siano impostate, puoi passare `"defaultConsent": "out"` durante la configurazione dell&#39;SDK Web. Il tentativo di eseguire comandi che dipendono dalle preferenze di consenso dell’utente non avrà alcun effetto finché non avrai comunicato le preferenze di consenso dell’utente all’SDK per web.

>[!NOTE]
>
>Attualmente, Web SDK supporta solo un singolo scopo &quot;tutto o niente&quot;. Anche se prevediamo di creare una serie più solida di finalità o categorie corrispondenti alle diverse funzionalità Adobe e offerte di prodotti, l’implementazione corrente è un approccio &quot;tutto o niente&quot; all’opt-in.  Questo vale solo per [!DNL Web SDK] e NON per altre librerie JavaScript di Adobe.

## Utilizzo di `defaultConsent` insieme a `setConsent` {#using-consent}

L’SDK per web offre due comandi di configurazione del consenso complementari:

* [`defaultConsent`](defaultconsent.md): questo comando ha lo scopo di acquisire le preferenze di consenso dei clienti Adobe utilizzando Web SDK.
* [`setConsent`](../setconsent.md): questo comando ha lo scopo di acquisire le preferenze di consenso dei visitatori del tuo sito.

Se utilizzate insieme, queste impostazioni possono portare a risultati diversi di raccolta dati e impostazione dei cookie, a seconda dei valori configurati.

Vedi la tabella seguente per capire quando si verifica la raccolta dei dati e quando vengono impostati i cookie, in base alle impostazioni del consenso.

| defaultConsent | setConsent | La raccolta dei dati avviene | Web SDK imposta i cookie del browser |
|---------|----------|---------|---------|
| `in` | `in` | Sì | Sì |
| `in` | `out` | No | Sì |
| `in` | Non impostato | Sì | Sì |
| `pending` | `in` | Sì | Sì |
| `pending` | `out` | No | Sì |
| `pending` | Non impostato | No | No |
| `out` | `in` | Sì | Sì |
| `out` | `out` | No | Sì |
| `out` | Non impostato | No | No |

I seguenti cookie vengono impostati quando la configurazione del consenso consente:

| Nome | Età massima | Descrizione |
|---|---|---|
| **AMCV_###@AdobeOrg** | 34128000 (395 giorni) | Presente quando [`idMigrationEnabled`](../configure/idmigrationenabled.md) è abilitato. È utile per la transizione a Web SDK quando alcune parti del sito utilizzano ancora `visitor.js`. |
| **Cookie demdex** | 15552000 (180 giorni) | Presente se la sincronizzazione ID è abilitata. L’Audience Manager imposta questo cookie per assegnare un ID univoco a un visitatore del sito. Il cookie demdex aiuta Audience Manager a eseguire funzioni di base come l’identificazione dei visitatori, la sincronizzazione degli ID, la segmentazione, la modellazione, il reporting e così via. |
| **kndctr_orgid_cluster** | 1800 (30 minuti) | Memorizza l&#39;area dell&#39;Edge Network che soddisfa le richieste dell&#39;utente corrente. L’area viene utilizzata nel percorso URL in modo che l’Edge Network possa indirizzare la richiesta all’area corretta. Se un utente si connette con un indirizzo IP diverso o in una sessione diversa, la richiesta viene nuovamente indirizzata all’area più vicina. |
| **kndct_orgid_identity** | 34128000 (395 giorni) | Memorizza l’ECID, così come altre informazioni relative all’ECID. |
| **kndctr_orgid_consent** | 15552000 (180 giorni) | Memorizza le preferenze di consenso degli utenti per il sito Web. |
| **s_ecid** | 63115200 (2 anni) | Contiene una copia dell&#39;ID Experience Cloud ([!DNL ECID]) o del MID. Il MID viene memorizzato in una coppia chiave/valore con sintassi `s_ecid=MCMID\|<ECID>`. |

## Impostare il consenso predefinito tramite l’estensione tag Web SDK

Selezionare il pulsante di opzione desiderato in **[!UICONTROL Consenso predefinito]** durante [la configurazione dell&#39;estensione tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione [!UICONTROL Privacy], quindi seleziona il **[!UICONTROL consenso predefinito]** desiderato.
1. Fai clic su **[!UICONTROL Salva]**, quindi pubblica le modifiche.

## Impostare il consenso predefinito utilizzando la libreria JavaScript dell’SDK per web

Impostare la proprietà stringa `defaultConsent` sul livello di consenso desiderato durante l&#39;esecuzione del comando `configure`. Questa proprietà fa distinzione tra maiuscole e minuscole e supporta solo i tre valori seguenti: `"in"`, `"out"` e `"pending"`. Se tenti di utilizzare un altro valore, la libreria genera un errore.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  defaultConsent: "pending"
});
```
