---
solution: Experience Platform
title: Campo Preferenza Di Marketing Generico Con Tipo Di Dati Di Abbonamento
topic-legacy: overview
description: Questo documento fornisce una panoramica del campo Preferenze di marketing generiche con tipo di dati XDM sottoscrizioni.
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: bd312024a1a3fb6da840a38d6e9d19fcbd6eab5a
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 3%

---

# [!UICONTROL Campo preferenza di marketing generico con tipo di dati ] Subscriptionsdata

[!UICONTROL Campo preferenza marketing generico con ] sottoscrizione è un tipo di dati XDM standard che descrive la selezione di un cliente per una particolare preferenza di marketing.

>[!NOTE]
>
>Questo tipo di dati è destinato a essere utilizzato per personalizzare la struttura degli schemi di consenso dell&#39;organizzazione utilizzando il gruppo di campi [[!UICONTROL Consensi e preferenze]](../field-groups/profile/consents.md) come linea di base.
>
>Se non hai bisogno di una mappatura `subscriptions` per un particolare campo delle preferenze di marketing, puoi invece utilizzare il tipo di dati del campo di marketing [base](./marketing-field.md).

![](../images/data-types/marketing-field-subscriptions.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `reason` | Stringa | Quando un cliente rinuncia a un caso di utilizzo marketing, questo campo stringa rappresenta il motivo per cui il cliente ha rinunciato. |
| `subscriptions` | Mappa | Mappa delle preferenze di marketing dei clienti per abbonamenti specifici. Per ulteriori informazioni, consulta la sezione sulle [sottoscrizioni](#subscriptions) . |
| `time` | DateTime | Una marca temporale ISO 8601 di quando la preferenza di marketing è cambiata, se applicabile. |
| `val` | Stringa | La scelta della preferenza fornita dal cliente per questo caso d’uso di marketing. Per i valori e le definizioni accettati, consulta la sezione [successiva](#val) . |

{style=&quot;table-layout:auto&quot;}

## `val` {#val}

La tabella seguente illustra i valori accettati per `val`:

| Valore | Title | Descrizione |
| --- | --- | --- |
| `y` | Sì | Il cliente ha acconsentito alla preferenza. In altre parole, **do** acconsentono all&#39;uso dei propri dati come indicato dalla preferenza in questione. |
| `n` | No | Il cliente ha rinunciato alla preferenza. In altre parole, **non** acconsentono all&#39;uso dei propri dati come indicato dalla preferenza in questione. |
| `p` | Verifica in sospeso | Il sistema non ha ancora ricevuto un valore di preferenza finale. Viene utilizzato più spesso come parte di un consenso che richiede una verifica in due fasi. Ad esempio, se un cliente sceglie di ricevere le e-mail, il consenso viene impostato su `p` fino a quando non seleziona un collegamento in un’e-mail per verificare di aver fornito l’indirizzo e-mail corretto, al punto in cui il consenso viene aggiornato a `y`.<br><br>Se questa preferenza non utilizza un processo di verifica a due set, è possibile utilizzare la  `p` scelta per indicare che il cliente non ha ancora risposto al prompt del consenso. Ad esempio, puoi impostare automaticamente il valore su `p` nella prima pagina di un sito web, prima che il cliente risponda al prompt del consenso. Nelle giurisdizioni che non richiedono un consenso esplicito, puoi anche utilizzarlo per indicare che il cliente non ha esplicitamente rinunciato (in altre parole, si presume che il consenso sia). |
| `u` | Sconosciuto | Informazioni sulle preferenze del cliente sconosciute. |
| `LI` | Interesse legittimo | Il legittimo interesse commerciale a raccogliere ed elaborare tali dati per lo scopo specificato supera il potenziale danno che essi comportano per l&#39;individuo. |
| `CT` | Contratto | La raccolta dei dati per lo scopo specificato è necessaria per adempiere agli obblighi contrattuali con la persona fisica. |
| `CP` | Rispetto di un obbligo giuridico | La raccolta dei dati per lo scopo specificato è necessaria per soddisfare gli obblighi legali dell&#39;impresa. |
| `VI` | Interesse fondamentale del singolo | La raccolta dei dati per lo scopo specifico è necessaria per tutelare gli interessi vitali dell&#39;individuo. |
| `PI` | Interesse pubblico | La raccolta dei dati per lo scopo specificato è necessaria per svolgere un compito di interesse pubblico o nell&#39;esercizio di un&#39;autorità ufficiale. |

{style=&quot;table-layout:auto&quot;}

## `subscriptions` {#subscriptions}

Alcune aziende consentono ai clienti di effettuare l’opt-in per iscrizioni diverse associate a un particolare canale di marketing. Ad esempio, una società bancaria può consentire ai clienti di abbonarsi a avvisi telefonici per conti non utilizzati o ricevere chiamate di vendita per offerte di programmi fedeltà.

Il seguente JSON rappresenta un campo di marketing di esempio per un canale di marketing con chiamata telefonica che contiene una mappa `subscriptions`. Ogni chiave nell’oggetto `subscriptions` rappresenta una sottoscrizione individuale per il canale di marketing. A sua volta, ogni abbonamento contiene un valore di consenso (`val`).

```json
"phone-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "subscribers": {
        "123-555-0928": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "overdrawn-account": {
      "val": "y",
      "type": "issues",
      "subscribers": {
        "123-555-0928": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "301-555-1527": {
          "time": "2020-02-03T07:54:21+07:00",
          "source": "call center"
        }
      }
    }
  }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `type` | Tipo di sottoscrizione. Può trattarsi di una qualsiasi stringa descrittiva, purché non contenga più di 15 caratteri. |
| `subscribers` | Un campo di tipo mappa facoltativo che rappresenta un insieme di identificatori (ad esempio indirizzi e-mail o numeri di telefono) che hanno effettuato la sottoscrizione a una particolare sottoscrizione. Ogni chiave in questo oggetto rappresenta l&#39;identificatore in questione e contiene due sottoproprietà: <ul><li>`time`: Una marca temporale ISO 8601 del momento in cui l’identità è stata sottoscritta, se applicabile.</li><li>`source`: Origine dell&#39;utente che ha effettuato l&#39;abbonamento. Può trattarsi di una qualsiasi stringa descrittiva, purché non contenga più di 15 caratteri.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Risorse aggiuntive

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
