---
solution: Experience Platform
title: Tipo di dati campo di consenso generico
description: Questo documento fornisce una panoramica del tipo di dati XDM per campo di consenso generico.
exl-id: f1f14eb7-21dd-45ca-8fb4-68f397cfa697
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 1%

---

# [!UICONTROL Campo di consenso generico] tipo di dati

[!UICONTROL Campo di consenso generico] è un tipo di dati XDM standard che descrive la selezione di un cliente per una particolare preferenza di consenso.

>[!NOTE]
>
>Questo tipo di dati è destinato a essere utilizzato per personalizzare la struttura degli schemi di consenso della tua organizzazione utilizzando [[!UICONTROL Consensi e preferenze] gruppo di campi](../field-groups/profile/consents.md) come base di riferimento.

![](../images/data-types/consent-field.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `val` | Stringa | La scelta del consenso fornito dal cliente per questo caso d’uso. Per i valori e le definizioni accettati, consulta la tabella seguente. |

{style="table-layout:auto"}

La tabella seguente illustra i valori accettati per `val`:

| Valore | Titolo | Descrizione |
| --- | --- | --- |
| `y` | Sì (consenso) | Il cliente ha acconsentito al consenso. In altre parole, **fare** acconsentire all’uso dei propri dati come indicato dal consenso in questione. |
| `n` | No (rinuncia) | Il cliente ha rinunciato al consenso. In altre parole, **non** acconsentire all’uso dei propri dati come indicato dal consenso in questione. |
| `p` | Verifica in sospeso | Il sistema non ha ancora ricevuto un valore di consenso finale. Questo viene spesso utilizzato come parte di un consenso che richiede una verifica in due fasi. Ad esempio, se un cliente acconsente alla ricezione di e-mail, il consenso viene impostato su `p` fino a quando non seleziona un collegamento in un’e-mail per verificare di aver fornito l’indirizzo e-mail corretto, dopodiché il consenso verrà aggiornato a `y`.<br><br>Se tale consenso non utilizza un processo di verifica a due insiemi, il `p` La scelta può invece essere utilizzata per indicare che il cliente non ha ancora risposto al prompt del consenso. Ad esempio, puoi impostare automaticamente il valore su `p` sulla prima pagina di un sito web, prima che il cliente abbia risposto al prompt del consenso. Nelle giurisdizioni che non richiedono il consenso esplicito, è possibile utilizzarlo anche per indicare che il cliente non ha esplicitamente rinunciato (in altre parole, si presume il consenso). |
| `u` | Sconosciuto | Le informazioni sul consenso del cliente sono sconosciute. |
| `dy` | Predefinito di Sì (consenso) | Il cliente non ha fornito un valore di consenso e viene trattato come un consenso (&quot;Sì&quot;) per impostazione predefinita. In altre parole, si presume il consenso fino a quando il cliente non indica il contrario.<br><br>Tieni presente che se le leggi o le modifiche all’informativa sulla privacy della tua azienda determinano modifiche alle impostazioni predefinite di alcuni o di tutti gli utenti, devi aggiornare manualmente tutti i profili contenenti i valori predefiniti. |
| `dn` | Predefinito per No (rinuncia) | Il cliente non ha fornito un valore di consenso e per impostazione predefinita viene trattato come una rinuncia (&quot;No&quot;). In altre parole, si presume che il cliente abbia negato il consenso fino a quando non indica diversamente.<br><br>Tieni presente che se le leggi o le modifiche all’informativa sulla privacy della tua azienda determinano modifiche alle impostazioni predefinite di alcuni o di tutti gli utenti, devi aggiornare manualmente tutti i profili contenenti i valori predefiniti. |
| `LI` | Interesse legittimo | Il legittimo interesse commerciale a raccogliere e trattare tali dati per lo scopo specificato supera il potenziale danno che essi comportano per l’individuo. |
| `CT` | Contratto | La raccolta dei dati per lo scopo specificato è necessaria per adempiere agli obblighi contrattuali con la persona. |
| `CP` | Rispetto di un obbligo legale | La raccolta dei dati per lo scopo specificato è necessaria per soddisfare gli obblighi legali dell&#39;impresa. |
| `VI` | Interesse vitale dell&#39;individuo | La raccolta di dati per lo scopo specificato è necessaria per proteggere gli interessi vitali dell&#39;individuo. |
| `PI` | Interesse pubblico | La raccolta di dati per lo scopo specificato è necessaria per svolgere un compito di interesse pubblico o nell&#39;esercizio di pubblici poteri. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.schema.json)
