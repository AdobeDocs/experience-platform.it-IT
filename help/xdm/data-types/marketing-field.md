---
solution: Experience Platform
title: Tipo di dati campo preferenza di marketing generico
description: Questo documento fornisce una panoramica del tipo di dati XDM del campo preferenza di marketing generico.
exl-id: d4c53885-f34f-4721-aa34-1fe02dc7006f
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 2%

---

# [!UICONTROL Campo preferenza marketing generico] tipo di dati

[!UICONTROL Campo preferenza marketing generico] è un tipo di dati XDM standard che descrive la selezione di un cliente per una particolare preferenza di marketing.

>[!NOTE]
>
>Questo tipo di dati è destinato a essere utilizzato per personalizzare la struttura degli schemi di consenso della tua organizzazione utilizzando il [[!UICONTROL Consensi e preferenze] gruppo di campi](../field-groups/profile/consents.md) come linea di base.
>
>Se hai bisogno di un `subscriptions` mappatura per un particolare campo delle preferenze di marketing, è necessario utilizzare [campo di marketing con tipo di dati di sottoscrizioni](./marketing-field-subscriptions.md) invece.

![](../images/data-types/marketing-field.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `reason` | Stringa | Quando un cliente rinuncia a un caso di utilizzo marketing, questo campo stringa rappresenta il motivo per cui il cliente ha rinunciato. |
| `time` | DateTime | Una marca temporale ISO 8601 di quando la preferenza di marketing è cambiata, se applicabile. |
| `val` | Stringa | La scelta della preferenza fornita dal cliente per questo caso d’uso di marketing. Vedi la tabella seguente per i valori e le definizioni accettati. |

{style=&quot;table-layout:auto&quot;}

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

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
