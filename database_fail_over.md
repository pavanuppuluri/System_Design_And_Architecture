# Database Failover Strategies

Database standby modes refer to different levels of redundancy and failover capabilities in database replication setups. 
The three main types are **cold standby**, **warm standby**, and **hot standby**, each offering different trade-offs in terms of recovery time and availability.

**Cold Standby**
---

Cold Standby is a disaster recovery strategy where a backup system (server or database) remains powered off or inactive until needed. It is only started and restored manually when the primary system fails.

<img width="668" alt="image" src="https://github.com/user-attachments/assets/f305315b-4afe-4f65-961b-dccae99b438d" />

<br>

<img width="404" alt="image" src="https://github.com/user-attachments/assets/77fb7fcb-4575-468c-9117-c7492054f37d" />

**Warm Standby**
---
In this we will use Replication instead of periodic backup. It constantly copies database data from Primary database to Secondary database.
SO instead of having a periodic backup that need to be manuallt restored, we make sure that second database host is always warm (It means it always gets a copy of the data and waiting for the trigger to ready-to-go). 

<img width="311" alt="image" src="https://github.com/user-attachments/assets/d7f3d114-7946-4a0c-8ce1-9d442249d0f9" />


In a Warm Standby approach, replication is used to keep the standby database updated periodically. Unlike Hot Standby (which is real-time), Warm Standby relies on delayed or batch-based replication methods. Here are the key replication techniques used in Warm Standby:

<img width="661" alt="image" src="https://github.com/user-attachments/assets/06aa761f-f28c-40df-92f9-0ef942d99ca8" />

<img width="641" alt="image" src="https://github.com/user-attachments/assets/04db6844-5ed6-4d2a-ac51-e3110ab1e3ad" />

<img width="497" alt="image" src="https://github.com/user-attachments/assets/934a0471-989f-4e50-b9d2-9460acc52598" />

<img width="585" alt="image" src="https://github.com/user-attachments/assets/b62b37c1-1d5c-4cef-be3d-a2892a16afeb" />

<br>
<br>

**Comparison**

| Replication Type          | Update Frequency       | Data Loss Risk  | Use Case                               |
|---------------------------|-----------------------|----------------|----------------------------------------|
| **Log Shipping**          | Periodic (Log-based)  | Low (depends on log interval) | Disaster Recovery                     |
| **Delayed Replication**   | Time-Delayed         | Low (allows rollback) | Protection from accidental changes    |
| **Snapshot Replication**  | Batch (Snapshot-based) | Moderate (until next snapshot) | Large datasets, periodic sync       |
| **Asynchronous Replication** | Near Real-Time     | Moderate (risk of lag) | Lower overhead, distributed databases |


**Hot Standby**
---

<img width="387" alt="image" src="https://github.com/user-attachments/assets/f643e7fa-5a27-4844-b737-ade966947ab5" />

**Hot Standby** is a high-availability database replication strategy where a standby (backup) database **continuously synchronizes with the primary database in real-time**. The standby server is always running and can take over immediately if the primary database fails.

<img width="658" alt="image" src="https://github.com/user-attachments/assets/e5bfe8eb-b633-4623-8dae-d410c7a627ef" />

<img width="671" alt="image" src="https://github.com/user-attachments/assets/7c16bcb4-d5b1-47f6-97cd-a34af29d3622" />

<img width="668" alt="image" src="https://github.com/user-attachments/assets/d5f55ceb-e48e-4a6c-863c-2c229b2b1f5f" />

---
#### Example Implementations
---
| Standby Type  | Database Example  | Implementation Method |
|--------------|------------------|----------------------|
| **Cold Standby**  | **PostgreSQL**  | `pg_dump` for full backups, `pg_restore` for recovery |
|                  | **MySQL**        | `mysqldump` for full backups, `mysqlbinlog` for incremental backups |
|                  | **SQL Server**   | `BACKUP DATABASE` and `RESTORE DATABASE` commands |
|                  | **Oracle**       | **Oracle RMAN (Recovery Manager)** for cold backups |
| **Warm Standby**  | **PostgreSQL**  | **PostgreSQL Log Shipping** (`WAL archiving` with manual recovery) |
|                  | **MySQL**        | **MySQL Delayed Replication** (`MASTER_DELAY` option) |
|                  | **SQL Server**   | **SQL Server Log Shipping** (`BACKUP LOG`, `RESTORE LOG`) |
|                  | **Oracle**       | **Oracle Data Guard** in **Maximum Performance mode** |
| **Hot Standby**  | **PostgreSQL**  | **PostgreSQL Streaming Replication** (`hot_standby`, `primary_conninfo`) |
|                  | **MySQL**        | **MySQL Group Replication**, **Percona XtraDB Cluster**, or **InnoDB Cluster** |
|                  | **SQL Server**   | **SQL Server Always On Availability Groups** |
|                  | **Oracle**       | **Oracle Data Guard (Maximum Availability mode)** or **Oracle RAC** |





