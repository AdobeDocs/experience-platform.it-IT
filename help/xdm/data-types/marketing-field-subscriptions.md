---
solution: Experience Platform
title: Campo Preferenza Di Marketing Generico Con Tipo Di Dati Di Abbonamento
description: Questo documento fornisce una panoramica del campo Preferenze di marketing generiche con tipo di dati XDM sottoscrizioni.
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 2%

---

# [!UICONTROL Campo preferenza marketing generico con sottoscrizioni] tipo di dati

[!UICONTROL Campo preferenza marketing generico con sottoscrizioni] è un tipo di dati XDM standard che descrive la selezione di un cliente per una particolare preferenza di marketing.

>[!NOTE]
>
>Questo tipo di dati è destinato a essere utilizzato per personalizzare la struttura degli schemi di consenso della tua organizzazione utilizzando il [[!UICONTROL Consensi e preferenze] gruppo di campi](../field-groups/profile/consents.md) come linea di base.
>
>Se non richiedi un `subscriptions` mappa per un particolare campo delle preferenze di marketing, puoi utilizzare la [tipo di dati del campo di marketing di base](./marketing-field.md) invece.

![](../images/data-types/marketing-field-subscriptions.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `reason` | Stringa | Quando un cliente rinuncia a un caso di utilizzo marketing, questo campo stringa rappresenta il motivo per cui il cliente ha rinunciato. |
| `subscriptions` | Mappa | Mappa delle preferenze di marketing dei clienti per abbonamenti specifici. Vedi la sezione su [abbonamenti](#subscriptions) per ulteriori informazioni. |
| `time` | DateTime | Una marca temporale ISO 8601 di quando la preferenza di marketing è cambiata, se applicabile. |
| `val` | Stringa | La scelta della preferenza fornita dal cliente per questo caso d’uso di marketing. Consulta la sezione [sezione successiva](#val) per i valori e le definizioni accettati. |

{style=&quot;table-layout:auto&quot;}

## `val` {#val}

La tabella seguente illustra i valori accettati per `val`:

| Valore | Title | Descrizione |
| --- | --- | --- |
| `y` | Sì (opt-in) | Il cliente ha acconsentito alla preferenza. In altre parole, **fare** il consenso all&#39;uso dei loro dati come indicato dalla preferenza in questione. |
| `n` | No (rinuncia) | Il cliente ha rinunciato alla preferenza. In altre parole, **non** il consenso all&#39;uso dei loro dati come indicato dalla preferenza in questione. |
| `p` | Verifica in sospeso | Il sistema non ha ancora ricevuto un valore di preferenza finale. Viene utilizzato più spesso come parte di un consenso che richiede una verifica in due fasi. Ad esempio, se un cliente sceglie di ricevere e-mail, il consenso viene impostato su `p` fino a quando non selezionano un collegamento in un’e-mail per verificare di aver fornito l’indirizzo e-mail corretto, al momento in cui il consenso viene aggiornato a `y`.<br><br>Se questa preferenza non utilizza un processo di verifica con due set, il `p` La scelta può essere invece utilizzata per indicare che il cliente non ha ancora risposto al prompt del consenso. Ad esempio, puoi impostare automaticamente il valore su `p` nella prima pagina di un sito web, prima che il cliente risponda al prompt del consenso. Nelle giurisdizioni che non richiedono un consenso esplicito, puoi anche utilizzarlo per indicare che il cliente non ha esplicitamente rinunciato (in altre parole, si presume che il consenso sia). |
| `u` | Sconosciuto | Informazioni sulle preferenze del cliente sconosciute. |
| `dy` | Impostazione predefinita di Sì (opt-in) | Il cliente non ha fornito direttamente il valore del consenso e viene trattato come un consenso (&quot;Sì&quot;) per impostazione predefinita. In altre parole, si presume il consenso finché il cliente non indica il contrario.<br><br>Tieni presente che se le leggi o le modifiche all’informativa sulla privacy della tua azienda determinano modifiche alle impostazioni predefinite di alcuni o tutti gli utenti, devi aggiornare manualmente tutti i profili contenenti valori predefiniti. |
| `dn` | Predefinito di No (rinuncia) | Il cliente non ha fornito direttamente il valore del consenso e viene trattato come una rinuncia (&quot;No&quot;) per impostazione predefinita. In altre parole, si presume che il cliente abbia negato il consenso fino a quando non ha indicato diversamente.<br><br>Tieni presente che se le leggi o le modifiche all’informativa sulla privacy della tua azienda determinano modifiche alle impostazioni predefinite di alcuni o tutti gli utenti, devi aggiornare manualmente tutti i profili contenenti valori predefiniti. |
| `LI` | Interesse legittimo | Il legittimo interesse commerciale a raccogliere ed elaborare tali dati per lo scopo specificato supera il potenziale danno che essi comportano per l&#39;individuo. |
| `CT` | Contratto | La raccolta dei dati per lo scopo specificato è necessaria per adempiere agli obblighi contrattuali con la persona fisica. |
| `CP` | Rispetto di un obbligo giuridico | La raccolta dei dati per lo scopo specificato è necessaria per soddisfare gli obblighi legali dell&#39;impresa. |
| `VI` | Interesse fondamentale del singolo | La raccolta dei dati per lo scopo specifico è necessaria per tutelare gli interessi vitali dell&#39;individuo. |
| `PI` | Interesse pubblico | La raccolta dei dati per lo scopo specificato è necessaria per svolgere un compito di interesse pubblico o nell&#39;esercizio di un&#39;autorità ufficiale. |

{style=&quot;table-layout:auto&quot;}

## `subscriptions` {#subscriptions}

Alcune aziende consentono ai clienti di effettuare l’opt-in per iscrizioni diverse associate a un particolare canale di marketing. Ad esempio, una società bancaria può consentire ai clienti di abbonarsi a avvisi telefonici per conti non utilizzati o ricevere chiamate di vendita per offerte di programmi fedeltà.

Il seguente JSON rappresenta un campo di marketing di esempio per un canale di marketing basato su chiamate telefoniche che contiene un `subscriptions` mappa. Ogni chiave nel `subscriptions` rappresenta una sottoscrizione individuale per il canale di marketing. A sua volta, ogni abbonamento contiene un valore di consenso (`val`).

```json
"email-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "topics": ["discounts", "early-access"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "newsletters": {
      "val": "y",
      "type": "advertising",
      "topics": ["hardware"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "tparan@example.com": {
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
| `val` | La [valore del consenso](#val) per l’abbonamento. |
| `type` | Tipo di sottoscrizione. Può trattarsi di una qualsiasi stringa descrittiva, purché non contenga più di 15 caratteri. |
| `topics` | Array di stringhe che rappresentano le aree di interesse a cui un cliente è iscritto, che possono essere utilizzate per inviare loro contenuti pertinenti. |
| `subscribers` | Un campo di tipo mappa facoltativo che rappresenta un insieme di identificatori (ad esempio indirizzi e-mail o numeri di telefono) che hanno effettuato la sottoscrizione a una particolare sottoscrizione. Ogni chiave in questo oggetto rappresenta l&#39;identificatore in questione e contiene due sottoproprietà: <ul><li>`time`: Una marca temporale ISO 8601 del momento in cui l’identità è stata sottoscritta, se applicabile.</li><li>`source`: Origine dell&#39;utente che ha effettuato l&#39;abbonamento. Può trattarsi di una qualsiasi stringa descrittiva, purché non contenga più di 15 caratteri.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Risorse aggiuntive

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
