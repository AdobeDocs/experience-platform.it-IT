---
description: Questa pagina tratta il formato del messaggio e la trasformazione del profilo nei dati esportati da Adobe Experience Platform nelle destinazioni.
title: Formato del messaggio
exl-id: 1212c1d0-0ada-4ab8-be64-1c62a1158483
source-git-commit: bd89df0659604c05ffd049682343056dbe5667e3
workflow-type: tm+mt
source-wordcount: '2266'
ht-degree: 2%

---

# Formato del messaggio

## Prerequisiti - Concetti di Adobe Experience Platform {#prerequisites}

Per comprendere il formato del messaggio e la configurazione e la trasformazione del profilo sul lato Adobe, acquisisci familiarità con i seguenti concetti di Experience Platform:

* **Experience Data Model (XDM)**. [Panoramica di XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it) e  [Come creare uno schema XDM in Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=it).
* **Classe**. [Creare e modificare le classi nell’interfaccia utente](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/classes.html?lang=en).
* **IdentityMap**. La mappa delle identità rappresenta una mappa di tutte le identità degli utenti finali in Adobe Experience Platform. Fai riferimento a `xdm:identityMap` nel [Dizionario campo XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).
* **SegmentMembership**. Il [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) L’attributo XDM indica di quali segmenti è membro un profilo. Per i tre valori diversi in `status` , leggi la documentazione su [Gruppo di campi schema Dettagli appartenenza segmento](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

## Panoramica {#overview}

Utilizza il contenuto di questa pagina insieme al resto del [opzioni di configurazione per le destinazioni partner](./configuration-options.md). Questa pagina tratta il formato del messaggio e la trasformazione del profilo nei dati esportati da Adobe Experience Platform nelle destinazioni. L’altra pagina tratta informazioni specifiche sulla connessione e l’autenticazione alla destinazione.

Adobe Experience Platform esporta dati in un numero significativo di destinazioni, in vari formati di dati. Alcuni esempi di tipi di destinazione sono le piattaforme pubblicitarie (Google), i social network (Facebook) e le posizioni di archiviazione cloud (Amazon S3, Azure Event Hubs).

Experience Platform può regolare il formato dei messaggi dei profili esportati in modo che corrisponda al formato previsto sul tuo lato. Per comprendere questa personalizzazione, sono importanti i seguenti concetti:
* Schema XDM di origine (1) e destinazione (2) in Adobe Experience Platform
* il formato previsto del messaggio sul lato partner (3), e
* Il livello di trasformazione tra lo schema XDM e il formato del messaggio previsto, che puoi definire creando un [modello di trasformazione dei messaggi](./message-format.md#using-templating).

![Trasformazione da schema a JSON](./assets/transformations-3-steps.png)

Experience Platform utilizza gli schemi XDM per descrivere la struttura dei dati in modo coerente e riutilizzabile.

<!--

Users who want to activate data to your destination need to map the fields in their Experience Platform datasets to a schema that translates to your destination's expected format. Adobe will create a custom field group for your company to add to the target schema. The fields in the field group depend on the profile attribute fields that you can receive.

-->

**Schema XDM di origine (1)**: questo elemento fa riferimento allo schema utilizzato dai clienti in Experience Platform. Ad Experience Platform, nella sezione [passaggio di mappatura](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#mapping) del flusso di lavoro di attivazione destinazione, i clienti mappano i campi dal proprio schema XDM allo schema di destinazione della tua destinazione (2).

**Schema XDM di destinazione (2)**: in base allo schema JSON standard (3) del formato previsto della destinazione e agli attributi che la destinazione può interpretare, puoi definire gli attributi e le identità del profilo nello schema XDM di destinazione. Puoi eseguire questa operazione nella configurazione delle destinazioni, nel [schemaConfig](./destination-configuration.md#schema-configuration) e [identityNamespaces](./destination-configuration.md#identities-and-attributes) oggetti.

**Schema standard JSON degli attributi del profilo di destinazione (3)**: questo esempio rappresenta una [Schema JSON](https://json-schema.org/learn/miscellaneous-examples.html) di tutti gli attributi di profilo supportati dalla piattaforma e dei relativi tipi (ad esempio: oggetto, stringa, array). Campi di esempio che la tua destinazione potrebbe supportare `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName`e così via. Hai bisogno di un [modello di trasformazione dei messaggi](./message-format.md#using-templating) per adattare i dati esportati da Experience Platform al formato previsto.

In base alle trasformazioni dello schema descritte in precedenza, ecco come cambia la configurazione di un profilo tra lo schema XDM di origine e uno schema di esempio sul lato partner:

![Esempio di messaggio delle trasformazioni](./assets/transformations-with-examples.png)

## Guida introduttiva: trasformazione di tre attributi di base {#getting-started}

Per illustrare il processo di trasformazione del profilo, l’esempio seguente utilizza tre attributi di profilo comuni in Adobe Experience Platform: **nome**, **cognome**, e **indirizzo e-mail**.

>[!NOTE]
>
>Il cliente mappa gli attributi dallo schema XDM di origine allo schema XDM del partner nell’interfaccia utente di Adobe Experience Platform, nel **Mappatura** passaggio del [attiva flusso di lavoro destinazione](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

Supponiamo che la tua piattaforma possa ricevere un formato di messaggio come:

```shell
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

| Attributo nello schema XDM del partner sul lato Adobe | Transformation (Trasformazione) | Attributo nel messaggio HTTP sul tuo lato |
|---------|----------|---------|
| `_your_custom_schema.firstName` | ` attributes.first_name` | `first_name` |
| `_your_custom_schema.lastName` | `attributes.last_name` | `last_name` |
| `personalEmail.address` | `attributes.external_id` | `external_id` |

{style="table-layout:auto"}

## Struttura del profilo in Experience Platform {#profile-structure}

Per comprendere gli esempi più avanti nella pagina, è importante conoscere la struttura di un profilo in Experience Platform.

I profili hanno 3 sezioni:

* `segmentMembership` (sempre presente in un profilo)
   * questa sezione contiene tutti i segmenti presenti nel profilo. I segmenti possono avere uno dei tre stati seguenti: `realized`, `existing`, `exited`.
* `identityMap` (sempre presente in un profilo)
   * questa sezione contiene tutte le identità presenti nel profilo (e-mail, Google GAID, Apple IDFA e così via) e di cui l’utente ha eseguito la mappatura per l’esportazione nel flusso di lavoro di attivazione.
* attributi (a seconda della configurazione di destinazione, questi potrebbero essere presenti nel profilo). C’è anche una leggera differenza da notare tra gli attributi predefiniti e gli attributi a forma libera:
   * per *attributi a forma libera*, che contengono una `.value` percorso se l’attributo è presente nel profilo (vedi `lastName` dall&#39;esempio 1). Se non sono presenti nel profilo, non conterranno `.value` percorso (vedere `firstName` dall&#39;esempio 1).
   * per *attributi predefiniti*, questi non contengono un `.value` percorso. Tutti gli attributi mappati presenti in un profilo saranno presenti nella mappa degli attributi. Quelli che non sono presenti non saranno presenti (vedere Esempio 2 - il `firstName` non esiste nel profilo).

Di seguito sono riportati due Experienci Platform di profili:

### Esempio 1 con `segmentMembership`, `identityMap` Attributi e per attributi a forma libera {#example-1}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "mobileIds": [
      {
        "id": "e86fb215-0921-4537-bc77-969ff775752c"
      }
    ]
  },
  "attributes": {
    "firstName": {
    },
    "lastName": {
      "value": "lastName"
    }
  }
}
```

### Esempio 2 con `segmentMembership`, `identityMap` Attributi e per attributi predefiniti {#example-2}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "mobileIds": [
      {
        "id": "e86fb215-0921-4537-bc77-969ff775752c"
      }
    ]
  },
  "attributes": {
    "lastName": "lastName"
  }
}
```

## Utilizzo di un linguaggio per modelli per le trasformazioni di identità, attributi e appartenenze a segmenti {#using-templating}

utilizzi Adobi [Modelli di ciottoli](https://pebbletemplates.io/), un linguaggio per modelli simile a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/), per trasformare i campi dallo schema XDM Experience Platform in un formato supportato dalla tua destinazione.

Questa sezione fornisce diversi esempi di come vengono effettuate queste trasformazioni, dallo schema XDM di input fino al modello e all’output nei formati di payload accettati dalla destinazione. Gli esempi seguenti sono presentati dalla complessità crescente, come segue:

1. Semplici esempi di trasformazione. Scopri come funziona il template con trasformazioni semplici per [Attributi del profilo](./message-format.md#attributes), [Iscrizione al segmento](./message-format.md#segment-membership), e [Identità](./message-format.md#identities) campi.
2. Sono stati aggiunti esempi di complessità dei modelli che combinano i campi riportati sopra: [Creare un modello che invia segmenti e identità](./message-format.md#segments-and-identities) e [Creare un modello che invia segmenti, identità e attributi di profilo](./message-format.md#segments-identities-attributes).
3. Modelli che includono la chiave di aggregazione. Quando si utilizza [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) nella configurazione di destinazione, Experience Platform raggruppa i profili esportati nella destinazione in base a criteri quali ID segmento, stato del segmento o spazi dei nomi di identità.

### Attributi del profilo {#attributes}

Per trasformare gli attributi del profilo esportati nella destinazione, consulta il JSON e gli esempi di codice seguenti.

>[!IMPORTANT]
>
>Per un elenco di tutti gli attributi di profilo disponibili in Adobe Experience Platform, vedi [Dizionario campo XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).


**Input**

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
>Per tutti i modelli utilizzati, è necessario utilizzare caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello in [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 della [Standard JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

### Appartenenza a un segmento {#segment-membership}

Il [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) L’attributo XDM indica di quali segmenti è membro un profilo.
Per i tre valori diversi in `status` , leggi la documentazione su [Gruppo di campi schema Dettagli appartenenza segmento](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

**Input**

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
>Per tutti i modelli utilizzati, è necessario utilizzare caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello in [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 della [Standard JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

Per informazioni sulle identità in Experience Platform, consulta [Panoramica sullo spazio dei nomi delle identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=it).

**Input**

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
>Per tutti i modelli utilizzati, è necessario utilizzare caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello in [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 della [Standard JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
L’esempio seguente mostra come trasformare l’iscrizione al segmento e il formato delle identità e come eseguirne l’output nella destinazione.

**Input**

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
>Per tutti i modelli utilizzati, è necessario utilizzare caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello in [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 della [Standard JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

Il `json` di seguito sono riportati i dati esportati da Adobe Experience Platform.

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

Un altro caso d’uso comune è l’esportazione di dati che contengono appartenenza a segmenti, identità (ad esempio: indirizzo e-mail, numero di telefono, ID pubblicitario) e attributi di profilo. Per esportare i dati in questo modo, vedi l’esempio seguente:

**Input**

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
>Per tutti i modelli utilizzati, è necessario utilizzare caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello in [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 della [Standard JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

Il `json` di seguito sono riportati i dati esportati da Adobe Experience Platform.

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

### Includi la chiave di aggregazione nel modello per accedere ai profili esportati raggruppati per vari criteri {#template-aggregation-key}

Quando si utilizza [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) nella configurazione di destinazione, puoi raggruppare i profili esportati nella destinazione in base a criteri quali ID segmento, alias segmento, appartenenza al segmento o spazi dei nomi delle identità.

Nel modello di trasformazione dei messaggi, puoi accedere alle chiavi di aggregazione indicate in precedenza, come mostrato negli esempi nelle sezioni seguenti. Utilizza le chiavi di aggregazione per strutturare il messaggio HTTP esportato da Experience Platform in modo che corrisponda ai limiti di formato e frequenza previsti dalla destinazione.

#### Utilizza la chiave di aggregazione ID segmento nel modello {#aggregation-key-segment-id}

Se usa [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) e imposta `includeSegmentId` su true, i profili nei messaggi HTTP esportati nella destinazione sono raggruppati per ID segmento. Di seguito trovi le modalità di accesso all’ID segmento nel modello.

**Input**

Considera i quattro profili seguenti, dove:
* i primi due fanno parte del segmento con l’ID segmento `788d8874-8007-4253-92b7-ee6b6c20c6f3`
* il terzo profilo fa parte del segmento con l’ID segmento `8f812592-3f06-416b-bd50-e7831848a31a`
* il quarto profilo fa parte di entrambi i segmenti qui sopra.

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
>Per tutti i modelli utilizzati, è necessario utilizzare caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello in [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 della [Standard JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Osserva come `audienceId` viene utilizzato nel modello per accedere agli ID dei segmenti. Questo esempio presuppone che tu utilizzi `audienceId` per l’iscrizione al segmento nella tassonomia di destinazione. In alternativa, puoi utilizzare qualsiasi altro nome di campo, a seconda della tassonomia.

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

Quando vengono esportati nella destinazione, i profili vengono suddivisi in due gruppi, in base al loro ID segmento.

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

#### Usa chiave di aggregazione alias segmento nel modello {#aggregation-key-segment-alias}

Se usa [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) e imposta `includeSegmentId` se impostato su true, puoi anche accedere all’alias del segmento nel modello.

Aggiungi la riga seguente al modello per accedere ai profili esportati raggruppati per alias del segmento.

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### Utilizza la chiave di aggregazione dello stato del segmento nel modello {#aggregation-key-segment-status}

Se usa [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) e imposta `includeSegmentId` e `includeSegmentStatus` se impostato su true, puoi accedere allo stato del segmento nel modello. In questo modo, puoi raggruppare i profili nei messaggi HTTP esportati nella destinazione in base al fatto che debbano essere aggiunti o rimossi dai segmenti.

I valori possibili sono:

* realizzato
* esistente
* uscita

Aggiungi la riga seguente al modello per aggiungere o rimuovere profili dai segmenti, in base ai valori riportati sopra:

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### Utilizza la chiave di aggregazione dello spazio dei nomi dell’identità nel modello {#aggregation-key-identity}

Di seguito è riportato un esempio in cui [aggregazione configurabile](./destination-configuration.md#configurable-aggregation) nella configurazione di destinazione è impostato per aggregare i profili esportati in base agli spazi dei nomi delle identità, nel modulo `"namespaces": ["email", "phone"]` e `"namespaces": ["GAID", "IDFA"]`. Consulta la sezione `groups` parametro in [riferimento API per la configurazione di destinazione](./destination-configuration-api.md) per ulteriori informazioni su questo raggruppamento.

**Input**

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
>Per tutti i modelli utilizzati, è necessario utilizzare caratteri non validi, ad esempio virgolette doppie `""` prima di inserire il modello in [configurazione del server di destinazione](./server-and-template-configuration.md#template-specs). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 della [Standard JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

Quando vengono esportati nella destinazione, i profili vengono suddivisi in due gruppi, in base ai rispettivi spazi dei nomi di identità. E-mail e telefono si trovano in un gruppo, mentre GAID e IDFA si trovano in un altro.

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

A seconda del caso di utilizzo, puoi utilizzare anche le chiavi di aggregazione qui descritte in un URL, come mostrato di seguito:

```python
https://api.example.com/audience/{{input.aggregationKey.segmentId}}
```

### Riferimento: contesto e funzioni utilizzati nei modelli di trasformazione {#reference}

Il contesto fornito al modello contiene `input`  (i profili/dati esportati in questa chiamata) e `destination` (dati sulla destinazione a cui l’Adobe invia i dati, validi per tutti i profili).

La tabella seguente fornisce le descrizioni delle funzioni negli esempi precedenti.

| Funzione | Descrizione |
|---------|----------|
| `input.profile` | Il profilo, rappresentato come [JsonNode](https://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). Segue lo schema XDM del partner menzionato più sopra in questa pagina. |
| `destination.segmentAliases` | Mappa dagli ID segmento nello spazio dei nomi Adobe Experience Platform agli alias segmento nel sistema del partner. |
| `destination.segmentNames` | Mappa i nomi dei segmenti nello spazio dei nomi di Adobe Experience Platform ai nomi dei segmenti nel sistema del partner. |
| `addedSegments(listOfSegments)` | Restituisce solo i segmenti con stato `realized` o `existing`. |
| `removedSegments(listOfSegments)` | Restituisce solo i segmenti con stato `exited`. |

{style="table-layout:auto"}

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come vengono trasformati i dati esportati da Experience Platform. Quindi, leggi le pagine seguenti per approfondire le tue conoscenze sulla creazione di modelli di trasformazione dei messaggi per la tua destinazione:

* [Creare e testare un modello di trasformazione dei messaggi](/help/destinations/destination-sdk/create-template.md)
* [Operazioni API del modello di rendering](/help/destinations/destination-sdk/render-template-api.md)
* [Funzioni di trasformazione supportate in Destination SDK](/help/destinations/destination-sdk/supported-functions.md)
