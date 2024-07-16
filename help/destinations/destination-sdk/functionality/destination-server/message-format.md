---
description: Questa pagina tratta il formato del messaggio e la trasformazione del profilo nei dati esportati da Adobe Experience Platform nelle destinazioni.
title: Formato del messaggio
exl-id: ab05d34e-530f-456c-b78a-7f3389733d35
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '2489'
ht-degree: 0%

---

# Formato del messaggio

## Prerequisiti - Concetti di Adobe Experience Platform {#prerequisites}

Per comprendere il formato del messaggio e la configurazione e la trasformazione del profilo sul lato Adobe, acquisisci familiarità con i seguenti concetti di Experience Platform:

* **Experience Data Model (XDM)**. [Panoramica XDM](../../../../xdm/home.md) e [Come creare uno schema XDM in Adobe Experience Platform](../../../../xdm/tutorials/create-schema-ui.md).
* **Classe**. [Creare e modificare le classi nell&#39;interfaccia utente](../../../../xdm/ui/resources/classes.md).
* **IdentityMap**. La mappa delle identità rappresenta una mappa di tutte le identità degli utenti finali in Adobe Experience Platform. Fare riferimento a `xdm:identityMap` nel dizionario di campi [XDM](../../../../xdm/schema/field-dictionary.md).
* **AppartenenzaSegmento**. L&#39;attributo XDM [segmentMembership](../../../../xdm/schema/field-dictionary.md) indica di quali tipi di pubblico è membro un profilo. Per i tre valori diversi nel campo `status`, leggere la documentazione sul gruppo di campi schema [Dettagli appartenenza pubblico](../../../../xdm/field-groups/profile/segmentation.md).

>[!IMPORTANT]
>
>Tutti i nomi e i valori dei parametri supportati da Destination SDK sono **con distinzione tra maiuscole e minuscole**. Per evitare errori di distinzione tra maiuscole e minuscole, utilizza i nomi e i valori dei parametri esattamente come mostrato nella documentazione.

## Tipi di integrazione supportati {#supported-integration-types}

Consulta la tabella seguente per informazioni dettagliate sui tipi di integrazioni che supportano le funzionalità descritte in questa pagina.

| Tipo di integrazione | Supporta la funzionalità |
|---|---|
| Integrazioni in tempo reale (streaming) | Sì |
| Integrazioni basate su file (batch) | Sì (solo i punti 1 e 2 del diagramma seguente) |

## Panoramica {#overview}

Questa pagina tratta il formato del messaggio e la trasformazione del profilo nei dati esportati da Adobe Experience Platform nelle destinazioni.

Adobe Experience Platform esporta dati in un numero significativo di destinazioni, in vari formati di dati. Alcuni esempi di tipi di destinazione sono le piattaforme pubblicitarie (Google), i social network (Facebook) e le posizioni di archiviazione cloud (Amazon S3, Azure Event Hubs).

Experience Platform può regolare il formato dei messaggi dei profili esportati in modo che corrisponda al formato previsto sul tuo lato. Per comprendere questa personalizzazione, sono importanti i seguenti concetti:

* Schema XDM di origine (1) e destinazione (2) in Adobe Experience Platform
* il formato previsto del messaggio sul lato partner (3), e
* Livello di trasformazione tra lo schema XDM e il formato del messaggio previsto, che è possibile definire creando un [modello di trasformazione del messaggio](#using-templating).

![Trasformazione da schema a JSON](../../assets/functionality/destination-server/transformations-3-steps.png)

Experience Platform utilizza gli schemi XDM per descrivere la struttura dei dati in modo coerente e riutilizzabile.

<!--

Users who want to activate data to your destination need to map the fields in their Experience Platform datasets to a schema that translates to your destination's expected format. Adobe will create a custom field group for your company to add to the target schema. The fields in the field group depend on the profile attribute fields that you can receive.

-->

**Schema XDM di Source (1)**: questo elemento fa riferimento allo schema utilizzato dai clienti in Experience Platform. Ad Experience Platform, nel [passaggio di mappatura](../../../ui/activate-segment-streaming-destinations.md#mapping) del flusso di lavoro attiva destinazione, i clienti mappano i campi dal proprio schema XDM allo schema di destinazione della destinazione (2).

**Schema XDM di destinazione (2)**: in base allo schema JSON standard (3) del formato previsto della destinazione e agli attributi che la destinazione può interpretare, puoi definire gli attributi e le identità del profilo nello schema XDM di destinazione. Puoi eseguire questa operazione nella configurazione delle destinazioni, negli oggetti [schemaConfig](../../functionality/destination-configuration/schema-configuration.md) e [identityNamespaces](../../functionality/destination-configuration/identity-namespace-configuration.md).

**Schema JSON standard degli attributi del profilo di destinazione (3)**: questo esempio rappresenta uno [schema JSON](https://json-schema.org/learn/miscellaneous-examples.html) di tutti gli attributi del profilo supportati dalla piattaforma e i relativi tipi (ad esempio: object, string, array). I campi di esempio che la destinazione potrebbe supportare potrebbero essere `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName` e così via. È necessario un [modello di trasformazione dei messaggi](#using-templating) per adattare i dati esportati in Experience Platform al formato previsto.

In base alle trasformazioni dello schema descritte in precedenza, ecco come cambia la configurazione di un profilo tra lo schema XDM di origine e uno schema di esempio sul lato partner:

![Esempio di messaggio delle trasformazioni](../../assets/functionality/destination-server/transformations-with-examples.png)

## Guida introduttiva: trasformazione di tre attributi di base {#getting-started}

Per illustrare il processo di trasformazione del profilo, nell&#39;esempio seguente vengono utilizzati tre attributi di profilo comuni in Adobe Experience Platform: **nome**, **cognome** e **indirizzo e-mail**.

>[!NOTE]
>
>Il cliente mappa gli attributi dallo schema XDM di origine allo schema XDM del partner nell&#39;interfaccia utente di Adobe Experience Platform, nel passaggio **Mapping** del flusso di lavoro [attiva destinazione](../../../ui/activate-segment-streaming-destinations.md#mapping).

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

| Attributo nello schema XDM del partner sul lato Adobe | Trasformazione | Attributo nel messaggio HTTP sul tuo lato |
|---------|----------|---------|
| `_your_custom_schema.firstName` | ` attributes.first_name` | `first_name` |
| `_your_custom_schema.lastName` | `attributes.last_name` | `last_name` |
| `personalEmail.address` | `attributes.external_id` | `external_id` |

{style="table-layout:auto"}

## Struttura del profilo in Experience Platform {#profile-structure}

Per comprendere gli esempi più avanti nella pagina, è importante conoscere la struttura di un profilo in Experience Platform.

I profili hanno 3 sezioni:

* `segmentMembership` (sempre presente in un profilo)
   * questa sezione contiene tutti i tipi di pubblico presenti nel profilo. I tipi di pubblico possono avere uno dei due stati seguenti: `realized` o `exited`.
* `identityMap` (sempre presente in un profilo)
   * questa sezione contiene tutte le identità presenti nel profilo (e-mail, Google GAID, Apple IDFA e così via) e di cui l’utente ha eseguito la mappatura per l’esportazione nel flusso di lavoro di attivazione.
* attributi (a seconda della configurazione di destinazione, questi potrebbero essere presenti nel profilo). C’è anche una leggera differenza da notare tra gli attributi predefiniti e gli attributi a forma libera:
   * per *attributi a forma libera*, questi contengono un percorso `.value` se l&#39;attributo è presente nel profilo (vedi l&#39;attributo `lastName` dell&#39;esempio 1). Se non sono presenti nel profilo, non conterranno il percorso `.value` (vedi l&#39;attributo `firstName` dell&#39;esempio 1).
   * per *attributi predefiniti*, questi non contengono un percorso `.value`. Tutti gli attributi mappati presenti in un profilo saranno presenti nella mappa degli attributi. Quelli non presenti non saranno presenti (vedi l&#39;esempio 2 - l&#39;attributo `firstName` non esiste nel profilo).

Di seguito sono riportati due Experienci Platform di profili:

### Esempio 1 con `segmentMembership`, `identityMap` e attributi per gli attributi a forma libera {#example-1}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "realized"
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

### Esempio 2 con `segmentMembership`, `identityMap` e attributi per attributi predefiniti {#example-2}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "realized"
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

## Utilizzo di un linguaggio per modelli per le trasformazioni di identità, attributi e appartenenza a un pubblico {#using-templating}

Adobe utilizza [modelli Pebble](https://pebbletemplates.io/), un linguaggio di modelli simile a [Jinja](https://jinja.palletsprojects.com/en/2.11.x/), per trasformare i campi dallo schema XDM Experience Platform in un formato supportato dalla destinazione.

Questa sezione fornisce diversi esempi di come vengono effettuate queste trasformazioni, dallo schema XDM di input fino al modello e all’output nei formati di payload accettati dalla destinazione. Gli esempi seguenti sono presentati dalla complessità crescente, come segue:

1. Semplici esempi di trasformazione. Scopri come funziona il modello con semplici trasformazioni per i campi [Attributi profilo](#attributes), [Appartenenza pubblico](#segment-membership) e [Identità](#identities).
2. Esempi di complessità aumentata dei modelli che combinano i campi riportati sopra: [Crea un modello che invia tipi di pubblico e identità](./message-format.md#segments-and-identities) e [Crea un modello che invia segmenti, identità e attributi di profilo](#segments-identities-attributes).
3. Modelli che includono la chiave di aggregazione. Quando si utilizza l&#39;[aggregazione configurabile](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) nella configurazione di destinazione, Experience Platform raggruppa i profili esportati nella destinazione in base a criteri quali l&#39;ID pubblico, lo stato del pubblico o gli spazi dei nomi di identità.

### Attributi del profilo {#attributes}

Per trasformare gli attributi del profilo esportati nella destinazione, consulta il JSON e gli esempi di codice seguenti.

>[!IMPORTANT]
>
>Per un elenco di tutti gli attributi di profilo disponibili in Adobe Experience Platform, consulta il [dizionario di campi XDM](../../../../xdm/schema/field-dictionary.md).


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
>Per tutti i modelli utilizzati, è necessario eseguire l&#39;escape dei caratteri non validi, ad esempio le virgolette doppie `""`, prima di inserire il [modello](../../functionality/destination-server/templating-specs.md) nella [configurazione del server di destinazione](../../authoring-api/destination-server/create-destination-server.md). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 nello standard [JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

### Appartenenza al pubblico {#audience-membership}

L&#39;attributo XDM [segmentMembership](../../../../xdm/schema/field-dictionary.md) indica di quali tipi di pubblico è membro un profilo.
Per i tre valori diversi nel campo `status`, leggere la documentazione sul gruppo di campi schema [Dettagli appartenenza pubblico](../../../../xdm/field-groups/profile/segmentation.md).

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
        "status": "realized"
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
        "status": "realized"
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
>Per tutti i modelli utilizzati, è necessario eseguire l&#39;escape dei caratteri non validi, ad esempio le virgolette doppie `""`, prima di inserire il [modello](../../functionality/destination-server/templating-specs.md) nella [configurazione del server di destinazione](../../authoring-api/destination-server/create-destination-server.md). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 nello standard [JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).


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
                {# Alternative syntax for filtering audiences by status: #}
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

Per informazioni sulle identità in Experience Platform, consulta la [Panoramica dello spazio dei nomi delle identità](../../../../identity-service/features/namespaces.md).

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
>Per tutti i modelli utilizzati, è necessario eseguire l&#39;escape dei caratteri non validi, ad esempio le virgolette doppie `""`, prima di inserire il [modello](../../functionality/destination-server/templating-specs.md) nella [configurazione del server di destinazione](../../authoring-api/destination-server/create-destination-server.md). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 nello standard [JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

### Creare un modello che invia tipi di pubblico e identità {#segments-and-identities}

Questa sezione fornisce un esempio di trasformazione comunemente utilizzata tra lo schema XDM di Adobe e lo schema di destinazione del partner.
L’esempio seguente mostra come trasformare il formato di appartenenza al pubblico e delle identità e come inviarli alla tua destinazione.

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
              "status": "realized"
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
>Per tutti i modelli utilizzati, è necessario eseguire l&#39;escape dei caratteri non validi, ad esempio le virgolette doppie `""`, prima di inserire il [modello](../../functionality/destination-server/templating-specs.md) nella [configurazione del server di destinazione](../../authoring-api/destination-server/create-destination-server.md). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 nello standard [JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
                    {# Alternative syntax for filtering audiences by status: #}
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

`json` rappresenta i dati esportati da Adobe Experience Platform.

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

Un altro caso d’uso comune è l’esportazione di dati che contengono l’iscrizione al pubblico, le identità (ad esempio: indirizzo e-mail, numero di telefono, ID pubblicitario) e gli attributi del profilo. Per esportare i dati in questo modo, vedi l’esempio seguente:

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
              "status": "realized"
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
>Per tutti i modelli utilizzati, è necessario eseguire l&#39;escape dei caratteri non validi, ad esempio le virgolette doppie `""`, prima di inserire il [modello](../../functionality/destination-server/templating-specs.md) nella [configurazione del server di destinazione](../../authoring-api/destination-server/create-destination-server.md). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 nello standard [JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
                {# Alternative syntax for filtering audiences by status: #}
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

`json` rappresenta i dati esportati da Adobe Experience Platform.

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

Quando si utilizza l&#39;[aggregazione configurabile](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) nella configurazione di destinazione, è possibile raggruppare i profili esportati nella destinazione in base a criteri quali ID pubblico, alias pubblico, appartenenza pubblico o spazi dei nomi di identità.

Nel modello di trasformazione dei messaggi, puoi accedere alle chiavi di aggregazione indicate in precedenza, come mostrato negli esempi nelle sezioni seguenti. Utilizza le chiavi di aggregazione per strutturare il messaggio HTTP esportato da Experience Platform in modo che corrisponda ai limiti di formato e frequenza previsti dalla destinazione.

#### Usa chiave di aggregazione ID pubblico nel modello {#aggregation-key-segment-id}

Se si utilizza l&#39;[aggregazione configurabile](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) e si imposta `includeSegmentId` su true, i profili nei messaggi HTTP esportati nella destinazione vengono raggruppati per ID pubblico. Di seguito trovi le modalità di accesso all’ID del pubblico nel modello.

**Input**

Considera i quattro profili seguenti, dove:

* i primi due fanno parte del pubblico con ID pubblico `788d8874-8007-4253-92b7-ee6b6c20c6f3`
* il terzo profilo fa parte del pubblico con ID pubblico `8f812592-3f06-416b-bd50-e7831848a31a`
* il quarto profilo fa parte di entrambi i tipi di pubblico indicati sopra.

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
            "status":"realized"
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
            "status":"realized"
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
            "status":"realized"
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
            "status":"realized"
         },
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

**Modello**

>[!IMPORTANT]
>
>Per tutti i modelli utilizzati, è necessario eseguire l&#39;escape dei caratteri non validi, ad esempio le virgolette doppie `""`, prima di inserire il [modello](../../functionality/destination-server/templating-specs.md) nella [configurazione del server di destinazione](../../authoring-api/destination-server/create-destination-server.md). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 nello standard [JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Tieni presente che `audienceId` viene utilizzato nel modello per accedere agli ID del pubblico. In questo esempio si presuppone che si utilizzi `audienceId` per l&#39;iscrizione al pubblico nella tassonomia di destinazione. In alternativa, puoi utilizzare qualsiasi altro nome di campo, a seconda della tassonomia.

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

Quando vengono esportati nella destinazione, i profili vengono suddivisi in due gruppi, in base al loro ID pubblico.

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

#### Utilizza la chiave di aggregazione degli alias del pubblico nel modello {#aggregation-key-segment-alias}

Se si utilizza l&#39;[aggregazione configurabile](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) e si imposta `includeSegmentId` su true, è anche possibile accedere all&#39;alias del pubblico nel modello.

Aggiungi la riga seguente al modello per accedere ai profili esportati raggruppati per alias di pubblico.

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### Utilizza la chiave di aggregazione dello stato del pubblico nel modello {#aggregation-key-segment-status}

Se si utilizza [aggregazione configurabile](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) e si impostano `includeSegmentId` e `includeSegmentStatus` su true, è possibile accedere allo stato del pubblico nel modello. In questo modo, puoi raggruppare i profili nei messaggi HTTP esportati nella destinazione in base al fatto che debbano essere aggiunti o rimossi dai segmenti.

I valori possibili sono:

* realizzato
* esistente
* uscita

Aggiungi la riga seguente al modello per aggiungere o rimuovere profili dai segmenti, in base ai valori riportati sopra:

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### Utilizza la chiave di aggregazione dello spazio dei nomi dell’identità nel modello {#aggregation-key-identity}

Di seguito è riportato un esempio in cui l&#39;aggregazione [configurabile](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) nella configurazione di destinazione è impostata per aggregare i profili esportati per spazi dei nomi di identità, nel formato `"namespaces": ["email", "phone"]` e `"namespaces": ["GAID", "IDFA"]`. Per ulteriori informazioni sul raggruppamento, consultare il parametro `groups` nella documentazione relativa alla [creazione della configurazione di destinazione](../../authoring-api/destination-configuration/create-destination-configuration.md).

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
>Per tutti i modelli utilizzati, è necessario eseguire l&#39;escape dei caratteri non validi, ad esempio le virgolette doppie `""`, prima di inserire il [modello](../../functionality/destination-server/templating-specs.md) nella [configurazione del server di destinazione](../../authoring-api/destination-server/create-destination-server.md). Per ulteriori informazioni sull&#39;escape delle virgolette doppie, vedere il Capitolo 9 nello standard [JSON](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

`input.aggregationKey.identityNamespaces` è utilizzato nel modello seguente

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

Il contesto fornito al modello contiene `input` (profili/dati esportati in questa chiamata) e `destination` (dati sulla destinazione a cui Adobe invia i dati, validi per tutti i profili).

La tabella seguente fornisce le descrizioni delle funzioni negli esempi precedenti.

| Funzione | Descrizione | Esempio |
|---------|----------|----------|
| `input.profile` | Il profilo, rappresentato come [JsonNode](https://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). Segue lo schema XDM del partner menzionato più sopra in questa pagina. |
| `hasSegments` | Questa funzione prende una mappa degli ID del pubblico dello spazio dei nomi come parametro. La funzione restituisce `true` se nella mappa è presente almeno un pubblico (indipendentemente dal suo stato) e `false` in caso contrario. Puoi utilizzare questa funzione per decidere se eseguire o meno l’iterazione su una mappa di tipi di pubblico. | `hasSegments(input.profile.segmentMembership)` |
| `destination.namespaceSegmentAliases` | Mappa dagli ID pubblico in uno specifico spazio dei nomi Adobe Experience Platform agli alias pubblico nel sistema del partner. | `destination.namespaceSegmentAliases["ups"]["seg-id-1"]` |
| `destination.namespaceSegmentNames` | Mappa i nomi del pubblico in spazi dei nomi specifici di Adobe Experience Platform ai nomi del pubblico nel sistema del partner. | `destination.namespaceSegmentNames["ups"]["seg-name-1"]` |
| `destination.namespaceSegmentTimestamps` | Restituisce l’ora in cui un pubblico è stato creato, aggiornato o attivato in formato timestamp UNIX. | <ul><li>`destination.namespaceSegmentTimestamps["ups"]["seg-id-1"].createdAt`: restituisce l&#39;ora di creazione del segmento con ID `seg-id-1`, dallo spazio dei nomi `ups`, in formato timestamp UNIX.</li><li>`destination.namespaceSegmentTimestamps["ups"]["seg-id-1"].updatedAt`: restituisce l&#39;ora in cui il pubblico con l&#39;ID `seg-id-1`, dallo spazio dei nomi `ups`, è stato aggiornato, in formato timestamp UNIX.</li><li>`destination.namespaceSegmentTimestamps["ups"]["seg-id-1"].mappingCreatedAt`: restituisce l&#39;ora in cui il pubblico con ID `seg-id-1`, dallo spazio dei nomi `ups`, è stato attivato nella destinazione, in formato timestamp UNIX.</li><li>`destination.namespaceSegmentTimestamps["ups"]["seg-id-1"].mappingUpdatedAt`: restituisce l&#39;ora in cui l&#39;attivazione del pubblico è stata aggiornata sulla destinazione, in formato timestamp UNIX.</li></ul> |
| `addedSegments(mapOfNamespacedSegmentIds)` | Restituisce solo i tipi di pubblico con stato `realized`, in tutti gli spazi dei nomi. | `addedSegments(input.profile.segmentMembership)` |
| `removedSegments(mapOfNamespacedSegmentIds)` | Restituisce solo i tipi di pubblico con stato `exited`, in tutti gli spazi dei nomi. | `removedSegments(input.profile.segmentMembership)` |
| `destination.segmentAliases` | **Obsoleto. Sostituito da`destination.namespaceSegmentAliases`** <br><br> Mappa dagli ID pubblico nello spazio dei nomi Adobe Experience Platform agli alias pubblico nel sistema del partner. | `destination.segmentAliases["seg-id-1"]` |
| `destination.segmentNames` | **Obsoleto. Sostituito da`destination.namespaceSegmentNames`** <br><br> Mappa dai nomi del pubblico nello spazio dei nomi Adobe Experience Platform ai nomi del pubblico nel sistema del partner. | `destination.segmentNames["seg-name-1"]` |
| `destination.segmentTimestamps` | **Obsoleto. Sostituito da`destination.namespaceSegmentTimestamps`** <br><br> Restituisce l&#39;ora in cui un pubblico è stato creato, aggiornato o attivato in formato timestamp UNIX. | <ul><li>`destination.segmentTimestamps["seg-id-1"].createdAt`: restituisce l&#39;ora di creazione del pubblico con l&#39;ID `seg-id-1`, in formato timestamp UNIX.</li><li>`destination.segmentTimestamps["seg-id-1"].updatedAt`: restituisce l&#39;ora in cui il pubblico con l&#39;ID `seg-id-1` è stato aggiornato, in formato timestamp UNIX.</li><li>`destination.segmentTimestamps["seg-id-1"].mappingCreatedAt`: restituisce l&#39;ora in cui il pubblico con l&#39;ID `seg-id-1` è stato attivato nella destinazione, in formato timestamp UNIX.</li><li>`destination.segmentTimestamps["seg-id-1"].mappingUpdatedAt`: restituisce l&#39;ora in cui l&#39;attivazione del pubblico è stata aggiornata sulla destinazione, in formato timestamp UNIX.</li></ul> |

{style="table-layout:auto"}

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come vengono trasformati i dati esportati da Experience Platform. Quindi, leggi le pagine seguenti per approfondire le tue conoscenze sulla creazione di modelli di trasformazione dei messaggi per la tua destinazione:

* [Creare e testare un modello di trasformazione dei messaggi](../../testing-api/streaming-destinations/create-template.md)
* [Operazioni API del modello di rendering](../../testing-api/streaming-destinations/render-template-api.md)
* [Funzioni di trasformazione supportate in Destination SDK](../destination-server/supported-functions.md)

Per ulteriori informazioni sugli altri componenti del server di destinazione, consulta i seguenti articoli:

* [Specifiche del server per le destinazioni create con Destination SDK](server-specs.md)
* [Specifiche di modello](templating-specs.md)
* [Configurazione formattazione file](file-formatting.md)
