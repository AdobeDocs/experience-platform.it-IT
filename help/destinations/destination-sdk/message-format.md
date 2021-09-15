---
description: Utilizza il contenuto di questa pagina insieme alle altre opzioni di configurazione per le destinazioni dei partner. Questa pagina tratta il formato di messaggistica dei dati esportati da Adobe Experience Platform alle destinazioni, mentre l’altra pagina tratta specifiche sulla connessione e l’autenticazione alla destinazione.
seo-description: Use the content on this page together with the rest of the configuration options for partner destinations. This page addresses the messaging format of data exported from Adobe Experience Platform to destinations, while the other page addresses specifics about connecting and authenticating to your destination.
seo-title: Message format
title: Formato del messaggio
exl-id: 1212c1d0-0ada-4ab8-be64-1c62a1158483
source-git-commit: 91228b5f2008e55b681053296e8b3ff4448c92db
workflow-type: tm+mt
source-wordcount: '1972'
ht-degree: 2%

---

# Formato del messaggio

## Prerequisiti - Concetti di Adobe Experience Platform {#prerequisites}

Per comprendere il processo dal lato Adobe, ti preghiamo di acquisire familiarità con i seguenti concetti di Experience Platform:

* **Experience Data Model (XDM)**. [Panoramica ](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it) di XDM e   [come creare uno schema XDM in Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en).
* **Classe**. [Creare e modificare le classi nell’interfaccia utente](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/classes.html?lang=en).
* **Gruppo di campi**. [Definizione del gruppo di campi ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#field-group) e  [ulteriori informazioni sui gruppi](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#field-group) di campi.
* **IdentityMap**. La mappa identità rappresenta una mappa di tutte le identità dell’utente finale in Adobe Experience Platform. Fai riferimento a `xdm:identityMap` nel [dizionario dei campi XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).
* **SegmentMembership**. L&#39;attributo [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) XDM indica di quali segmenti fa parte un profilo. Per i tre valori diversi nel campo `status`, leggere la documentazione sul gruppo di campi [Dettagli appartenenza al segmento](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

## Panoramica {#overview}

Utilizza il contenuto di questa pagina insieme alle altre opzioni di configurazione [per le destinazioni partner](./configuration-options.md). Questa pagina tratta il formato di messaggistica dei dati esportati da Adobe Experience Platform alle destinazioni, mentre l’altra pagina tratta specifiche sulla connessione e l’autenticazione alla destinazione.

Adobe Experience Platform esporta i dati in un numero significativo di destinazioni, in vari formati di dati. Alcuni esempi di tipi di destinazione sono piattaforme pubblicitarie (Google), social network (Facebook), posizioni di archiviazione cloud (Amazon S3, Azure Event Hubs).

Ad Experience Platform, puoi regolare il formato del messaggio esportato in modo che corrisponda al formato previsto sul tuo lato. Per comprendere questa personalizzazione, sono importanti i seguenti concetti:
* Lo schema XDM di origine (1) e di destinazione (2) in Adobe Experience Platform
* il formato del messaggio sul lato partner (3) e
* Il livello di trasformazione tra i due, che puoi definire creando un [modello di trasformazione del messaggio](./message-format.md#using-templating).

![Schema di trasformazione JSON](./assets/transformations-3-steps.png)

Experience Platform utilizza gli schemi per descrivere la struttura dei dati in modo coerente e riutilizzabile.

Gli utenti che desiderano attivare i dati nella destinazione devono mappare i campi utilizzati per i set di dati in Experience Platform su uno schema che si traduca nel formato previsto della destinazione. Ad Adobe, verrà creato un gruppo di campi personalizzato da aggiungere allo schema di destinazione per la tua azienda. I campi nel gruppo di campi dipendono dai campi dell’attributo del profilo che puoi ricevere.

**Schema XDM di origine (1)**: Questo si riferisce allo schema utilizzato da un cliente in Experience Platform. Ad Experience Platform, nel [passaggio di mappatura](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#mapping) del flusso di lavoro di attivazione della destinazione, i clienti mappano i campi dallo schema di origine allo schema di destinazione della tua destinazione (2).

**Schema XDM di Target (2)**: In base allo schema standard JSON (3) condiviso con Adobe, il team di Adobe creerà uno schema personalizzato per la destinazione. Tieni presente che in una [fase futura del progetto](./overview.md#phased-approach) potrai creare da solo lo schema personalizzato per la destinazione.

**Schema JSON standard degli attributi del profilo di destinazione (3)**: Condividi con noi uno  [schema ](https://json-schema.org/learn/miscellaneous-examples.html) JSON di tutti gli attributi di profilo supportati dalla tua piattaforma e i relativi tipi (ad esempio: oggetto, stringa, array). I campi di esempio supportati dalla destinazione possono essere `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName` e così via.

In base alle trasformazioni dello schema descritte qui sopra, la struttura di un messaggio cambia tra lo schema XDM di origine e lo schema di esempio sul lato partner:

![Esempio di messaggio di trasformazione](./assets/transformations-with-examples.png)

<br> 


## Guida introduttiva - trasformazione di tre attributi di base {#getting-started}

Per illustrare il processo di trasformazione, l’esempio seguente utilizza tre attributi di profilo comuni in Adobe Experience Platform: **nome**, **cognome** e **indirizzo e-mail**.

>[!NOTE]
>
>Il cliente mappa gli attributi dallo schema XDM di origine allo schema XDM partner nell&#39;interfaccia utente Adobe Experience Platform, nel passaggio **Mapping** del [attiva flusso di lavoro di destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate-destinations.html#mapping).

Supponiamo che la piattaforma possa ricevere un formato di messaggio come:

```curl
POST https://YOUR_REST_API_URL/users/
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY

{
  "attributes":
    {
      "first_name": "Yours",
      "last_name": "Truly",
      "external_id": "yourstruly@adobe.com"
    }
}
```

Considerando il formato del messaggio, le trasformazioni corrispondenti sono le seguenti:

| Attributo nello schema XDM del partner sul lato Adobe | Transformation (Trasformazione) | Attributo nel messaggio HTTP sul lato |
|---------|----------|---------|
| `_your_custom_schema.firstName` | ` attributes.first_name` | `first_name` |
| `_your_custom_schema.lastName` | `attributes.last_name` | `last_name` |
| `personalEmail.address` | `attributes.external_id` | `external_id` |

## Utilizzo di un linguaggio di template per le trasformazioni di identità, attributi e appartenenza ai segmenti {#using-templating}

Adobe utilizza un linguaggio di template simile a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) per trasformare i campi dallo schema XDM in un formato supportato dalla destinazione.

Questa sezione fornisce diversi esempi di come vengono effettuate queste trasformazioni, dallo schema XDM di input, attraverso il modello e l’output nei formati di payload accettati dalla destinazione. Gli esempi seguenti sono ordinati in base alla complessità crescente, come segue:

1. Semplici esempi di trasformazione. Scopri come la modellazione funziona con semplici trasformazioni per i campi [Attributi del profilo](./message-format.md#attributes), [Iscrizione al segmento](./message-format.md#segment-membership) e [Identità](./message-format.md#identities).
2. Esempi di modelli più complessi che combinano i campi di cui sopra: [Crea un modello che invia segmenti e identità](./message-format.md#segments-and-identities) e [Crea un modello che invia segmenti, identità e attributi di profilo](./message-format.md#segments-identities-attributes).
3. I modelli includono la chiave di aggregazione. Quando utilizzi [un&#39;aggregazione configurabile](./destination-configuration.md#configurable-aggregation) nella configurazione di destinazione, Experience Platform raggruppa i profili esportati nella destinazione in base a criteri quali l&#39;ID segmento, lo stato del segmento o i namespace di identità.

### Attributi del profilo {#attributes}

Per trasformare gli attributi di profilo esportati nella destinazione, consulta il JSON e gli esempi di codice riportati di seguito.

>[!IMPORTANT]
>
>Per un elenco di tutti gli attributi di profilo disponibili in Adobe Experience Platform, consulta il [dizionario di campo XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).


**Ingresso**

Profilo 1:

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
    },
    "birthDate": {}
  }
}
```

Profilo 2:

```json
{
  "attributes": {
    "firstName": {
      "value": "Harry"
    },
    "birthDate": {
        "value": "1980/07/31"
    }
  }
}
```

**Modello**

>[!IMPORTANT]
>
>Per tutti i modelli utilizzati, è necessario evitare i caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello nella [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedi il capitolo 9 in [JSON standard](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            {% for attribute in profile.attributes %}
            "{{ attribute.key }}":
                {% if attribute.value is empty %}
                    null
                {% else %}
                    "{{ attribute.value.value }}"
                {% endif %}
            {% if not loop.last %},{% endif %}
            {% endfor %}
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Risultato**


```json
{
    "profiles": [
        {
            "firstName": "Hermione",
            "birthDate": null
        },
        {
            "firstName": "Harry",
            "birthDate": "1980/07/31"
        }
    ]
}
```

### Iscrizione al segmento {#segment-membership}

L&#39;attributo [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) XDM indica di quali segmenti fa parte un profilo.
Per i tre valori diversi nel campo `status`, leggere la documentazione sul gruppo di campi [Dettagli appartenenza al segmento](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

**Ingresso**

Profilo 1:

```json
{
  "segmentMembership": {
    "ups": {
      "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "existing"
      },
      "8f812592-3f06-416b-bd50-e7831848a31a": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      }
    }
  }
}
```

Profilo 2:

```json
{
  "segmentMembership": {
    "ups": {
      "32396e4b-16f6-4033-9702-fc69b5e24e7c": {
        "lastQualificationTime": "2021-08-20T17:23:04Z",
        "status": "realized"
      },
      "af854278-894a-4192-a96b-320fbf2623fd": {
        "lastQualificationTime": "2021-08-20T16:44:37Z",
        "status": "existing"
      },
      "66505bf9-bc08-4bac-afbc-8b6706650ea4": {
        "lastQualificationTime": "2019-08-20T17:23:04Z",
        "status": "realized"
      }
    }
  }
}
```

**Modello**


>[!IMPORTANT]
>
>Per tutti i modelli utilizzati, è necessario evitare i caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello nella [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedi il capitolo 9 in [JSON standard](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering segments by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Risultato**

```json
{
    "profiles": [
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "32396e4b-16f6-4033-9702-fc69b5e24e7c",
                    "af854278-894a-4192-a96b-320fbf2623fd",
                    "66505bf9-bc08-4bac-afbc-8b6706650ea4"
                ],
                "remove": [
                ]
            }
        }
    ]
}
```

### Identità {#identities}

Per informazioni sulle identità in Experience Platform, consulta la [Panoramica spazio dei nomi identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=it).

**Ingresso**

Profilo 1:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    }
}
```

