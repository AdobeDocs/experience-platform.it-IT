---
solution: Experience Platform
title: Campo Preferenza Di Marketing Generica Con Tipo Di Dati Sottoscrizioni
description: Scopri il campo delle preferenze di marketing generiche con il tipo di dati XDM delle sottoscrizioni.
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 1%

---

# [!UICONTROL Campo preferenza di marketing generico con tipo di dati Sottoscrizioni]

[!UICONTROL Il campo delle preferenze di marketing generiche con abbonamenti] è un tipo di dati XDM standard che descrive la selezione di un cliente per una particolare preferenza di marketing.

>[!NOTE]
>
>Questo tipo di dati è destinato a essere utilizzato per personalizzare la struttura degli schemi di consenso della tua organizzazione utilizzando come base di riferimento il gruppo di campi [[!UICONTROL Consensi e preferenze]](../field-groups/profile/consents.md).
>
>Se non è necessaria una mappa `subscriptions` per un particolare campo delle preferenze di marketing, è possibile utilizzare il tipo di dati [campo di marketing di base](./marketing-field.md).

![](../images/data-types/marketing-field-subscriptions.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `reason` | Stringa | Quando un cliente rinuncia a un caso di utilizzo di marketing, questo campo stringa rappresenta il motivo per cui il cliente ha rinunciato. |
| `subscriptions` | Mappa | Una mappa delle preferenze di marketing dei clienti per abbonamenti specifici. Per ulteriori informazioni, vedere la sezione relativa alle [sottoscrizioni](#subscriptions). |
| `time` | Data e ora | Una marca temporale ISO 8601 indicante quando la preferenza di marketing è cambiata, se applicabile. |
| `val` | Stringa | Scelta preferenziale fornita dal cliente per questo caso d’uso di marketing. Per informazioni sui valori e le definizioni accettati, consulta la [sezione successiva](#val). |

{style="table-layout:auto"}

## `val` {#val}

La tabella seguente illustra i valori accettati per `val`:

| Valore | Titolo | Descrizione |
| --- | --- | --- |
| `y` | Sì (consenso) | Il cliente ha acconsentito alla preferenza. In altre parole, **acconsentono** all&#39;utilizzo dei propri dati come indicato dalla preferenza in questione. |
| `n` | No (rinuncia) | Il cliente ha rinunciato alla preferenza. In altre parole, **non** acconsentono all&#39;utilizzo dei propri dati come indicato dalla preferenza in questione. |
| `p` | Verifica in sospeso | Il sistema non ha ancora ricevuto un valore di preferenza finale. Questo viene spesso utilizzato come parte di un consenso che richiede una verifica in due fasi. Ad esempio, se un cliente acconsente alla ricezione di e-mail, tale consenso viene impostato su `p` fino a quando non seleziona un collegamento in un messaggio e-mail per verificare di aver fornito l&#39;indirizzo e-mail corretto, nel qual caso il consenso verrà aggiornato a `y`.<br><br>Se questa preferenza non utilizza un processo di verifica a due set, è possibile utilizzare la scelta `p` per indicare che il cliente non ha ancora risposto alla richiesta di consenso. Ad esempio, puoi impostare automaticamente il valore su `p` nella prima pagina di un sito Web, prima che il cliente abbia risposto alla richiesta di consenso. Nelle giurisdizioni che non richiedono il consenso esplicito, è possibile utilizzarlo anche per indicare che il cliente non ha esplicitamente rinunciato (in altre parole, si presume il consenso). |
| `u` | Sconosciuto | Informazioni sulle preferenze del cliente sconosciute. |
| `dy` | Predefinito di Sì (consenso) | Il cliente non ha fornito un valore di consenso e viene trattato come un consenso (&quot;Sì&quot;) per impostazione predefinita. In altre parole, si presume il consenso fino a quando il cliente non indica il contrario.<br><br>Se le leggi o le modifiche all&#39;informativa sulla privacy della tua azienda determinano modifiche alle impostazioni predefinite di alcuni o di tutti gli utenti, devi aggiornare manualmente tutti i profili contenenti i valori predefiniti. |
| `dn` | Predefinito per No (rinuncia) | Il cliente non ha fornito un valore di consenso e per impostazione predefinita viene trattato come una rinuncia (&quot;No&quot;). In altre parole, si presume che il cliente abbia negato il consenso fino a quando non indica diversamente.<br><br>Se le leggi o le modifiche all&#39;informativa sulla privacy della tua azienda determinano modifiche alle impostazioni predefinite di alcuni o di tutti gli utenti, devi aggiornare manualmente tutti i profili contenenti i valori predefiniti. |
| `LI` | Interesse legittimo | Il legittimo interesse commerciale a raccogliere e trattare tali dati per lo scopo specificato supera il potenziale danno che essi comportano per l’individuo. |
| `CT` | Contratto | La raccolta dei dati per lo scopo specificato è necessaria per adempiere agli obblighi contrattuali con la persona. |
| `CP` | Rispetto di un obbligo legale | La raccolta dei dati per lo scopo specificato è necessaria per soddisfare gli obblighi legali dell&#39;impresa. |
| `VI` | Interesse vitale dell&#39;individuo | La raccolta di dati per lo scopo specificato è necessaria per proteggere gli interessi vitali dell&#39;individuo. |
| `PI` | Interesse pubblico | La raccolta di dati per lo scopo specificato è necessaria per svolgere un compito di interesse pubblico o nell&#39;esercizio di pubblici poteri. |

{style="table-layout:auto"}

## `subscriptions` {#subscriptions}

Alcune aziende consentono ai clienti di fornire il consenso per diversi abbonamenti associati a un particolare canale di marketing. Ad esempio, una società bancaria può consentire ai clienti di abbonarsi agli avvisi telefonici per gli account sovrautilizzati o di ricevere chiamate di vendita per le offerte del programma fedeltà.

Il codice JSON seguente rappresenta un campo di marketing di esempio per un canale di marketing con telefonata contenente una mappa `subscriptions`. Ogni chiave nell&#39;oggetto `subscriptions` rappresenta una singola sottoscrizione per il canale di marketing. A sua volta, ogni sottoscrizione contiene un valore di consenso (`val`).

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
| `val` | Il [valore di consenso](#val) per la sottoscrizione. |
| `type` | Il tipo di abbonamento. Può essere una qualsiasi stringa descrittiva, purché non superi i 15 caratteri. |
| `topics` | Un array di stringhe che rappresentano le aree di interesse a cui un cliente è abbonato, che possono essere utilizzate per inviare loro contenuti rilevanti. |
| `subscribers` | Campo di tipo mappa facoltativo che rappresenta un set di identificatori (ad esempio indirizzi e-mail o numeri di telefono) abbonati a un abbonamento specifico. Ogni chiave in questo oggetto rappresenta l’identificatore in questione e contiene due sottoproprietà: <ul><li>`time`: una marca temporale ISO 8601 indicante quando l’identità è stata sottoscritta, se applicabile.</li><li>`source`: origine del sottoscrittore. Può essere una qualsiasi stringa descrittiva, purché non superi i 15 caratteri.</li></ul> |

{style="table-layout:auto"}

## Risorse aggiuntive

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
