---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Panoramica sul mixaggio della privacy
topic: guide
translation-type: tm+mt
source-git-commit: 02014c503dc9d4597e1129cafe3ba86f4abe37e9
workflow-type: tm+mt
source-wordcount: '1778'
ht-degree: 1%

---


# [!DNL Privacy Consent] panoramica del mixin

Il [!DNL Privacy/Marketing Preferences (Consent)] mixin (in seguito denominato &quot;[!DNL Privacy Consent] mixin&quot;) è un mixin [!DNL Experience Data Model] (XDM) destinato a supportare la raccolta di autorizzazioni e preferenze utente generate dai CMP e da altre fonti dei clienti. Il presente documento illustra la struttura e l&#39;uso previsto dei vari campi forniti dal mixin.

## Prerequisiti  {#prerequisites}

Questo documento richiede una conoscenza approfondita di [!DNL Experience Data Model] (XDM) e dell&#39;utilizzo degli schemi in [!DNL Experience Platform]. Prima di continuare, consulta la seguente documentazione:

* [Panoramica del sistema XDM](http://www.adobe.com/go/xdm-home-en)
* [Nozioni di base sulla composizione dello schema](http://www.adobe.com/go/xdm-schema-best-practices-en)

## Esempio di schema {#schema}

>[!NOTE]
>
>L&#39;esempio seguente illustra la struttura dei dati inviati [!DNL Platform] tramite il [!DNL Privacy Consent] mixin, in modo da contestualizzare la sezione successiva di questo documento che illustra i principali campi forniti dal mixin. Un esempio completo della struttura dello schema si trova nell&#39; [appendice](#full-schema) a scopo di riferimento.

Il seguente JSON mostra un esempio del tipo di dati che il [!DNL Privacy Consent] mixin è in grado di elaborare. Le informazioni sull&#39;uso specifico di ciascuno di questi campi sono fornite nella sezione successiva.

```json
{
  "xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ],
  "xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  },
  "xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  },
  "xdm:version": "1.0.0",
  "xdm:timestamp": "2019-01-01T15:52:25+00:00",
  "xdm:userLocale": "UK",
  "xdm:localeSource": "ip"
}
```

## Campi {#fields}

Le sezioni seguenti descrivono l’uso di ciascuno dei principali campi forniti dal [!DNL Privacy Consent] mixin e la struttura dei relativi sottocampi.

### xdm:privacyOptOuts {#privacyOptOuts}

`xdm:privacyOptOuts` è un array che rappresenta le impostazioni generali di rifiuto selezionate dal cliente. Diversi oggetti possono essere inclusi in questa matrice, ciascuno dei quali rappresenta un tipo specifico di rinuncia e le preferenze selezionate dal cliente per quel tipo.

```json
"xdm:privacyOptOuts": [
     {
        "xdm:optOutType": "general_opt_out",
        "xdm:optOutValue": "in",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "legitimate_interest"
     },
     {
        "xdm:optOutType": "device_linking",
        "xdm:optOutValue": "not_provided",
        "xdm:basisOfProcessing": "vital_interest"
     },
     {
        "xdm:optOutType": "anonymous_analysis",
        "xdm:optOutValue": "out"
     }
  ]
```

| Proprietà | Descrizione |
| --- | --- |
| `xdm:optOutType` | Tipo di rifiuto. Cfr. l&#39; [appendice](#optOutType-values) per i valori e le definizioni accettati. |
| `xdm:optOutValue` | La preferenza selezionata dal cliente per questo particolare tipo di rinuncia. Cfr. l&#39; [appendice](#choice-optOutValue-values) per i valori e le definizioni accettati. |
| `xdm:timestamp` | Una marca temporale ISO 8601 che indica quando la preferenza di rifiuto è cambiata, se applicabile. |
| `xdm:basisOfProcessing` | Indica la base relativa alla privacy tramite la quale i dati devono essere raccolti ed elaborati. Per impostazione predefinita, questo campo è impostato su `consent`, il che indica che i dati devono essere elaborati solo se l&#39;utente ha fornito il consenso (come mostrato in `xdm:optOutValue`).<br><br>In alcune circostanze, ai clienti non viene richiesto di fornire il consenso per l&#39;elaborazione dei dati. `xdm:basisOfProcessing` deve essere incluso nell&#39;oggetto di rinuncia in questi casi, indicando il motivo per cui non è stata fornita una richiesta di consenso. Cfr. l&#39; [appendice](#basisOfProcessing-values) per i valori e le definizioni accettati. |

### xdm:personalizationPreferences {#personalizationPreferences}

`xdm:personalizationPreferences` acquisisce le preferenze dei clienti in merito alle modalità in cui i loro dati possono essere utilizzati per la personalizzazione. Gli utenti possono scegliere di non partecipare a specifici casi di utilizzo della personalizzazione o di rinunciare completamente alla personalizzazione.

>[!IMPORTANT]
>
>`xdm:personalizationPreferences` non copre i casi di utilizzo marketing. Ad esempio, se un cliente rinuncia alla personalizzazione per le e-mail, non smetterà di ricevere le e-mail. Piuttosto, le e-mail che ricevono saranno generiche e non basate sul loro profilo.
>
>Nello stesso esempio, se un cliente rinuncia al marketing tramite e-mail ( `xdm:marketingPreferences`come spiegato nella sezione [](#marketingPreferences)successiva), non riceverà alcuna e-mail, anche se è consentita la personalizzazione tramite e-mail.

```json
"xdm:personalizationPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown",
        "xdm:timestamp": "2019-01-01T15:52:25+00:00",
        "xdm:basisOfProcessing": "consent"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in"
        },
        {
           "xdm:type": "push_notifications",
           "xdm:choice": "out",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00"
        }
     ]
  }
```

| Proprietà | Descrizione |
| --- | --- |
| `xdm:default` | I dati forniti in questo oggetto rappresentano le preferenze del cliente per la personalizzazione nel suo insieme. |
| `xdm:details` | Un array di oggetti, uno per ciascun tipo di personalizzazione specifico per il quale il cliente ha fornito le preferenze. |
| `xdm:choice` | La preferenza di consenso fornita dal cliente per la personalizzazione in generale, o un tipo di personalizzazione specifico, a seconda che sia fornita in `xdm:default` o `xdm:details`, rispettivamente. Cfr. l&#39; [appendice](#choice-optOutValue-values) per i valori e le definizioni accettati. |
| `xdm:type` | Gli oggetti nell&#39; `xdm:details` array devono fornire questo campo per indicare il caso di utilizzo della personalizzazione specifico per il quale il cliente fornisce i dati di consenso. Cfr. l&#39; [appendice](#type-values) per i valori e le definizioni accettati. |
| `xdm:timestamp` | Una marca temporale ISO 8601 che indica quando la preferenza di rifiuto è cambiata, se applicabile. |
| `xdm:basisOfProcessing` | Indica la base relativa alla privacy tramite la quale i dati devono essere raccolti ed elaborati. Per impostazione predefinita, questo campo è impostato su `consent`, il che indica che i dati devono essere elaborati solo se l&#39;utente ha fornito il consenso (come mostrato in `xdm:choice`).<br><br>In alcune circostanze, ai clienti non viene richiesto di fornire il consenso per la personalizzazione. `xdm:basisOfProcessing` deve essere incluso nell&#39;oggetto di rinuncia in questi casi, indicando il motivo per cui non è stata fornita una richiesta di consenso. Cfr. l&#39; [appendice](#basisOfProcessing-values) per i valori e le definizioni accettati. |


### xdm:marketingPreferences {#marketingPreferences}

`xdm:marketingPreferences` acquisisce le preferenze dei clienti in merito alle finalità di marketing per le quali i loro dati possono essere utilizzati. Gli utenti possono scegliere di non partecipare a specifici casi di utilizzo del marketing o di non partecipare al marketing diretto.

```json
"xdm:marketingPreferences": {
     "xdm:default": {
        "xdm:choice": "unknown"
     },
     "xdm:details": [
        {
           "xdm:type": "email",
           "xdm:choice": "in",
           "xdm:subscriptions": {
              "weekly_mailer": {
                 "xdm:choice": "out",
                 "xdm:timestamp": "2019-02-03T15:52:25+00:00"
              },
              "daily_newsletter": {
                 "xdm:choice": "pending"
              }
           }
        },
        {
           "xdm:type": "iot",
           "xdm:choice": "out",
           "xdm:timestamp": "2019-01-01T15:52:25+00:00",
           "xdm:basisOfProcessing": "legitimate_interest",
           "xdm:subscriptions": {
              "out_of_milk": {
                 "xdm:choice": "in"
              }
           }
        }
     ]
  }
```

| Proprietà | Descrizione |
| --- | --- |
| `xdm:default` | I dati forniti in questo oggetto rappresentano le preferenze del cliente per l&#39;intero marketing diretto. |
| `xdm:details` | Un array di oggetti, uno per ogni caso di utilizzo marketing specifico per cui il cliente ha fornito le preferenze. |
| `xdm:choice` | La preferenza di consenso fornita dal cliente per la commercializzazione in generale, o un caso di utilizzo marketing specifico, a seconda che sia fornita rispettivamente in `xdm:default` o `xdm:details`. Cfr. l&#39; [appendice](#choice-optOutValue-values) per i valori e le definizioni accettati. |
| `xdm:subscriptions` | Un oggetto le cui chiavi rappresentano sottoscrizioni specifiche per la società, come mailing list o newsletter. Ciascun oggetto di iscrizione deve a sua volta contenere un `xdm:choice` valore per la sottoscrizione in questione. |
| `xdm:type` | Gli oggetti nell&#39; `xdm:details` array devono fornire questo campo per indicare il caso di utilizzo marketing specifico per il quale il cliente fornisce i dati di consenso. Cfr. l&#39; [appendice](#type-values) per i valori e le definizioni accettati. |
| `xdm:timestamp` | Una marca temporale ISO 8601 che indica quando la preferenza di rifiuto è cambiata, se applicabile. |
| `xdm:basisOfProcessing` | Indica la base relativa alla privacy tramite la quale i dati devono essere raccolti ed elaborati. Per impostazione predefinita, questo campo è impostato su `consent`, il che indica che i dati devono essere elaborati solo se l&#39;utente ha fornito il consenso (come mostrato in `xdm:choice`).<br><br>In alcune circostanze, ai clienti non viene richiesto di fornire il consenso per il marketing diretto. `xdm:basisOfProcessing` deve essere incluso nell&#39;oggetto di rinuncia in questi casi, indicando il motivo per cui non è stata fornita una richiesta di consenso. Cfr. l&#39; [appendice](#basisOfProcessing-values) per i valori e le definizioni accettati. |

## Inserimento di dati di consenso tramite il mixin {#ingest}

Per utilizzare il [!DNL Privacy Consent] mixin per acquisire i dati di consenso dai clienti, è necessario aggiungere il mixin a uno schema nuovo o esistente e creare un dataset basato su tale schema.

Per informazioni sull&#39;aggiunta di mixin a uno schema, vedere l&#39;esercitazione sulla [creazione di uno schema nell&#39;interfaccia utente](http://www.adobe.com/go/xdm-schema-editor-tutorial-en) . Il[!DNL  Privacy Consent] mixin è compatibile con schemi basati sulle classi [!DNL XDM Individual Profile] o [!DNL XDM ExperienceEvent].

Dopo aver creato uno schema contenente il [!DNL Privacy Consent] mixin, fare riferimento alla sezione sulla [creazione di un dataset](../../catalog/datasets/user-guide.md#create) nella guida utente del dataset, seguendo la procedura per creare un dataset con uno schema esistente.

>[!IMPORTANT]
>
>Se si desidera inviare i dati di consenso a [!DNL Real-time Customer Profile], è necessario creare uno schema [!DNL Profile]abilitato basato sulla [!DNL XDM Individual Profile] classe che contiene il [!DNL Privacy Consent] mixin. Anche il set di dati creato in base a tale schema deve essere abilitato per [!DNL Profile]. Per i passaggi specifici relativi ai [!DNL Real-time Customer Profile] requisiti, fare riferimento alle esercitazioni di cui sopra.

## Appendice {#appendix}

Le sezioni seguenti forniscono ulteriori informazioni di riferimento relative alla [!DNL Privacy Consent] miscelazione.

### Valori accettati per xdm:optOutType {#optOutType-values}

Nella tabella seguente sono riportati i valori accettati per `xdm:optOutType`:

| Valore | Descrizione |
| --- | --- |
| `general_opt_out` | I dati non possono essere utilizzati per alcun scopo. In genere questo blocca la raccolta dei dati, tranne quando la base di elaborazione non è &quot;consenso&quot;.<br><br>Quando si utilizza questo tipo di rifiuto, i valori accettati `in` e `out` ottenere il seguente significato contestuale:<ul><li>`in`: L&#39;utente **ha acconsentito** all&#39;utilizzo dei propri dati per l&#39;elaborazione generale.</li><li>`out`: L&#39;utente **non accetta** che i propri dati vengano utilizzati per l&#39;elaborazione generale.</li></ul>Per ulteriori informazioni, vedere la tabella sui valori [accettati per xdm:optOutValue](#choice-optOutValue-values) . |
| `anonymous_analysis` | I dati non possono essere utilizzati per metriche Web generiche che non richiedono alcun tipo di ID utente, ad esempio il numero di volte in cui una particolare pagina è stata visualizzata. |
| `device_linking` | I dati di un dispositivo utilizzato da un visitatore non possono essere combinati con i dati di un altro dispositivo utilizzato dallo stesso visitatore. I dispositivi sono collegati utilizzando tecniche quali un nome utente o un indirizzo e-mail comuni, spesso tramite la cooperativa di dispositivi  Adobe o un grafico di dispositivi privati. |
| `pseudonymous_analysis` | I dati non possono essere utilizzati per le metriche Web fornite da  Adobe Analytics, che richiedono ID pseudonimi per identificare i percorsi seguiti dagli utenti attraverso un sito Web (ad esempio un rapporto di abbandono), per stabilire le sessioni e a scopo di attribuzione. |
| `sales_sharing_opt_out` | I dati non possono essere utilizzati a fini di vendita o per la condivisione con terzi.<br><br>Quando si utilizza questo tipo di rifiuto, i valori accettati `in` e `out` ottenere il seguente significato contestuale:<ul><li>`in`: L&#39;utente **ha fornito il consenso** affinché i propri dati vengano utilizzati a fini di vendita e condivisione.</li><li>`out`: L&#39;utente **non accetta** che i propri dati vengano utilizzati a fini di vendita e condivisione.</li></ul>Per ulteriori informazioni, vedere la tabella sui valori [accettati per xdm:optOutValue](#choice-optOutValue-values) . |

### Valori accettati per xdm:baseOfProcessing {#basisOfProcessing-values}

Nella tabella seguente sono riportati i valori accettati per `xdm:basisOfProcessing`:

| Valore | Descrizione |
| --- | --- |
| `consent` **(Predefinito)** | La raccolta di dati per lo scopo specificato è consentita, dato che l&#39;individuo ha fornito l&#39;autorizzazione esplicita. Questo è il valore predefinito di `xdm:basisOfProcessing` se non viene fornito nessun altro valore. <br><br>**IMPORTANTE **: I valori per`xdm:choice`e`xdm:optOutValue`vengono rispettati solo se`xdm:basisOfProcessing`è impostato su`consent`. Se vengono utilizzati per`xdm:basisOfProcessing`sostituire gli altri valori indicati in questa tabella, le scelte di consenso dell&#39;utente vengono ignorate. |
| `compliance` | La raccolta di dati per lo scopo specificato è necessaria per soddisfare gli obblighi legali dell&#39;impresa. |
| `contract` | La raccolta di dati per lo scopo specificato è necessaria per adempiere agli obblighi contrattuali con l&#39;individuo. |
| `legitimate_interest` | Il legittimo interesse commerciale a raccogliere ed elaborare tali dati per lo scopo specificato supera il potenziale danno che comporta per l&#39;individuo. |
| `public_interest` | La raccolta di dati per lo scopo specificato è necessaria per svolgere un compito di interesse pubblico o nell&#39;esercizio di un&#39;autorità ufficiale. |
| `vital_interest` | La raccolta di dati per lo scopo specificato è necessaria per proteggere gli interessi vitali dell&#39;individuo. |

### Valori accettati per xdm:choice e xdm:optOutValue {#choice-optOutValue-values}

La tabella seguente delinea i valori accettati per `xdm:choice` e `xdm:optOutValue`:

| Valore | Descrizione |
| --- | --- |
| `pending` | Il sistema non ha ancora ricevuto informazioni di consenso-preferenza dal cliente. Può essere utilizzato per la prima pagina di un sito Web mentre viene ottenuto il consenso. Può anche essere utilizzato per indicare che il consenso è &quot;presunto&quot;, piuttosto che esplicitamente fornito. |
| `in` | L&#39;utente ha scelto la preferenza di consenso. In altre parole, essi **acconsentono** all&#39;uso dei loro dati come indicato dalla preferenza di consenso in questione. |
| `out` | L&#39;utente ha rinunciato alla preferenza di consenso. In altre parole, essi **non** acconsentono all&#39;uso dei loro dati come indicato dalla preferenza di consenso in questione. |
| `not_applicable` | La preferenza di consenso in questione non si applica al cliente. |
| `not_provided` | Il cliente non ha fornito informazioni sulla preferenza relativa al consenso. |
| `unknown` | Le informazioni sulle preferenze del cliente relative al consenso sono sconosciute. |

### Valori accettati per xdm:type {#type-values}

Nella tabella seguente sono riportati i valori accettati per `xdm:type`:

| Valore | Descrizione |
| --- | --- |
| `ads` | Annunci che possono essere visualizzati da siti Web non correlati. |
| `content` | Contenuto visualizzato sul sito Web. |
| `customer_support` | Dati relativi all’assistenza clienti. |
| `email` | Messaggi e-mail. |
| `iot` | Dati relativi all&#39;&quot;Internet delle cose&quot; (IoT). |
| `in_app_messages` | Messaggi in-app. |
| `in_home` | Messaggi interni. |
| `in_store` | Messaggi in-store. |
| `in_vehicle` | Messaggi di bordo. |
| `offers` | Offerte speciali. |
| `phone_calls` | Dati relativi alle interazioni telefoniche. |
| `push_notifications` | Notifiche push. |
| `sms` | Messaggi SMS. |
| `social_media` | Contenuto social media. |
| `snail_mail` | Messaggi inviati tramite la distribuzione postale convenzionale. |
| `third_party_content` | Contenuto o articoli visualizzati sul sito Web forniti da un&#39;entità non correlata. |
| `third_party_offers` | Offerte o annunci visualizzati sul tuo sito Web servizi pubblicitari da un&#39;entità non correlata. |

### Schema completo [!DNL Privacy Consent] {#full-schema}

Il seguente JSON rappresenta lo [!DNL Privacy Consent] schema completo così come viene visualizzato nel Registro di sistema dello schema:

```json
{
  "meta:license": [
    "Copyright 2019 Adobe Systems Incorporated. All rights reserved.",
    "This work is licensed under a Creative Commons Attribution 4.0 International (CC BY 4.0) license",
    "you may not use this file except in compliance with the License. You may obtain a copy",
    "of the License at https://creativecommons.org/licenses/by/4.0/"
  ],
  "$id": "https://ns.adobe.com/xdm/context/consent-preferences",
  "$schema": "http://json-schema.org/draft-06/schema#",
  "title": "Privacy/Marketing Preferences (Consent)",
  "description": "This schema captures privacy, personalization and marketing preferences (consents).",
  "type": "object",
  "meta:extensible": true,
  "meta:abstract": true,
  "definitions": {
    "consentValue": {
      "type": "string",
      "enum": [
        "not_provided",
        "pending",
        "in",
        "out",
        "unknown",
        "not_applicable"
      ],
      "meta:enum": {
        "not_provided": "Not provided",
        "pending": "Pending verification",
        "in": "Opt-in",
        "out": "Opt-out",
        "unknown": "Unknown",
        "not_applicable": "Not Applicable"
      }
    },
    "basisOfProcessing": {
      "title": "Basis Of Processing",
      "type": "string",
      "description": "Basis of Processing",
      "enum": [
        "consent",
        "legitimate_interest",
        "contract",
        "vital_interest",
        "compliance",
        "public_interest"
      ],
      "meta:enum": {
        "consent": "User Consent",
        "legitimate_interest": "Legitimate Interest",
        "contract": "Contract",
        "vital_interest": "Vital Interest of the Individual",
        "compliance": "Compliance with a Legal Obligation",
        "public_interest": "Public Interest"
      }
    },
    "timestamp": {
      "title": "Preference timestamp",
      "description": "Timestamp of this specific opt out or preference.",
      "type": "string",
      "format": "date-time"
    },
    "consent-preferences": {
      "properties": {
        "xdm:privacyOptOuts": {
          "title": "Privacy Preferences",
          "description": "Encapsulates data privacy preferences.",
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "xdm:optOutType": {
                "title": "Opt-out type",
                "type": "string",
                "description": "The type of user permission.",
                "enum": [
                  "general_opt_out",
                  "sales_sharing_opt_out",
                  "anonymous_analysis",
                  "pseudonymous_analysis",
                  "device_linking"
                ],
                "meta:enum": {
                  "general_opt_out": "General opt-out",
                  "sales_sharing_opt_out": "Sales/sharing opt-out",
                  "anonymous_analysis": "Anonymous Analysis",
                  "pseudonymous_analysis": "Pseudonymous Analysis",
                  "device_linking": "Device Linking"
                }
              },
              "xdm:optOutValue": {
                "title": "Opt Out Value",
                "description": "The value of the specific opt out.",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          }
        },
        "xdm:personalizationPreferences": {
          "title": "Personalization Preferences",
          "description": "User's Personalization Preferences",
          "type": "object",
          "properties": {
            "xdm:default": {
              "title": "Global Personalization Preferences",
              "description": "User's Default Personalization Preference",
              "type": "object",
              "properties": {
                "xdm:choice": {
                  "title": "Default Personalization Preferences Value",
                  "description": "The default value for personalization",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            },
            "xdm:details": {
              "title": "Itemized Personalization Preferences",
              "description": "Preferences for specific types of personalization",
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "meta:enum": {
                    "content": "Personalize Content",
                    "in_app": "Personalize In App Messages",
                    "offers": "Personalize Offers",
                    "email": "Personalize eMail",
                    "snail_mail": "Personalize Regular Mail",
                    "phone_calls": "Personalize Phone Calls",
                    "push_notifications": "Personalize Push Notifications",
                    "sms": "Personalize SMS",
                    "customer_support": "Personalize Customer Support",
                    "in_store": "Personalize In Store",
                    "in_vehicle": "Personalize In Vehicle",
                    "in_home": "Personalize In Home",
                    "iot": "Personalize IoT",
                    "social_media": "Personalize Social Media",
                    "third_party_offers": "Personalize Third-party Offers",
                    "third_party_content": "Personalize Third-party Content",
                    "ads": "Personalize My Business's Ads on Other Sites"
                  }
                },
                "xdm:choice": {
                  "title": "Personalization Preference Value",
                  "description": "The value for this specific personalization preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                }
              }
            }
          }
        }
      },
      "xdm:marketingPreferences": {
        "title": "Marketing Preferences",
        "description": "User's Direct Marketing Preferences",
        "type": "object",
        "properties": {
          "xdm:default": {
            "title": "Default Direct Marketing Preference",
            "description": "User's Default Marketing Preference",
            "type": "object",
            "properties": {
              "xdm:choice": {
                "title": "Default Marketing Preferences Value",
                "description": "The default value for direct marketing preferences",
                "$ref": "#/definitions/consentValue"
              },
              "xdm:basisOfProcessing": {
                "$ref": "#/definitions/basisOfProcessing"
              },
              "xdm:timestamp": {
                "$ref": "#/definitions/timestamp"
              }
            }
          },
          "xdm:details": {
            "title": "Itemized Direct Marketing Preferences",
            "description": "Preferences for specific types of direct marketing",
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "xdm:type": {
                  "title": "Marketing Preference",
                  "type": "string",
                  "description": "The specific marketing preference.",
                  "enum": [
                    "email",
                    "push_notifications",
                    "in_app_messages",
                    "sms",
                    "phone_calls",
                    "snail_mail",
                    "in_vehicle_messages",
                    "in_home_messages",
                    "iot",
                    "social_media"
                  ],
                  "meta:enum": {
                    "email": "Receive eMail",
                    "push_notifications": "Receive Push Notifications",
                    "in_app_messages": "Receive In App Messages",
                    "sms": "Receive SMS",
                    "phone_calls": "Receive Phone Calls",
                    "snail_mail": "Receive Regular Mail",
                    "in_vehicle_messages": "Receive In Vehicle Messages",
                    "in_home_messages": "Receive In Home Messages",
                    "iot": "Receive IoT",
                    "social_media": "Receive Social Media Messages"
                  }
                },
                "xdm:choice": {
                  "title": "Marketing Preference Value",
                  "description": "The value for this specific marketing preference",
                  "$ref": "#/definitions/consentValue"
                },
                "xdm:basisOfProcessing": {
                  "$ref": "#/definitions/basisOfProcessing"
                },
                "xdm:timestamp": {
                  "$ref": "#/definitions/timestamp"
                },
                "xdm:subscriptions": {
                  "title": "Company-specific subscriptions",
                  "description": "Company-specific subscriptions, such as mailing lists or newsletters",
                  "type": "object",
                  "meta:xdmType": "map",
                  "additionalProperties": {
                    "xdm:choice": {
                      "title": "Marketing Preference Value",
                      "description": "The value for this specific marketing preference",
                      "$ref": "#/definitions/consentValue"
                    },
                    "xdm:timestamp": {
                      "$ref": "#/definitions/timestamp"
                    }
                  }
                }
              }
            }
          }
        }
      },
      "xdm:timestamp": {
        "title": "Consent Preferences timestamp",
        "description": "Timestamp of the complete set of user consent preferences.",
        "type": "string",
        "format": "date-time"
      },
      "xdm:version": {
        "title": "Preferences Version",
        "description": "Version of the Privacy Preferences Standard",
        "type": "string"
      },
      "xdm:userLocale": {
        "title": "User Locale",
        "description": "User location or jurisdiction that applies to the consents for this user",
        "type": "string"
      },
      "xdm:localeSource": {
        "title": "Locale Source",
        "description": "Method used to determine the user's locale",
        "enum": [
          "ip",
          "gps",
          "user_provided",
          "website_location",
          "inferred",
          "other"
        ],
        "meta:enum": {
          "ip": "IP Address",
          "gps": "Device GPS",
          "user_provided": "User Provided",
          "website_location": "Website eTDL",
          "inferred": "Inferred",
          "other": "Other"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context"
    },
    {
      "$ref": "#/definitions/consent-preferences"
    }
  ],
  "meta:status": "experimental"
}
```