Profilo 2:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    }
}
```

**Modello**


>[!IMPORTANT]
>
>Per tutti i modelli utilizzati, è necessario evitare i caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello nella [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedi il capitolo 9 in [JSON standard](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ]
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Risultato**

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ]
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ]
        }
    ]
}
```


### Creare un modello che invia segmenti e identità {#segments-and-identities}

Questa sezione fornisce un esempio di trasformazione comunemente utilizzata tra lo schema XDM di Adobe e lo schema di destinazione del partner.
L’esempio seguente mostra come trasformare l’appartenenza al segmento e il formato delle identità e inviarli alla destinazione.

**Ingresso**

Profilo 1:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "existing"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

Profilo 2:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2021-08-31T10:01:42Z",
                "status": "realized"
            }
        }
    }
}
```

**Modello**

>[!IMPORTANT]
>
>Per tutti i modelli utilizzati, è necessario evitare i caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello nella [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedi il capitolo 9 in [JSON standard](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
                
                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}
                
                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ],
                "remove": [
                    {# Alternative syntax for filtering segments by status: #}
                    {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Risultato**

Il `json` seguente rappresenta i dati esportati da Adobe Experience Platform.

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### Creare un modello che invia segmenti, identità e attributi di profilo {#segments-identities-attributes}

Questa sezione fornisce un esempio di trasformazione comunemente utilizzata tra lo schema XDM di Adobe e lo schema di destinazione del partner.

Un altro caso d’uso comune è l’esportazione di dati contenenti l’appartenenza a un segmento, le identità (ad esempio: indirizzo e-mail, numero di telefono, ID pubblicitario) e attributi del profilo. Per esportare i dati in questo modo, vedi l’esempio seguente:

**Ingresso**

Profilo 1:

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
        },
        "birthDate": {}
    },
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "existing"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

Profilo 2:

```json
{
    "attributes": {
        "firstName": {
            "value": "Harry"
        },
        "birthDate": {
            "value": "1980/07/31"
        }
    },
    "identityMap": {
        "email": [
            {
                "id": "harry.p@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            }
        }
    }
}
```

**Modello**

>[!IMPORTANT]
>
>Per tutti i modelli utilizzati, è necessario evitare i caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello nella [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedi il capitolo 9 in [JSON standard](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "attributes": {
            {% for attribute in profile.attributes %}
                "{{ attribute.key }}":
                    {% if attribute.value is empty %}
                        null
                    {% else %}
                        "{{ attribute.value.value }}"
                    {% endif %}
                {% if not loop.last %},{% endif %}
            {% endfor %}
            },
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if we have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering segments by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }
    ]
}
```

**Risultato**

Il `json` seguente rappresenta i dati esportati da Adobe Experience Platform.

```json
{
    "profiles": [
        {
            "attributes": {
                "firstName": "Hermione",
                "birthDate": null
            },
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "attributes": {
                "firstName": "Harry",
                "birthDate": "1980/07/21"
            },
            "identities": [
                {
                    "type": "email",
                    "id": "harry.p@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### Includi chiave di aggregazione nel modello per raggruppare i profili esportati in base a vari criteri {#template-aggregation-key}

Quando utilizzi [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) nella configurazione di destinazione, puoi modificare il modello di trasformazione del messaggio per raggruppare i profili esportati nella destinazione in base a criteri quali ID segmento, alias segmento, appartenenza al segmento o namespace di identità, come mostrato negli esempi seguenti.

#### Utilizza la chiave di aggregazione ID segmento nel modello {#aggregation-key-segment-id}

Se utilizzi [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) e imposti `includeSegmentId` su true, puoi utilizzare `segmentId` nel modello per raggruppare i profili nei messaggi HTTP esportati nella destinazione:

**Ingresso**

Considera i quattro profili seguenti, in cui i primi due fanno parte del segmento con l’ ID `788d8874-8007-4253-92b7-ee6b6c20c6f3` e gli altri due fanno parte del segmento con l’ ID `8f812592-3f06-416b-bd50-e7831848a31a`.

Profilo 1:

```json
{
   "attributes":{
      "firstName":{
         "value":"Hermione"
      },
      "birthDate":{
         
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"existing"
         }
      }
   }
}
```

Profilo 2:

```json
{
   "attributes":{
      "firstName":{
         "value":"Harry"
      },
      "birthDate":{
         "value":"1980/07/31"
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"existing"
         }
      }
   }
}
```

Profilo 3:

```json
{
   "attributes":{
      "firstName":{
         "value":"Tom"
      },
      "birthDate":{
         
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"existing"
         }
      }
   }
}
```

Profilo 4:

```json
{
   "attributes":{
      "firstName":{
         "value":"Jerry"
      },
      "birthDate":{
         "value":"1940/01/01"
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"existing"
         }
      }
   }
}
```

**Modello**

>[!IMPORTANT]
>
>Per tutti i modelli utilizzati, è necessario evitare i caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello nella [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedi il capitolo 9 in [JSON standard](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            {% for attribute in profile.attributes %}
            "{{ attribute.key }}":
                {% if attribute.value is empty %}
                    null
                {% else %}
                    "{{ attribute.value.value }}"
                {% endif %}
            {% if not loop.last %},{% endif %}
            {% endfor %}
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
    "audienceId": "{{input.aggregationKey.segmentId}}"
}
```

