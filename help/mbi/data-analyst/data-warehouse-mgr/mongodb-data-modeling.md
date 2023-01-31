---
title: Modellazione dati MongoDB
description: Scopri come evitare pattern di dati che pongono un problema.
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# [!DNL MongoDB] Modellazione dati

Quando [!DNL MBI] tira dentro [!DNL MongoDB] i dati vengono tradotti in un modello relazionale.

La cattiva notizia: Anche se la maggior parte dei pattern di dati non pone un problema, ce ne sono alcuni che, a causa della traduzione in un modello relazionale, [!DNL MBI] non supporta .

La buona notizia: Tutti questi modelli possono essere evitati.

## Array sottonidificati {#subnested}

Se la tua raccolta si presenta come nell’esempio seguente, [!DNL MBI] replicherà i dati solo nella matrice elementi. I dati della matrice dei sottoelementi non verranno estratti.

```bash
    {
        _id: 0000000000000001
        items: [
            {
                _id: 0000000000000002
               subItems: [
                   {
                       _id: 0000000000000003
                      name: "Donut"
                      description: "glazed"
                   }
               ]
            }
        ]
    }
```

## Tasti oggetto variabili {#varobjectkeys}

Le raccolte che includono oggetti con chiavi di oggetto variabile non vengono replicate in [!DNL MBI]. Ad esempio:

```bash
    {
        _id: 0000000000000001
        friends: {
            0000000000000002: "Jimmy",
            0000000000000004: "Roger",
            0000000000000005: "Susan"
        },
    }
```

Ciò si verifica in genere quando si utilizza un oggetto e una matrice risulta più appropriata. Ora, rielaboreremo l&#39;esempio precedente:

```bash
    {
        _id: 0000000000000001
        friends: [
            { friend_id: 0000000000000002, name: "Jimmy" },
            { friend_id: 0000000000000004, name: "Roger" },
            { friend_id: 0000000000000005, name: "Susan"}
        ]
    }
```
