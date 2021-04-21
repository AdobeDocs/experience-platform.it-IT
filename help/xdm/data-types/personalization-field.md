---
solution: Experience Platform
title: Tipo di dati campo preferenza personalizzazione generica
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM del campo delle preferenze di personalizzazione generica.
exl-id: 3f6a3c31-19f3-4bad-921e-9ad33c6b9ac9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# [!UICONTROL Generic Personalization Preference Field] tipo di dati

[!UICONTROL Generic Personalization Preference Field] è un tipo di dati XDM standard che descrive la selezione di un cliente per una particolare preferenza di personalizzazione.

>[!NOTE]
>
>Questo tipo di dati è destinato a essere utilizzato per personalizzare la struttura degli schemi di consenso dell’organizzazione utilizzando il mixin [[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)]](../mixins/profile/consents.md) come linea di base.

![](../images/data-types/personalization-field.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `val` | Stringa | La scelta preferenziale fornita dal cliente per questo caso di utilizzo di personalizzazione. Vedi la tabella seguente per i valori e le definizioni accettati. |

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

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.schema.json)