**Risultato**

Quando vengono esportati nella destinazione, i profili vengono suddivisi in due gruppi, in base al relativo ID segmento.

```json
{
    "profiles": [
        {
            "firstName": "Hermione",
            "birthDate": null
        },
        {
            "firstName": "Harry",
            "birthDate": "1980/07/31"
        }
    ],
    "audienceId": "788d8874-8007-4253-92b7-ee6b6c20c6f3"
}
```

```json
{
    "profiles": [
        {
            "firstName": "Tom",
            "birthDate": null
        },
        {
            "firstName": "Jerry",
            "birthDate": "1940/01/01"
        }
    ],
    "audienceId": "8f812592-3f06-416b-bd50-e7831848a31a"
}
```

#### Utilizza la chiave di aggregazione degli alias dei segmenti nel modello {#aggregation-key-segment-alias}

Se utilizzi [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) e imposti `includeSegmentId` su true, puoi utilizzare l’alias del segmento nel modello per raggruppare i profili nei messaggi HTTP esportati nella destinazione.

Aggiungi la riga sottostante al modello per raggruppare i profili esportati in base all’alias del segmento.

```python
"customerList={{input.aggregationKey.segmentAlias}}"
```

#### Utilizza la chiave di aggregazione dello stato del segmento nel modello {#aggregation-key-segment-status}

