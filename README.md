# Loki-openshift-PoC
# 🚀 Implementing Loki in OpenShift using the Loki Operator

## Prerequisites
- **OpenShift Cluster**: Ensure you have an OpenShift cluster up and running.
- **Cluster Admin Access**: You need cluster-admin privileges to install operators.

## Steps to Install Loki Operator

### 1. 🔑 Access OpenShift Web Console:
- Log in to your OpenShift web console.

### 2. 📦 Navigate to OperatorHub:
- In the left-hand menu, click on **Operators** and then **OperatorHub**.

### 3. 🔍 Search for Loki Operator:
- Use the search bar to find the Loki Operator.

### 4. 📥 Install Loki Operator:
- Click on the Loki Operator from the search results.
- Click **Install**.
- Choose **All namespaces on the cluster** for the installation mode.
- Select the **openshift-operators** namespace for the installed namespace.
- Enable operator recommended cluster monitoring on this namespace.
- Choose an Approval Strategy (Automatic or Manual).
- Click **Install**.

### 5. ✅ Verify Installation:
- Go to **Installed Operators** under the Operators menu.
- Ensure the Loki Operator is listed with a status of **Succeeded**.

## Deploying LokiStack

### 1. 📝 Create LokiStack Custom Resource:
- In the OpenShift web console, navigate to **Installed Operators**.
- Click on **Loki Operator**.
- Under the Loki Operator menu, click on **LokiStack**.
- Click **Create LokiStack**.

### 2. ⚙️ Configure LokiStack:
- Define the LokiStack configuration according to your requirements. This includes setting up storage, replication, and other parameters.
- Example configuration:
    ```yaml
    apiVersion: loki.grafana.com/v1
    kind: LokiStack
    metadata:
        name: lokistack-sample
        namespace: openshift-operators
    spec:
        size: 1x.small
        storage:
            type: s3
            s3:
                endpoint: s3.amazonaws.com
                bucketnames: my-loki-bucket
                accesskeyid: <your-access-key-id>
                secretaccesskey: <your-secret-access-key>
    ```
- Adjust the configuration to match your environment and requirements.

### 3. 💾 Apply the Configuration:
- Save the configuration file and apply it using `oc` command:
    ```sh
    oc apply -f lokistack.yaml
    ```

### 4. 🔍 Verify LokiStack Deployment:
- Check the status of the LokiStack deployment:
    ```sh
    oc get lokistack -n openshift-operators
    ```

## Accessing Loki

### 1. 🌐 Access Loki UI:
- Once Loki is deployed, you can access the Loki UI through the OpenShift web console or by exposing the service.

### 2. 📊 Query Logs:
- Use LogQL to query logs stored in Loki.

These steps should help you get Loki up and running in your OpenShift environment using the Loki Operator. If you encounter any issues, feel free to ask for further assistance!
