# Create Partner Code Group (Reward Item Group) Flow

## Overview of steps
- Step1 - Upload file
- Step2 - Create Reward Item Group
- Step3 - Publish REWARD_ITEM_GROUP_CREATED.v1 and consume it
- Step4 - Publish REWARD_ITEM_GROUP_DEPLOYED.v1 and consume it


### Step1 - Upload file 

| Repo           | https://dev.azure.com/PepsiCoIT/PEPCommerce_Loyalty/_git/dtcloyalty-admin-rewardsadmin-filemanager |
|--------------------|-----------------------------------------------------------------------------------------------------|
| API Endpoint   | [http://localhost:8080/files/upload](http://localhost:8080/files/upload)                            |
| Example<br>Parameters     | `program_id=018a2bd5-fdc2-77ce-9367-7d700186d5ae`<br>`partner_id=8834025b-b51d-4669-9973-200f07a9ed54` |
| Body           | **Key** = file<br>**Type** = File<br>**Value** = File to be uploaded                                |



**Sample file**

<img width="368" alt="image" src="https://github.com/user-attachments/assets/d4949888-953f-44d5-9fa8-9049aad729b8" />

**Request**

<img width="1262" alt="image" src="https://github.com/user-attachments/assets/fd077ae6-aa36-46dd-9994-be45adbeaca9" />

**API Response**
```
[
    {
        "id": "0947507f-2055-4894-adf6-94713a59d7ca",
        "name": "10_Codes069.txt",
        "size": 170,
        "type": "text/plain",
        "program_id": "018a2bd5-fdc2-77ce-9367-7d700186d5ae",
        "partner_id": "8834025b-b51d-4669-9973-200f07a9ed54",
        "metadata": {
            "description": "SAVED FILE 8834025b-b51d-4669-9973-200f07a9ed54/10_Codes069.txt",
            "container_name": "kaz",
            "tags": [
                "UploadDate=2024-12-29",
                "ProgramId=018a2bd5-fdc2-77ce-9367-7d700186d5ae",
                "PartnerId=8834025b-b51d-4669-9973-200f07a9ed54",
                "FileName=8834025b-b51d-4669-9973-200f07a9ed54/10_Codes069.txt"
            ],
            "uploaded_by": "SYSTEM",
            "uploaded_at": "2024-12-29 10:38:17"
        }
    }
]
```

### Step2 - Create Reward Item Group

| Repo           | https://dev.azure.com/PepsiCoIT/PEPCommerce_Loyalty/_git/dtcloyalty-admin-rewardsadmin-rewardsmanager |
|--------------------|-----------------------------------------------------------------------------------------------------|
| API Endpoint   | http://localhost:8080/reward-item-groups                            |


**Sample Request Body**
```
{
    "name": "KZrewarditemgroup145",
    "description": "KZrewarditemgroup145",
    "program_id": "018a2bd5-fdc2-77ce-9367-7d700186d5ae",
    "partner_id": "8834025b-b51d-4669-9973-200f07a9ed54",
    "code_warning_limit_percentage": 80,
    "reward_item_file_data": [
        {
            "id": "5de33ce2-1919-445e-afda-78c28ecbcab8",
            "name": "10_Codes069.txt",
            "size": 170,
            "type": "text/plain",
            "program_id": "018a2bd5-fdc2-77ce-9367-7d700186d5ae",
            "partner_id": "8834025b-b51d-4669-9973-200f07a9ed54",
            "metadata": {
                "description": "SAVED FILE 8834025b-b51d-4669-9973-200f07a9ed54/10_Codes06.txt",
                "container_name": "kaz",
                "tags": [
                    "UploadDate=2024-12-27",
                    "FileName=8834025b-b51d-4669-9973-200f07a9ed54/10_Codes06.txt",
                    "ProgramId=018a2bd5-fdc2-77ce-9367-7d700186d5ae",
                    "PartnerId=8834025b-b51d-4669-9973-200f07a9ed54"
                ],
                "uploaded_by": "SYSTEM",
                "uploaded_at": "2024-12-27 23:15:33"
            }
        }
    ],
    "is_active": true,
    "start_date": "2024-10-28T08:03:18",
    "end_date": "2025-07-12T08:03:18"
}
```

**API Response**
```
{
    "reward_item_file_data": [
        {
            "name": "10_Codes069.txt",
            "size": 170,
            "reward_item_group_id": "d475ae59-66a4-489e-82dc-7efc1b3dc877",
            "metadata_id": "2fd2ce3a-d0f4-4140-812b-eff226b29b3b",
            "metadata": {
                "tags": [
                    "UploadDate=2024-12-27",
                    "FileName=8834025b-b51d-4669-9973-200f07a9ed54/10_Codes06.txt",
                    "ProgramId=018a2bd5-fdc2-77ce-9367-7d700186d5ae",
                    "PartnerId=8834025b-b51d-4669-9973-200f07a9ed54"
                ],
                "container_name": "kaz",
                "uploaded_by": "SYSTEM",
                "uploaded_at": "2024-12-27 23:15:33",
                "description": "SAVED FILE 8834025b-b51d-4669-9973-200f07a9ed54/10_Codes06.txt",
                "id": "2fd2ce3a-d0f4-4140-812b-eff226b29b3b"
            },
            "id": "b75c4af3-8e77-4f0d-bbfa-cd14f55e9c81"
        }
    ],
    "name": "KZrewarditemgroup145",
    "description": "KZrewarditemgroup145",
    "partner_id": "8834025b-b51d-4669-9973-200f07a9ed54",
    "program_id": "018a2bd5-fdc2-77ce-9367-7d700186d5ae",
    "code_warning_limit_percentage": 80,
    "is_active": true,
    "exhausted_code": 0,
    "code_count": 0,
    "is_imported": false,
    "start_date": "2024-10-28T08:03:18",
    "end_date": "2025-07-12T08:03:18",
    "id": "d475ae59-66a4-489e-82dc-7efc1b3dc877",
    "status": "INACTIVE",
    "processing_status": "IMPORTING"
}
```

<img width="1223" alt="image" src="https://github.com/user-attachments/assets/b2ce633c-1f87-4de0-8c7f-0cd7f514fca9" />


### Step3 - Publish REWARD_ITEM_GROUP_CREATED.v1 and consume it

Run below repo locally to consume an event

**Repo**
https://dev.azure.com/PepsiCoIT/PEPCommerce_Loyalty/_git/dtcloyalty-runtime-consumerrewards-deployment-service

Raise com.pepsico.dtcloyalty.configurationnadmin.REWARD_ITEM_GROUP_CREATED.v1

**How to do it?**
- Login to
  https://portal.azure.com/#@pepsico.onmicrosoft.com/resource/subscriptions/8a22bd18-1080-472c-a8af-da15be88b076/resourceGroups/pep-dop-nonprod-gwc-01-rg/providers/Microsoft.ServiceBus/namespaces/pep-cep-kz-gwc-dev/topics/dtc-loyalty-sb-consumerrewards-outbound/subscriptions/loyalty-dtcloyalty-rewards-test/explorer
- Send New Message

**Sample Payload**

```
{
    "specversion": "1.0",
    "id": "ao1026e003a-a103ca-a33da-b1130b-0d8a27ba35a106",
    "source": "com.pepsico.dtcloyalty.adminrewarditemgroup",
    "type": "com.pepsico.dtcloyalty.configurationnadmin.REWARD_ITEM_GROUP_CREATED.v1",
    "datacontenttype": "application/json",
    "dataschema": "",
    "time": "2024-11-30T11:24:59.7377393Z",
    "messagepublishingscope": "DOMAIN_EXTERNAL",
    "data": {
        "reward_item_file_data": [
            {
                "name": "10_Codes06.txt",
                "size": 170,
                "type": "text/plain",
                "metadata_id": "bd918371-9665-4194-88c7-ee42d09929f9",
                "reward_item_group_id": "6080bcf1-f4fb-429e-9234-0e8a9090549b",
                "metadata": {
                    "tags": [
                        "UploadDate=2024-12-27",
                        "FileName=8834025b-b51d-4669-9973-200f07a9ed54/10_Codes06.txt",
                        "ProgramId=018a2bd5-fdc2-77ce-9367-7d700186d5ae",
                        "PartnerId=8834025b-b51d-4669-9973-200f07a9ed54"
                    ],
                    "container_name": "kaz",
                    "uploaded_by": "SYSTEM",
                    "uploaded_at": "2024-12-27 23:15:33",
                    "description": "SAVED FILE 8834025b-b51d-4669-9973-200f07a9ed54/10_Codes06.txt",
                    "id": "bd918371-9665-4194-88c7-ee42d09929f9"
                },
                "id": "f39a4f5f-ace7-4bcc-a691-a03708d67d3f"
            }
        ],
        "name": "KZrewarditemgroup141",
        "description": "KZrewarditemgroup141",
        "partner_id": "8834025b-b51d-4669-9973-200f07a9ed54",
        "program_id": "018a2bd5-fdc2-77ce-9367-7d700186d5ae",
        "code_warning_limit_percentage": 80,
        "is_active": true,
        "exhausted_code": 0,
        "code_count": 0,
        "is_imported": false,
        "start_date": "2024-10-28T08:03:18",
        "end_date": "2025-07-12T08:03:18",
        "id": "6080bcf1-f4fb-429e-9234-0e8a9090549b",
        "status": "INACTIVE",
        "processing_status": "IMPORTING"
    }
}
```

Message type = application/json
Along with the payload give Session Id as 1234

Now submitting this event message should be consumed by our local running deployment service

### Step4 - Publish REWARD_ITEM_GROUP_DEPLOYED.v1 and consume it

Run below repo locally to consume an event

**Repo**
https://dev.azure.com/PepsiCoIT/PEPCommerce_Loyalty/_git/dtcloyalty-admin-rewardsadmin-rewarditemprocessor

Raise com.pepsico.dtcloyalty.consumerrewards.REWARD_ITEM_GROUP_DEPLOYED.v1

**How to do it?**
- Login to
  https://portal.azure.com/#@pepsico.onmicrosoft.com/resource/subscriptions/8a22bd18-1080-472c-a8af-da15be88b076/resourceGroups/pep-dop-nonprod-gwc-01-rg/providers/Microsoft.ServiceBus/namespaces/pep-cep-kz-gwc-dev/topics/dtc-loyalty-sb-consumerrewards-outbound/subscriptions/loyalty-dtcloyalty-rewards-test/explorer
- Send New Message

**Sample Payload**

```
{
    "specversion": "1.0",
    "id": "ao1026e003a-a103ca-a33da-b1130b-0d8a27ba35a106",
    "source": "com.pepsico.dtcloyalty.adminrewarditemgroup",
    "type": "com.pepsico.dtcloyalty.consumerrewards.REWARD_ITEM_GROUP_DEPLOYED.v1",
    "datacontenttype": "application/json",
    "dataschema": "",
    "time": "2024-11-30T11:24:59.7377393Z",
    "messagepublishingscope": "DOMAIN_EXTERNAL",
    "data": {
        "reward_item_file_data": [
            {
                "name": "10_Codes06.txt",
                "size": 170,
                "type": "text/plain",
                "meta_data_id": "bd918371-9665-4194-88c7-ee42d09929f9",
                "reward_item_group_id": "6080bcf1-f4fb-429e-9234-0e8a9090549b",
                "metadata": {
                    "tags": [
                        "UploadDate=2024-12-27",
                        "FileName=8834025b-b51d-4669-9973-200f07a9ed54/10_Codes06.txt",
                        "ProgramId=018a2bd5-fdc2-77ce-9367-7d700186d5ae",
                        "PartnerId=8834025b-b51d-4669-9973-200f07a9ed54"
                    ],
                    "container_name": "kaz",
                    "uploaded_by": "SYSTEM",
                    "uploaded_at": "2024-12-27 23:15:33",
                    "description": "SAVED FILE 8834025b-b51d-4669-9973-200f07a9ed54/10_Codes06.txt",
                    "id": "bd918371-9665-4194-88c7-ee42d09929f9"
                },
                "id": "f39a4f5f-ace7-4bcc-a691-a03708d67d3f"
            }
        ],
        "name": "KZrewarditemgroup141",
        "description": "KZrewarditemgroup141",
        "partner_id": "8834025b-b51d-4669-9973-200f07a9ed54",
        "program_id": "018a2bd5-fdc2-77ce-9367-7d700186d5ae",
        "code_warning_limit_percentage": 80,
        "is_active": true,
        "exhausted_code": 0,
        "code_count": 0,
        "is_imported": false,
        "start_date": "2024-10-28T08:03:18",
        "end_date": "2025-07-12T08:03:18",
        "id": "6080bcf1-f4fb-429e-9234-0e8a9090549b",
        "status": "INACTIVE",
        "processing_status": "IMPORTING"
    }
}
```

Message type = application/json
Along with the payload give Session Id as 1234

Now submitting this event message should be consumed by our local running rewarditemprocessor service


## Trouble shooting tips

| Issue                                      | Solution                                                                                           |
|--------------------------------------------|----------------------------------------------------------------------------------------------------|
| **Error while downloading file in Step4**  | Download the certificate of the blob storage URL and install it locally.   <br><br> Command Example <br><br> ```keytool -import -trustcacerts -keystore "/Users/pavanu/Library/Java/JavaVirtualMachines/openjdk-23/Contents/Home/lib/security/cacerts" -storepass changeit -alias rewardadminfilemanagerCert -file "/Users/kavyasrutiputrevu/Downloads/_.global.gw01.aks01.gwc.nonprod.azure.intra.pepsico.com.pem"```                       |
| **Event publishing may be failing**       | Ensure to provide a unique ID in the event payload.                                                |







