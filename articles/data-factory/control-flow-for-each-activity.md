---
title: Działanie ForEach w usłudze Azure Data Factory | Dokumentacja firmy Microsoft
description: Dla każdego działania definiuje powtarzający się przepływ sterowania w potoku. Jest on używany do wykonania iteracji przez kolekcję i wykonać określone działania.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: conceptual
ms.date: 11/26/2018
ms.author: shlo
ms.openlocfilehash: 90c36e728a8ec91606f93c080258eeca9c3825e6
ms.sourcegitcommit: 25936232821e1e5a88843136044eb71e28911928
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/04/2019
ms.locfileid: "54020782"
---
# <a name="foreach-activity-in-azure-data-factory"></a>Działanie ForEach w usłudze Azure Data Factory
Działanie ForEach definiuje powtarzający się przepływ sterowania w potoku. To działanie służy do wykonywania iteracji po kolekcji i wykonuje określone działania w pętli. Implementacja pętli tego działania przypomina strukturę pętli Foreach w językach programowania.

## <a name="syntax"></a>Składnia
Właściwości są opisane w dalszej części tego artykułu. Właściwość items jest kolekcji, a każdy element w kolekcji jest określana za pomocą `@item()` jak pokazano na następującej składni:  

```json
{  
   "name":"MyForEachActivityName",
   "type":"ForEach",
   "typeProperties":{  
      "isSequential":"true",
        "items": {
            "value": "@pipeline().parameters.mySinkDatasetFolderPathCollection",
            "type": "Expression"
        },
      "activities":[  
         {  
            "name":"MyCopyActivity",
            "type":"Copy",
            "typeProperties":{  
               ...
            },
            "inputs":[  
               {  
                  "referenceName":"MyDataset",
                  "type":"DatasetReference",
                  "parameters":{  
                     "MyFolderPath":"@pipeline().parameters.mySourceDatasetFolderPath"
                  }
               }
            ],
            "outputs":[  
               {  
                  "referenceName":"MyDataset",
                  "type":"DatasetReference",
                  "parameters":{  
                     "MyFolderPath":"@item()"
                  }
               }
            ]
         }
      ]
   }
}

```

## <a name="type-properties"></a>Właściwości typu

