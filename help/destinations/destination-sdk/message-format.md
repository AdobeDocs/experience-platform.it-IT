---
description: Questa pagina tratta il formato del messaggio e la trasformazione del profilo nei dati esportati da Adobe Experience Platform alle destinazioni.
title: Formato del messaggio
exl-id: 1212c1d0-0ada-4ab8-be64-1c62a1158483
source-git-commit: 468b9309c5184684c0b25c2656a9eef37715af53
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 2%

---

# Formato del messaggio

## Prerequisiti - Concetti di Adobe Experience Platform {#prerequisites}

Per comprendere il formato del messaggio e la configurazione del profilo e il processo di trasformazione sul lato Adobe, ti preghiamo di acquisire familiarità con i seguenti concetti di Experience Platform:

* **Experience Data Model (XDM)**. [Panoramica di XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it) e  [Come creare uno schema XDM in Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en).
* **Classe**. [Creare e modificare le classi nell’interfaccia utente](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/classes.html?lang=en).
* **IdentityMap**. La mappa identità rappresenta una mappa di tutte le identità dell’utente finale in Adobe Experience Platform. Fai riferimento a `xdm:identityMap` in [Dizionario dei campi XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).
* **SegmentMembership**. La [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) L’attributo XDM indica di quali segmenti fa parte un profilo. Per i tre valori diversi nel `status` , leggi la documentazione su [Gruppo di campi Dettagli appartenenza segmento](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

## Panoramica {#overview}

Utilizza il contenuto di questa pagina insieme al resto del [opzioni di configurazione per le destinazioni dei partner](./configuration-options.md). Questa pagina tratta il formato del messaggio e la trasformazione del profilo nei dati esportati da Adobe Experience Platform alle destinazioni. L’altra pagina contiene informazioni specifiche sulla connessione e l’autenticazione alla destinazione.

Adobe Experience Platform esporta i dati in un numero significativo di destinazioni, in vari formati di dati. Alcuni esempi di tipi di destinazione sono piattaforme pubblicitarie (Google), social network (Facebook) e posizioni di archiviazione cloud (Amazon S3, Azure Event Hubs).

Ad Experience Platform, puoi regolare il formato del messaggio dei profili esportati in modo che corrisponda al formato previsto sul tuo lato. Per comprendere questa personalizzazione, sono importanti i seguenti concetti:
* Lo schema XDM di origine (1) e di destinazione (2) in Adobe Experience Platform
* il formato previsto del messaggio sul lato partner (3) e
* Il livello di trasformazione tra lo schema XDM e il formato del messaggio previsto, che è possibile definire creando un [modello di trasformazione dei messaggi](./message-format.md#using-templating).

![Schema di trasformazione JSON](./assets/transformations-3-steps.png)

Experience Platform utilizza gli schemi XDM per descrivere la struttura dei dati in modo coerente e riutilizzabile.

<!--

Users who want to activate data to your destination need to map the fields in their Experience Platform datasets to a schema that translates to your destination's expected format. Adobe will create a custom field group for your company to add to the target schema. The fields in the field group depend on the profile attribute fields that you can receive.

-->

**Schema XDM di origine (1)**: Questo elemento fa riferimento allo schema utilizzato ad Experience Platform dai clienti. Ad Experience Platform, nella [fase di mappatura](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#mapping) del flusso di lavoro di destinazione di attivazione, i clienti mappano i campi dallo schema di origine allo schema di destinazione della tua destinazione (2).

**Schema XDM di Target (2)**: In base allo schema JSON standard (3) del formato previsto della destinazione, puoi definire attributi e identità di profilo nello schema XDM di destinazione. Puoi eseguire questa operazione nella configurazione delle destinazioni, nel [schemaConfig](./destination-configuration.md#schema-configuration) e [identityNamespaces](./destination-configuration.md#identities-and-attributes) oggetti.

**Schema JSON standard degli attributi del profilo di destinazione (3)**: Questo elemento rappresenta un [Schema JSON](https://json-schema.org/learn/miscellaneous-examples.html) di tutti gli attributi di profilo supportati dalla piattaforma e dei relativi tipi (ad esempio: oggetto, stringa, array). Campi di esempio supportati dalla destinazione `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName`e così via. Hai bisogno di un [modello di trasformazione dei messaggi](./message-format.md#using-templating) per adattare i dati esportati da Experience Platform al formato previsto.

In base alle trasformazioni dello schema descritte qui sopra, viene illustrato come cambia una configurazione del profilo tra lo schema XDM di origine e uno schema di esempio sul lato partner:

![Esempio di messaggio di trasformazione](./assets/transformations-with-examples.png)

<br> 


## Guida introduttiva - trasformazione di tre attributi di base {#getting-started}

Per illustrare il processo di trasformazione del profilo, l’esempio seguente utilizza tre attributi di profilo comuni in Adobe Experience Platform: **nome**, **cognome** e **indirizzo e-mail**.

>[!NOTE]
>
>Il cliente mappa gli attributi dallo schema XDM di origine allo schema XDM del partner nell’interfaccia utente di Adobe Experience Platform, nel **Mappatura** fase [attiva flusso di lavoro di destinazione](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

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

Adobe utilizza un linguaggio modello simile a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) per trasformare i campi dallo schema XDM in un formato supportato dalla destinazione.

Questa sezione fornisce diversi esempi di come vengono effettuate queste trasformazioni - dallo schema XDM di input, attraverso il modello e l’output nei formati di payload accettati dalla destinazione. Gli esempi seguenti sono presentati da una complessità crescente, come segue:

1. Semplici esempi di trasformazione. Scopri come la templazione funziona con semplici trasformazioni per [Attributi del profilo](./message-format.md#attributes), [Iscrizione al segmento](./message-format.md#segment-membership)e [Identità](./message-format.md#identities) campi.
2. Esempi di modelli più complessi che combinano i campi di cui sopra: [Creare un modello che invia segmenti e identità](./message-format.md#segments-and-identities) e [Creare un modello che invia segmenti, identità e attributi di profilo](./message-format.md#segments-identities-attributes).
3. Modelli che includono la chiave di aggregazione. Quando utilizzi [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) nella configurazione di destinazione, Experience Platform raggruppa i profili esportati nella destinazione in base a criteri come ID segmento, stato del segmento o spazi dei nomi delle identità.

### Attributi del profilo {#attributes}

Per trasformare gli attributi di profilo esportati nella destinazione, consulta il JSON e gli esempi di codice riportati di seguito.

>[!IMPORTANT]
>
>Per un elenco di tutti gli attributi di profilo disponibili in Adobe Experience Platform, consulta la sezione [Dizionario dei campi XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).


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
>Per tutti i modelli utilizzati, è necessario evitare i caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello nel [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 nella [Standard JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

La [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) L’attributo XDM indica di quali segmenti fa parte un profilo.
Per i tre valori diversi nel `status` , leggi la documentazione su [Gruppo di campi Dettagli appartenenza segmento](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

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
>Per tutti i modelli utilizzati, è necessario evitare i caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello nel [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 nella [Standard JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

Per informazioni sulle identità in Experience Platform, consulta la sezione [Panoramica dello spazio dei nomi identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=it).

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
>Per tutti i modelli utilizzati, è necessario evitare i caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello nel [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 nella [Standard JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
>Per tutti i modelli utilizzati, è necessario evitare i caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello nel [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 nella [Standard JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

La `json` di seguito sono riportati i dati esportati da Adobe Experience Platform.

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
>Per tutti i modelli utilizzati, è necessario evitare i caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello nel [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 nella [Standard JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

La `json` di seguito sono riportati i dati esportati da Adobe Experience Platform.

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

### Includi chiave di aggregazione nel modello per accedere ai profili esportati raggruppati per vari criteri {#template-aggregation-key}

Quando utilizzi [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) nella configurazione di destinazione, puoi raggruppare i profili esportati nella destinazione in base a criteri quali ID segmento, alias segmento, appartenenza al segmento o namespace di identità.

Nel modello di trasformazione dei messaggi, puoi accedere alle chiavi di aggregazione di cui sopra, come mostrato negli esempi nelle sezioni seguenti. Utilizza le chiavi di aggregazione per strutturare il messaggio HTTP esportato fuori da Experience Platform in modo che corrisponda ai limiti di formato e tasso previsti dalla destinazione.

#### Utilizza la chiave di aggregazione ID segmento nel modello {#aggregation-key-segment-id}

Se utilizzi [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) e impostare `includeSegmentId` su true, i profili nei messaggi HTTP esportati nella destinazione sono raggruppati per ID segmento. Vedi sotto come puoi accedere all’ID del segmento nel modello.

**Ingresso**

Considera i quattro profili seguenti, dove:
* i primi due fanno parte del segmento con l’ID del segmento `788d8874-8007-4253-92b7-ee6b6c20c6f3`
* il terzo profilo fa parte del segmento con l’ID del segmento `8f812592-3f06-416b-bd50-e7831848a31a`
* il quarto profilo fa parte di entrambi i segmenti di cui sopra.

Profilo 1:

```json
{
   "attributes":{
      "firstName":{
         "value":"Hermione"
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
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"existing"
         },
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"existing"
         }
      }
   }
}
```

**Modello**

>[!IMPORTANT]
>
>Per tutti i modelli utilizzati, è necessario evitare i caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello nel [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 nella [Standard JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Di seguito viene illustrato come `audienceId` viene utilizzato nel modello per accedere agli ID del segmento. Questo esempio presuppone che l&#39;utente utilizzi `audienceId` per l’appartenenza al segmento nella tassonomia di destinazione. È invece possibile utilizzare qualsiasi altro nome di campo, a seconda della tassonomia.

```python
{
    "audienceId": "{{ input.aggregationKey.segmentId }}",
    "profiles": [
        {% for profile in input.profiles %}
        {
            "first_name": "{{ profile.attributes.firstName.value }}"
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Risultato**

Quando vengono esportati nella destinazione, i profili vengono suddivisi in due gruppi, in base al relativo ID segmento.

```json
{
   "audienceId":"788d8874-8007-4253-92b7-ee6b6c20c6f3",
   "profiles":[
      {
         "firstName":"Hermione"
      },
      {
         "firstName":"Harry"
      },
      {
         "firstName":"Jerry"
      }
   ]
}
```

```json
{
   "audienceId":"8f812592-3f06-416b-bd50-e7831848a31a",
   "profiles":[
      {
         "firstName":"Tom"
      },
      {
         "firstName":"Jerry"
      }
   ]
}
```

#### Utilizza la chiave di aggregazione degli alias dei segmenti nel modello {#aggregation-key-segment-alias}

Se utilizzi [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) e impostare `includeSegmentId` su true, puoi anche accedere all’alias del segmento nel modello.

Aggiungi la riga sottostante al modello per accedere ai profili esportati raggruppati per alias del segmento.

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### Utilizza la chiave di aggregazione dello stato del segmento nel modello {#aggregation-key-segment-status}

Se utilizzi [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) e impostare `includeSegmentId` e `includeSegmentStatus` su true, puoi accedere allo stato del segmento nel modello. In questo modo, puoi raggruppare i profili nei messaggi HTTP esportati nella tua destinazione in base al fatto che i profili debbano essere aggiunti o rimossi dai segmenti.

I valori possibili sono:

* realizzato
* esistente
* uscito

Aggiungi la riga sottostante al modello per aggiungere o rimuovere profili dai segmenti, in base ai valori sopra riportati:

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### Utilizza la chiave di aggregazione dello spazio dei nomi identità nel modello {#aggregation-key-identity}

Di seguito è riportato un esempio in cui il [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) nella configurazione di destinazione viene impostato per aggregare i profili esportati in base ai namespace di identità nel modulo `"namespaces": ["email", "phone"]` e `"namespaces": ["GAID", "IDFA"]`. Fai riferimento a `groups` nel [riferimento API per la configurazione della destinazione](./destination-configuration-api.md) per ulteriori informazioni su questo raggruppamento.

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
      ],
      "IDFA":[
         {
            "id":"AEBE52E7-03EE-455A-B3C4-E57283966239"
         }
      ],
      "GAID":[
         {
            "id":"e4fe9bde-caa0-47b6-908d-ffba3fa184f2"
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
      ],
      "IDFA":[
         {
            "id":"134GHU45-34HH-GHJ7-K0H8-LHN665998NN0"
         }
      ],
      "GAID":[
         {
            "id":"47bh00i9-8jv6-334n-lll8-nb7f24sghg76"
         }
      ]
   }
}
```

**Modello**

>[!IMPORTANT]
>
>Per tutti i modelli utilizzati, è necessario evitare i caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello nel [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 nella [Standard JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Tieni presente che `input.aggregationKey.identityNamespaces` viene utilizzato nel modello seguente

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

Quando vengono esportati nella destinazione, i profili vengono suddivisi in due gruppi, in base ai rispettivi namespace di identità. Le e-mail e il telefono sono in un gruppo, mentre GAID e IDFA sono in un altro.

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

```json
{
   "profiles":[
      {
         "IDFA":[
            "AEBE52E7-03EE-455A-B3C4-E57283966239"
         ],
         "GAID":[
            "e4fe9bde-caa0-47b6-908d-ffba3fa184f2"
         ]
      },
      {
         "IDFA":[
            "134GHU45-34HH-GHJ7-K0H8-LHN665998NN0"
         ],
         "GAID":[
            "47bh00i9-8jv6-334n-lll8-nb7f24sghg76"
         ]
      }
   ]
}
```

#### Utilizzare la chiave di aggregazione in un modello URL {#aggregation-key-url-template}

A seconda del caso d’uso, puoi anche utilizzare le chiavi di aggregazione descritte qui in un URL, come illustrato di seguito:

```python
https://api.example.com/audience/{{input.aggregationKey.segmentId}}
```

### Riferimento: Contesto e funzioni utilizzati nei modelli di trasformazione {#reference}

Il contesto fornito al modello contiene `input`  (i profili/dati esportati in questa chiamata) e `destination` (dati sulla destinazione a cui l’Adobe invia i dati, validi per tutti i profili).

La tabella seguente fornisce una descrizione delle funzioni degli esempi precedenti.

| Funzione | Descrizione |
|---------|----------|
| `input.profile` | Il profilo, rappresentato come [JsonNode](https://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). Segue lo schema XDM partner menzionato più avanti in questa pagina. |
| `destination.segmentAliases` | Mappa dagli ID segmento nello spazio dei nomi Adobe Experience Platform agli alias dei segmenti nel sistema del partner. |
| `destination.segmentNames` | Esegui la mappatura dai nomi dei segmenti nello spazio dei nomi Adobe Experience Platform ai nomi dei segmenti nel sistema del partner. |
| `addedSegments(listOfSegments)` | Restituisce solo i segmenti con stato `realized` o `existing`. |
| `removedSegments(listOfSegments)` | Restituisce solo i segmenti con stato `exited`. |

<!--

## What Adobe needs from you to set up your destination {#what-adobe-needs}

Based on the transformations outlined in the sections above, Adobe needs the following information to set up your destination:

* Considering *all* the fields that your platform can receive, Adobe needs the standard JSON schema that corresponds to your expected message format. Having the template allows Adobe to define transformations and to create a custom XDM schema for your company, which customers would use to export data to your destination.

-->