Se utilizzi [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) e imposti `includeSegmentId` e `includeSegmentStatus` su true, puoi utilizzare lo stato del segmento nel modello per raggruppare i profili nei messaggi HTTP esportati nella destinazione in base al fatto che i profili debbano essere aggiunti o rimossi dai segmenti.

I valori possibili sono:

* realizzato
* esistente
* uscito

Aggiungi la riga sottostante al modello per aggiungere o rimuovere profili dai segmenti, in base ai valori sopra riportati.:

```python
"action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}"
```

#### Utilizza la chiave di aggregazione dello spazio dei nomi identità nel modello {#aggregation-key-identity}

Di seguito è riportato un esempio in cui l’ [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) nella configurazione di destinazione è impostata per aggregare i profili esportati per spazi dei nomi di identità, nel modulo `"identityNamespaces": ["email", "phone"]`

**Ingresso**

Profilo 1:

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e1@example.com"
         },
         {
            "id":"e2@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744111222"
         }
      ]
   }
}
```

Profilo 2:

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e3@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744333444"
         },
         {
            "id":"+40744555666"
         }
      ]
   }
}
```

**Modello**

>[!IMPORTANT]
>
>Per tutti i modelli utilizzati, è necessario evitare i caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello nella [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedi il capitolo 9 in [JSON standard](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

```python
{
            "profiles": [
            {% for profile in input.profiles %}
            {
                {% for ns in input.aggregationKey.identityNamespaces %}
                "{{ns}}": [
                    {% for id in profile.identityMap[ns] %}
                    "{{id.id}}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]{% if not loop.last %},{% endif %}
                {% endfor %}
            }{% if not loop.last %},{% endif %}
            {% endfor %}
        ]
}
```

**Risultato**

Il `json` seguente rappresenta i dati esportati da Adobe Experience Platform.

```json
{
   "profiles":[
      {
         "email":[
            "e1@example.com",
            "e2@example.com"
         ],
         "phone":[
            "+40744111222"
         ]
      },
      {
         "email":[
            "e3@example.com"
         ],
         "phone":[
            "+40744333444",
            "+40744555666"
         ]
      }
   ]
}
```

#### Utilizzare la chiave di aggregazione in un modello URL

A seconda del caso d’uso, puoi anche utilizzare le chiavi di aggregazione descritte qui in un URL, come illustrato di seguito:

```python
https://api.example.com/audience/{{input.aggregationKey.segmentId}}
```

### Riferimento: Contesto e funzioni utilizzati nei modelli di trasformazione {#reference}

Il contesto fornito al modello contiene `input` (i profili/dati esportati in questa chiamata) e `destination` (i dati sulla destinazione a cui l’Adobe invia i dati, validi per tutti i profili).

La tabella seguente fornisce una descrizione delle funzioni degli esempi precedenti.

| Funzione | Descrizione |
|---------|----------|
| `input.profile` | Il profilo, rappresentato come [JsonNode](http://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). Segue lo schema XDM partner menzionato più avanti in questa pagina. |
| `destination.segmentAliases` | Mappa dagli ID segmento nello spazio dei nomi Adobe Experience Platform agli alias dei segmenti nel sistema del partner. |
| `destination.segmentNames` | Esegui la mappatura dai nomi dei segmenti nello spazio dei nomi Adobe Experience Platform ai nomi dei segmenti nel sistema del partner. |
| `addedSegments(listOfSegments)` | Restituisce solo i segmenti che hanno lo stato `realized` o `existing`. |
| `removedSegments(listOfSegments)` | Restituisce solo i segmenti che hanno lo stato `exited`. |

<!--

## What Adobe needs from you to set up your destination {#what-adobe-needs}

Based on the transformations outlined in the sections above, Adobe needs the following information to set up your destination:

* Considering *all* the fields that your platform can receive, Adobe needs the standard JSON schema that corresponds to your expected message format. Having the template allows Adobe to define transformations and to create a custom XDM schema for your company, which customers would use to export data to your destination.

-->
