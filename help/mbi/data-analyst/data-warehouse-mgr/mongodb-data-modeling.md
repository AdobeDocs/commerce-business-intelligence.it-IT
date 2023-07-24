---
title: Modellazione dati MongoDB
description: Scopri come evitare pattern di dati che pongono un problema.
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# [!DNL MongoDB] Modellazione dati

Quando [!DNL Adobe Commerce Intelligence] richiama [!DNL MongoDB] dati, questi dati vengono tradotti in un modello relazionale.

La cattiva notizia: anche se la maggior parte dei pattern di dati non pone alcun problema, ce ne sono alcuni che non sono supportati da [!DNL Commerce Intelligence], a causa della traduzione in un modello relazionale.

La buona notizia: tutti questi modelli possono essere evitati.

## Array subannidati {#subnested}

Se la tua raccolta è simile all’esempio di seguito, [!DNL Commerce Intelligence] replica solo i dati nell&#39;array items. I dati dell’array dei sottoelementi non vengono estratti.

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

## Chiavi oggetto variabili {#varobjectkeys}

Le raccolte che includono oggetti con chiavi di oggetti variabili non vengono replicate in [!DNL Commerce Intelligence]. Ad esempio:

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

Ciò si verifica in genere quando viene utilizzato un oggetto e un array è più appropriato. Ora, rielabora l’esempio precedente:

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