Właściwość | Opis | Dozwolone wartości | Wymagane
-------- | ----------- | -------------- | --------
name | Nazwa dla każdego działania. | Ciąg | Yes
type | Musi być równa **ForEach** | Ciąg | Yes
isSequential | Określa, czy pętla powinny być wykonywane kolejno lub równolegle.  Maksymalna liczba iteracji pętli 20 mogą być wykonywane jednocześnie równolegle). Na przykład, jeśli masz ForEach działania Iterowanie działania kopiowania przy użyciu 10 różnych danych źródła i ujścia przy użyciu **isSequential** ma wartość False, wszystkie kopie są wykonywane tylko raz. Domyślną jest False. <br/><br/> Jeśli "isSequential" jest ustawiona na "false", upewnij się, że jest poprawną konfigurację do uruchamiania wielu aplikacji wykonywalnych. W przeciwnym razie tej właściwości należy używać ostrożnie w celu uniknięcia konfliktów przy zapisywaniu. Aby uzyskać więcej informacji, zobacz [równoległym](#parallel-execution) sekcji. | Wartość logiczna | Nie. Domyślną jest False.
batchCount | Liczba partii, która ma być używany do kontrolowania liczby przetwarzania równoległego, (gdy isSequential jest ustawiona na wartość false). | Liczba całkowita (maksymalna 50) | Nie. Domyślna to 20.
Items | Wyrażenie, które zwraca tablicę JSON, aby być powtarzana. | Wyrażenie (która zwraca tablicę JSON) | Yes
Działania | Czynności do wykonania. | Lista działań | Yes

## <a name="parallel-execution"></a>Wykonywanie równoległe
Jeśli **isSequential** jest ustawiona na wartość false, działanie iteruje równolegle z maksymalnie 20 równoczesnych iteracji. Tego ustawienia należy używać ostrożnie. Współbieżne iteracji pisania w tym samym folderze, ale do różnych plików, to podejście jest odpowiednie. Współbieżne iteracji pisania jednocześnie dokładnie tego samego pliku, to podejście najprawdopodobniej spowoduje wystąpienie błędu. 

## <a name="iteration-expression-language"></a>Język wyrażeń iteracji
Działanie ForEach zawiera tablicę, należy powtórzyć za pośrednictwem właściwości **elementy**. " Użyj `@item()` Iterowanie pojedynczego wyliczenia w działaniu ForEach. Na przykład jeśli **elementów** jest tablicą: [1, 2, 3], `@item()` zwraca wartość 1 w pierwszej iteracji 2 w drugim i 3 w trzecim iteracji.

## <a name="iterating-over-a-single-activity"></a>Iterowanie po pojedyncze działanie
**Scenariusz:** Skopiuj z tym samym pliku źródłowym w usłudze Azure Blob do wielu plików docelowych w usłudze Azure Blob.

### <a name="pipeline-definition"></a>Definicji potoku

```json
{
    "name": "<MyForEachPipeline>",
    "properties": {
        "activities": [
            {
                "name": "<MyForEachActivity>",
                "type": "ForEach",
                "typeProperties": {
                    "isSequential": "true",
                    "items": {
                        "value": "@pipeline().parameters.mySinkDatasetFolderPath",
                        "type": "Expression"
                    },
                    "activities": [
                        {
                            "name": "MyCopyActivity",
                            "type": "Copy",
                            "typeProperties": {
                                "source": {
                                    "type": "BlobSource",
                                    "recursive": "false"
                                },
                                "sink": {
                                    "type": "BlobSink",
                                    "copyBehavior": "PreserveHierarchy"
                                }
                            },
                            "inputs": [
                                {
                                    "referenceName": "<MyDataset>",
                                    "type": "DatasetReference",
                                    "parameters": {
                                        "MyFolderPath": "@pipeline().parameters.mySourceDatasetFolderPath"
                                    }
                                }
                            ],
                            "outputs": [
                                {
                                    "referenceName": "MyDataset",
                                    "type": "DatasetReference",
                                    "parameters": {
                                        "MyFolderPath": "@item()"
                                    }
                                }
                            ]
                        }
                    ]
                }
            }
        ],
        "parameters": {
            "mySourceDatasetFolderPath": {
                "type": "String"
            },
            "mySinkDatasetFolderPath": {
                "type": "String"
            }
        }
    }
}

```

### <a name="blob-dataset-definition"></a>Definicja zestawu danych obiektów blob

```json
{  
   "name":"<MyDataset>",
   "properties":{  
      "type":"AzureBlob",
      "typeProperties":{  
         "folderPath":{  
            "value":"@dataset().MyFolderPath",
            "type":"Expression"
         }
      },
      "linkedServiceName":{  
         "referenceName":"StorageLinkedService",
         "type":"LinkedServiceReference"
      },
      "parameters":{  
         "MyFolderPath":{  
            "type":"String"
         }
      }
   }
}

```

### <a name="run-parameter-values"></a>Uruchom wartości parametrów

```json
{
    "mySourceDatasetFolderPath": "input/",
    "mySinkDatasetFolderPath": [ "outputs/file1", "outputs/file2" ]
}

```

## <a name="iterate-over-multiple-activities"></a>Iteracja wielu działań
Istnieje możliwość przejść przez wiele działań (na przykład: działania kopiowania i sieci web) w działaniu ForEach. W tym scenariuszu firma Microsoft zaleca abstrakcji się z się z wielu działań do oddzielnych potoku. Następnie należy użyć [działaniu ExecutePipeline](control-flow-execute-pipeline-activity.md) w potoku za pomocą działania ForEach wywoływanie oddzielne potoku obejmujący wiele działań. 


### <a name="syntax"></a>Składnia

```json
{
  "name": "masterPipeline",
  "properties": {
    "activities": [
      {
        "type": "ForEach",
        "name": "<MyForEachMultipleActivities>"
        "typeProperties": {
          "isSequential": true,
          "items": {
            ...
          },
          "activities": [
            {
              "type": "ExecutePipeline",
              "name": "<MyInnerPipeline>"
              "typeProperties": {
                "pipeline": {
                  "referenceName": "<copyHttpPipeline>",
                  "type": "PipelineReference"
                },
                "parameters": {
                  ...
                },
                "waitOnCompletion": true
              }
            }
          ]
        }
      }
    ],
    "parameters": {
      ...
    }
  }
}

```
### <a name="example"></a>Przykład
**Scenariusz:** Iteracja InnerPipeline wewnątrz działania ForEach, za pomocą działania Execute Pipeline. Wewnętrzny potok kopiuje przy użyciu definicji schematów sparametryzowanych.

#### <a name="master-pipeline-definition"></a>Definicję wzorca potoku

```json
{
  "name": "masterPipeline",
  "properties": {
    "activities": [
      {
        "type": "ForEach",
        "name": "MyForEachActivity",
        "typeProperties": {
          "isSequential": true,
          "items": {
            "value": "@pipeline().parameters.inputtables",
            "type": "Expression"
          },
          "activities": [
            {
              "type": "ExecutePipeline",
              "typeProperties": {
                "pipeline": {
                  "referenceName": "InnerCopyPipeline",
                  "type": "PipelineReference"
                },
                "parameters": {
                  "sourceTableName": {
                    "value": "@item().SourceTable",
                    "type": "Expression"
                  },
                  "sourceTableStructure": {
                    "value": "@item().SourceTableStructure",
                    "type": "Expression"
                  },
                  "sinkTableName": {
                    "value": "@item().DestTable",
                    "type": "Expression"
                  },
                  "sinkTableStructure": {
                    "value": "@item().DestTableStructure",
                    "type": "Expression"
                  }
                },
                "waitOnCompletion": true
              },
              "name": "ExecuteCopyPipeline"
            }
          ]
        }
      }
    ],
    "parameters": {
      "inputtables": {
        "type": "Array"
      }
    }
  }
}

```

#### <a name="inner-pipeline-definition"></a>Definicji potoku wewnętrzny

```json
{
  "name": "InnerCopyPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            }
          },
          "sink": {
            "type": "SqlSink"
          }
        },
        "name": "CopyActivity",
        "inputs": [
          {
            "referenceName": "sqlSourceDataset",
            "parameters": {
              "SqlTableName": {
                "value": "@pipeline().parameters.sourceTableName",
                "type": "Expression"
              },
              "SqlTableStructure": {
                "value": "@pipeline().parameters.sourceTableStructure",
                "type": "Expression"
              }
            },
            "type": "DatasetReference"
          }
        ],
        "outputs": [
          {
            "referenceName": "sqlSinkDataset",
            "parameters": {
              "SqlTableName": {
                "value": "@pipeline().parameters.sinkTableName",
                "type": "Expression"
              },
              "SqlTableStructure": {
                "value": "@pipeline().parameters.sinkTableStructure",
                "type": "Expression"
              }
            },
            "type": "DatasetReference"
          }
        ]
      }
    ],
    "parameters": {
      "sourceTableName": {
        "type": "String"
      },
      "sourceTableStructure": {
        "type": "String"
      },
      "sinkTableName": {
        "type": "String"
      },
      "sinkTableStructure": {
        "type": "String"
      }
    }
  }
}

```

#### <a name="source-dataset-definition"></a>Definicja zestawu danych źródłowych

```json
{
  "name": "sqlSourceDataset",
  "properties": {
    "type": "SqlServerTable",
    "typeProperties": {
      "tableName": {
        "value": "@dataset().SqlTableName",
        "type": "Expression"
      }
    },
    "structure": {
      "value": "@dataset().SqlTableStructure",
      "type": "Expression"
    },
    "linkedServiceName": {
      "referenceName": "sqlserverLS",
      "type": "LinkedServiceReference"
    },
    "parameters": {
      "SqlTableName": {
        "type": "String"
      },
      "SqlTableStructure": {
        "type": "String"
      }
    }
  }
}

```

#### <a name="sink-dataset-definition"></a>Definicja zestawu danych ujścia

```json
{
  "name": "sqlSinkDataSet",
  "properties": {
    "type": "AzureSqlTable",
    "typeProperties": {
      "tableName": {
        "value": "@dataset().SqlTableName",
        "type": "Expression"
      }
    },
    "structure": {
      "value": "@dataset().SqlTableStructure",
      "type": "Expression"
    },
    "linkedServiceName": {
      "referenceName": "azureSqlLS",
      "type": "LinkedServiceReference"
    },
    "parameters": {
      "SqlTableName": {
        "type": "String"
      },
      "SqlTableStructure": {
        "type": "String"
      }
    }
  }
}

```

#### <a name="master-pipeline-parameters"></a>Parametry potoku głównego
```json
{
    "inputtables": [
        {
            "SourceTable": "department",
            "SourceTableStructure": [
              {
                "name": "departmentid",
                "type": "int"
              },
              {
                "name": "departmentname",
                "type": "string"
              }
            ],
            "DestTable": "department2",
            "DestTableStructure": [
              {
                "name": "departmentid",
                "type": "int"
              },
              {
                "name": "departmentname",
                "type": "string"
              }
            ]
        }
    ]
    
}

```
## <a name="aggregating-metric-output"></a>Metryki agregacji w danych wyjściowych
Wyrażenie do zbierania danych wyjściowych wszystkim iteracjom pętli ForEach jest `@activity('NameofInnerActivity')`. Na przykład, jeśli działanie ForEach powtarzana "MyCopyActivity", składnia będzie: `@activity('MyCopyActivity')`. Dane wyjściowe jest tablicą, z każdym elementem, zapewniając szczegółowe informacje o określonej iteracji.

> [!NOTE]
> Jeśli chcesz, aby uzyskać szczegółowe informacje o określonej iteracji, składnia to: `@activity('NameofInnerActivity')[0]` najnowsze iteracji. Umożliwia liczba w nawiasach dostęp do określonej iteracji tablicy. Aby uzyskać dostęp do konkretnej właściwości określonej iteracji, należy użyć: `@activity('NameofInnerActivity')[0].output` lub `@activity('NameofInnerActivity')[0].pipelineName`.

**Szczegóły danych wyjściowych macierz wszystkich iteracji:**
```json
[    
    {      
        "pipelineName": "db1f7d2b-dbbd-4ea8-964e-0d9b2d3fe676",      
        "jobId": "a43766cb-ba13-4c68-923a-8349af9a76a3",      
        "activityRunId": "217526fa-0218-42f1-b85c-e0b4f7b170ce",      
        "linkedServiceName": "ADFService",      
        "status": "Succeeded",      
        "statusCode": null,      
        "output": 
            {        
                "progress": 100,        
                "loguri": null,        
                "dataRead": "6.00 Bytes",        
                "dataWritten": "6.00 Bytes",        
                "regionOrGateway": "West US",        
                "details": "Data Read: 6.00 Bytes, Written: 6.00 Bytes",        
                "copyDuration": "00:00:05",        
                "dataVolume": "6.00 Bytes",        
                "throughput": "1.16 Bytes/s",       
                 "totalDuration": "00:00:10"      
            },      
        "resumptionToken": 
            {       
                "ExecutionId": "217526fa-0218-42f1-b85c-e0b4f7b170ce",        
                "ResumptionToken": 
                    {          
                        "in progress": "217526fa-0218-42f1-b85c-e0b4f7b170ce/wu/cloud/"       
                    },        
                "ExtendedProperties": 
                    {          
                        "dataRead": "6.00 Bytes",          
                        "dataWritten": "6.00 Bytes",          
                        "regionOrGateway": "West US",          
                        "details": "Data Read: 6.00 Bytes, Written: 6.00 Bytes",          
                        "copyDuration": "00:00:05",          
                        "dataVolume": "6.00 Bytes",          
                        "throughput": "1.16 Bytes/s",          
                        "totalDuration": "00:00:10"        
                    }      
            },      
        "error": null,      
        "executionStartTime": "2017-08-01T04:17:27.5747275Z",      
        "executionEndTime": "2017-08-01T04:17:46.4224091Z",     
        "duration": "00:00:18.8476816"    
    },
    {      
        "pipelineName": "db1f7d2b-dbbd-4ea8-964e-0d9b2d3fe676",      
        "jobId": "54232-ba13-4c68-923a-8349af9a76a3",      
        "activityRunId": "217526fa-0218-42f1-b85c-e0b4f7b170ce",      
        "linkedServiceName": "ADFService",      
        "status": "Succeeded",      
        "statusCode": null,      
        "output": 
            {        
                "progress": 100,        
                "loguri": null,        
                "dataRead": "6.00 Bytes",        
                "dataWritten": "6.00 Bytes",        
                "regionOrGateway": "West US",        
                "details": "Data Read: 6.00 Bytes, Written: 6.00 Bytes",        
                "copyDuration": "00:00:05",        
                "dataVolume": "6.00 Bytes",        
                "throughput": "1.16 Bytes/s",       
                 "totalDuration": "00:00:10"      
            },      
        "resumptionToken": 
            {       
                "ExecutionId": "217526fa-0218-42f1-b85c-e0b4f7b170ce",        
                "ResumptionToken": 
                    {          
                        "in progress": "217526fa-0218-42f1-b85c-e0b4f7b170ce/wu/cloud/"       
                    },        
                "ExtendedProperties": 
                    {          
                        "dataRead": "6.00 Bytes",          
                        "dataWritten": "6.00 Bytes",          
                        "regionOrGateway": "West US",          
                        "details": "Data Read: 6.00 Bytes, Written: 6.00 Bytes",          
                        "copyDuration": "00:00:05",          
                        "dataVolume": "6.00 Bytes",          
                        "throughput": "1.16 Bytes/s",          
                        "totalDuration": "00:00:10"        
                    }      
            },      
        "error": null,      
        "executionStartTime": "2017-08-01T04:18:27.5747275Z",      
        "executionEndTime": "2017-08-01T04:18:46.4224091Z",     
        "duration": "00:00:18.8476816"    
    }
]

```

## <a name="limitations-and-workarounds"></a>Ograniczenia i rozwiązania

Poniżej przedstawiono niektóre ograniczenia działanie ForEach i sugerowane rozwiązania problemu.

| Ograniczenia | Obejście |
|---|---|
| Nie można zagnieździć wewnątrz innej pętli ForEach pętla ForEach (lub pętlą Until). | Zaprojektuj potoku dwupoziomowej, gdzie zewnętrzne potoku za pomocą zewnętrzna pętla ForEach iteruje przez wewnętrzny potoku za pomocą zagnieżdżonej pętli. |
| Działanie ForEach może zawierać maksymalnie `batchCount` 50 do równoległego przetwarzania i maksymalnie 100 000 elementów. | Zaprojektuj potoku dwupoziomowej, gdzie zewnętrzne potoku za pomocą działania ForEach iteruje przez wewnętrzny potoku. |
| | |

## <a name="next-steps"></a>Kolejne kroki
Zobacz inne działania przepływu sterowania obsługiwanych przez usługę Data Factory: 

- [Działanie Execute Pipeline](control-flow-execute-pipeline-activity.md)
- [Działanie GetMetadata](control-flow-get-metadata-activity.md)
- [Działanie Lookup](control-flow-lookup-activity.md)
- [Działanie internetowe](control-flow-web-activity.md)
