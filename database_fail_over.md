# Database Failover Strategies

Database standby modes refer to different levels of redundancy and failover capabilities in database replication setups. 
The three main types are **cold standby**, **warm standby**, and **hot standby**, each offering different trade-offs in terms of recovery time and availability.

**Cold Standby**
---
<img width="825" alt="image" src="https://github.com/user-attachments/assets/d6339988-be37-4386-a7fe-db17e67cddd9" />

**Warm Standby**
---
In this we will use Replication instead of periodic backup. It constantly copies database data from Primary database to Secondary database.
SO instead of having a periodic backup that need to be manuallt restored, we make sure that second database host is always warm (It means it always gets a copy of the data and waiting for the trigger to ready-to-go). 

<img width="640" alt="image" src="https://github.com/user-attachments/assets/f8f766f2-0655-486d-a5fc-e614fecfc806" />

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


