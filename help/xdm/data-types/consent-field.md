---
solution: Experience Platform
title: Tipo di dati campo di consenso generico
topic: ' - Panoramica'
description: Questo documento fornisce una panoramica del tipo di dati XDM del campo di consenso generico.
translation-type: tm+mt
source-git-commit: ebcd8900687b6e91d3f06690a9db0e118bbc3b58
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 2%

---


# [!UICONTROL Generic Consent Field] tipo di dati

[!UICONTROL Generic Consent Field] è un tipo di dati XDM standard che descrive la selezione di un cliente per una particolare preferenza di consenso.

>[!NOTE]
>
>Questo tipo di dati è destinato a essere utilizzato per personalizzare la struttura degli schemi di consenso dell’organizzazione utilizzando il mixin [[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)]](../mixins/profile/consents.md) come linea di base.

![](../images/data-types/consent-field.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `val` | Stringa | La scelta del consenso fornito dal cliente per questo caso d’uso. Vedi la tabella seguente per i valori e le definizioni accettati. |

La tabella seguente illustra i valori accettati per `val`:

| Valore | Title | Descrizione |
| --- | --- | --- |
| `y` | Sì | Il cliente ha acconsentito. In altre parole, **do** acconsentono all&#39;uso dei propri dati come indicato dal consenso in questione. |
| `n` | No | Il cliente ha rinunciato al consenso. In altre parole, **non** acconsentono all&#39;uso dei propri dati come indicato dal consenso in questione. |
| `p` | Verifica in sospeso | Il sistema non ha ancora ricevuto un valore finale di consenso. Viene utilizzato più spesso come parte di un consenso che richiede una verifica in due fasi. Ad esempio, se un cliente sceglie di ricevere le e-mail, il consenso viene impostato su `p` fino a quando non seleziona un collegamento in un’e-mail per verificare di aver fornito l’indirizzo e-mail corretto, al punto in cui il consenso viene aggiornato a `y`.<br><br>Se questo consenso non utilizza un processo di verifica a due set, la  `p` scelta può essere invece utilizzata per indicare che il cliente non ha ancora risposto al prompt del consenso. Ad esempio, puoi impostare automaticamente il valore su `p` nella prima pagina di un sito web, prima che il cliente risponda al prompt del consenso. Nelle giurisdizioni che non richiedono un consenso esplicito, puoi anche utilizzarlo per indicare che il cliente non ha esplicitamente rinunciato (in altre parole, si presume che il consenso sia). |
| `u` | Sconosciuto | Le informazioni sul consenso del cliente sono sconosciute. |
| `LI` | Interesse legittimo | Il legittimo interesse commerciale a raccogliere ed elaborare tali dati per lo scopo specificato supera il potenziale danno che essi comportano per l&#39;individuo. |
| `CT` | Contratto | La raccolta dei dati per lo scopo specificato è necessaria per adempiere agli obblighi contrattuali con la persona fisica. |
| `CP` | Rispetto di un obbligo giuridico | La raccolta dei dati per lo scopo specificato è necessaria per soddisfare gli obblighi legali dell&#39;impresa. |
| `VI` | Interesse fondamentale del singolo | La raccolta dei dati per lo scopo specifico è necessaria per tutelare gli interessi vitali dell&#39;individuo. |
| `PI` | Interesse pubblico | La raccolta dei dati per lo scopo specificato è necessaria per svolgere un compito di interesse pubblico o nell&#39;esercizio di un&#39;autorità ufficiale. |

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.schema.json)