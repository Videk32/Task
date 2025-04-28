# Development Task

## Koraki izvedbe:

1. Namestil sem Minikube in Docker Desktop.

2. Zagnal sem Minikube z ukazom:
   ```bash
   minikube start --driver=docker
   ```

3. Preveril node z ukazom:
   ```bash
   kubectl get nodes
   ```

4. Deployal sem node in jih preveril z ukazi:
   ```bash
   kubectl apply -f citus-master.yaml
   kubectl apply -f citus-worker1.yaml
   kubectl apply -f citus-worker2.yaml
   kubectl get pods
   ```

5. Povezal sem se v glavni Pod z ukazom:
   ```bash
   kubectl exec -it citus-master -- psql -U postgres
   ```

6. Na koncu sem v PostgreSQL naredil naslednje:

   - Ustvaril bazo `test`:
     ```sql
     CREATE DATABASE test;
     ```

   - Povezal sem se na bazo `test`:
     ```sql
     \c test
     ```

   - Ustvaril tabelo `uporabniki`:
     ```sql
     CREATE TABLE uporabniki (
       id SERIAL PRIMARY KEY,
       ime TEXT,
       priimek TEXT
     );
     ```

   - Nalozil Citus extension:
     ```sql
     CREATE EXTENSION citus;
     ```

   - Shardal tabelo `uporabniki`:
     ```sql
     SELECT create_distributed_table('uporabniki', 'id');
     ```
---