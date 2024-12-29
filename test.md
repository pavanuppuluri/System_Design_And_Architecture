# Create Partner Code Group (Reward Item Group) Flow

## Step1

Upload file 

**Repo**
https://dev.azure.com/PepsiCoIT/PEPCommerce_Loyalty/_git/dtcloyalty-admin-rewardsadmin-filemanager

**Api Endpoint**
http://localhost:8080/files/upload

**Example**

Parameters
program_id=018a2bd5-fdc2-77ce-9367-7d700186d5ae
partner_id=8834025b-b51d-4669-9973-200f07a9ed54

Body
Key = file 
Type = File
Value = File to be uploaded

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



