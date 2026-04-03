---
title: Supporto dell’identità unificata nella raccolta dati
description: Scopri in che modo il supporto dell’identità unificata riunisce la persistenza di prime parti e l’attivazione di terze parti supportata nella raccolta di dati web.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 32c2565d31eed4eda28195afaf82aac6f04a6f8a
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 3%

---

# Supporto dell’identità unificata nella raccolta dati

>[!AVAILABILITY]
>
>Questa funzione è attualmente in versione beta. La disponibilità, il comportamento e la documentazione possono cambiare.

Il supporto dell’identità unificata consente ad Edge Network di funzionare sia nel contesto di identità di prima parte che in quello di terze parti. Combina un’identificazione di prima parte durevole sulle proprietà di tua proprietà con flussi di lavoro di attivazione di terze parti nei browser che supportano i cookie di terze parti. Per informazioni generali sulla gestione di ECID, FPID e altri segnali di identità da parte del Web SDK, vedere [Identità nella raccolta dati](./overview.md).

Con il supporto per le identità unificate, puoi:

* **Massimizza la portata del pubblico**: attiva i tipi di pubblico di Experience Platform su destinazioni di terze parti (DSP, SSP, reti pubblicitarie) per una quota maggiore del traffico.
* **Mantenere la precisione di misurazione**: assicurati che l&#39;identificazione dei visitatori nelle tue proprietà e nelle tue piattaforme pubblicitarie sia coerente.
* **Implementazione a prova di futuro**: utilizza gli ID dispositivo di prime parti come base, mantenendo la compatibilità con i flussi di lavoro di attivazione di terze parti.

Quando un visitatore arriva sul tuo sito, Edge Network valuta i segnali di identità disponibili, collegando automaticamente i contesti di prime e terze parti quando le condizioni lo consentono. I browser che bloccano i cookie di terze parti continuano a funzionare in modalità di prime parti senza interrompere l’implementazione.

## Come funziona

Edge Network genera gli ECID valutando i segnali di identità disponibili nel seguente ordine di priorità:

| Priorità | Origine | Contesto | Comportamento |
| --- | --- | --- | --- |
| 1 | **ID demdex** | Terze parti | Se è presente un ID Demdex, l’ECID viene derivato da esso. Questo seed genera un ECID coerente tra i domini che condividono lo stesso cookie di terze parti. |
| 2 | **FPID** | Prime parti | Se non è presente alcun ID demdex ma esiste un FPID, l’ECID viene derivato dall’FPID e da questo deriva un ID demdex. |
| 3 | **Random** | Prime parti | Se non è disponibile né un ID Demdex né un FPID, viene generato un nuovo ECID casuale e da esso viene derivato un ID Demdex. |

Gli ECID e gli ID Demdex sono collegati crittograficamente attraverso un algoritmo deterministico, il che significa che uno può essere derivato dall&#39;altro. Questa relazione consente ad Edge Network di tradurre tra contesti di identità di prima parte e di terze parti senza richiedere una logica di gestione del visitatore separata nell’implementazione.

Poiché la relazione è deterministica, i tipi di pubblico basati su ECID di prime parti possono essere attivati tramite un’infrastruttura di terze parti quando è disponibile l’ID Demdex corrispondente.

Per i visitatori che dispongono già di un ECID derivato da FPID, Edge Network può collegare automaticamente la loro identità di prima parte al contesto di identità di terze parti. Questo accade in modo trasparente quando il browser supporta i cookie di terze parti e non richiede modifiche all’implementazione. Quando si verifica il collegamento automatico:

1. L’Edge Network rileva che l’ECID del visitatore non è derivato da un ID Demdex.
1. Se il browser del visitatore supporta i cookie di terze parti, viene attivata una sincronizzazione delle identità leggera.
1. Il sistema crea un collegamento tra l’ECID di prima parte del visitatore e la sua identità di terze parti.
1. Il collegamento viene archiviato nell’archivio delle identità, consentendo l’attivazione del pubblico su destinazioni di terze parti.

Il collegamento automatico mantiene gli ECID esistenti e impedisce il cliff dei visitatori. Nel tempo, una parte maggiore del pubblico diventa gradualmente idonea all’attivazione di terze parti man mano che i visitatori ritornano e si verificano i collegamenti.

L’attivazione di un pubblico di terze parti si basa sulla sincronizzazione ID (sincronizzazione ID). Quando Edge Network stabilisce o aggiorna un’identità di terze parti, restituisce le istruzioni di sincronizzazione ID nella risposta. Queste istruzioni indirizzano il browser per sincronizzare l’identità del visitatore con i domini partner (DSP, reti di annunci e altre piattaforme di attivazione), in modo che i tipi di pubblico di Experience Platform possano corrispondere e essere distribuiti su tali piattaforme.

## Prerequisiti

Il supporto per le identità unificate richiede tutti i seguenti elementi:

* Il sito utilizza la raccolta dati di prime parti in un dominio controllato.
* La tua implementazione utilizza come base gli FPID o un’altra strategia di persistenza di prime parti.
* I cookie di terze parti sono abilitati nella configurazione del Web SDK.
* La sincronizzazione ID di terze parti è abilitata per lo stream di dati.
* Il visitatore utilizza un browser che consente i cookie di terze parti (vedi [Compatibilità del browser](#browser-compatibility) di seguito).

## Configurazione

1. **Abilitare i cookie di terze parti in Web SDK**: abilitare l&#39;impostazione **Utilizzare i cookie di terze parti** nell&#39;implementazione di Web SDK. Se utilizzi l&#39;estensione tag, abilita **[!UICONTROL Use third-party cookies]** in [Impostazioni configurazione identità](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies). Se si utilizza la libreria JavaScript, impostare [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md) su `true`.

1. **Abilita sincronizzazione ID di terze parti nello stream di dati**: abilita l&#39;opzione **[!UICONTROL Third-Party ID Sync]** nelle impostazioni avanzate dello stream di dati. Consulta [Creare e configurare gli stream di dati](/help/datastreams/configure.md#advanced-options).

1. **Assicurati che la persistenza di prime parti sia attiva**: verifica che la tua strategia di persistenza di prime parti (come gli FPID) sia già distribuita nel tuo dominio di proprietà. Vedi [ID dispositivo di prime parti nella raccolta dati](fpid.md).

## Convalida

Per verificare il corretto funzionamento del supporto dell’identità unificata:

1. Apri gli strumenti di sviluppo del browser e passa alla scheda **Rete**.
1. Cancella le richieste esistenti e attiva un evento Web SDK (caricamento pagina o evento personalizzato) in una sessione nuova o in incognito.
1. Trova la risposta di Edge Network (cerca le chiamate a `adobedc.demdex.net` e l&#39;endpoint di raccolta di prime parti).
1. Ispeziona il payload di risposta per le istruzioni di sincronizzazione ID.

Quando sono presenti istruzioni di sincronizzazione ID, la risposta include un handle `identity:exchange` simile al seguente:

```json
{
  "handle": [
    {
      "type": "identity:exchange",
      "payload": [
        {
          "type": "url",
          "id": 411,
          "spec": {
            "url": "https://example.com/...",
            "hideReferrer": false,
            "ttlMinutes": 10080
          }
        },
        {
          "type": "url",
          "id": 89,
          "spec": {
            "url": "https://example.org/...",
            "hideReferrer": true,
            "ttlMinutes": 10080
          }
        }
      ]
    }
  ]
}
```

| Elemento | Descrizione |
| --- | --- |
| `type: "identity:exchange"` | Indica che sono presenti istruzioni di sincronizzazione ID. |
| Array `payload` | Elenco degli URL di sincronizzazione ID partner. |
| `url` valori | Reindirizza gli URL ai domini partner per la sincronizzazione ID. |
| `id` valori | Identificatori dei partner. |

>[!TIP]
>
>Se nella risposta non viene visualizzato l&#39;handle `identity:exchange`:
>
>* Assicurati di eseguire il test con una sessione del browser nuova o in incognito. Le identità esistenti non attivano nuove sincronizzazioni.
>* Verifica che le impostazioni dello stream di dati e di Web SDK siano configurate correttamente.
>* Conferma di utilizzare un browser che supporta i cookie di terze parti (consulta la tabella seguente).

Dopo aver confermato l’attività di sincronizzazione ID, verifica che:

* L’identità di prima parte persiste come previsto nei vari caricamenti di pagina sul dominio di proprietà.
* Negli ambienti supportati, i flussi di attivazione e reporting si comportano come previsto.

## Compatibilità browser {#browser-compatibility}

Le funzioni di identità di terze parti dipendono dal supporto del browser per i cookie di terze parti. La tabella seguente riepiloga il comportamento previsto:

| Browser | Supporto di cookie di terze parti | Demdex disponibile | Comportamento identità |
| --- | --- | --- | --- |
| Google Chrome | Supportato | Sì | Demdex → ECID (coerente tra domini diversi) |
| Microsoft Edge | Supportato per impostazione predefinita | Sì | Demdex → ECID (coerente tra domini diversi) |
| Mozilla Firefox | Bloccato per impostazione predefinita (ETP) | No (per impostazione predefinita) | FPID → ECID (per dominio) |
| Apple Safari | Bloccato (ITP) | No | FPID → ECID (per dominio) |

Per i browser che bloccano i cookie di terze parti, l’identificazione di prima parte continua a funzionare normalmente. Le funzioni di attivazione di terze parti sono disponibili solo se il browser consente i cookie di terze parti.

## Limitazioni

* Il comportamento di identità di terze parti dipende interamente dal browser del visitatore che consente i cookie di terze parti. Non esiste alcun fallback per l’attivazione di terze parti nei browser che li bloccano.
* Il collegamento automatico richiede che il visitatore torni al sito. La quota di pubblico idonea per l’attivazione di terze parti aumenta gradualmente nel tempo.
