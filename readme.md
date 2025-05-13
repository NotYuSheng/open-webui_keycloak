# Keycloak Installation with Helm

This guide provides instructions for installing and accessing Keycloak using Helm.

## Prerequisites

Ensure you have the following installed:
- [Helm](https://helm.sh/docs/intro/install/)
- [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)

## Installation Steps

1. **Add the Bitnami Helm repository:**

    ```bash
    helm repo add bitnami https://charts.bitnami.com/bitnami
    ```

2. **Update your Helm repositories:**

    ```bash
    helm repo update
    ```

3. **Install Keycloak using Helm:**

    ```bash
    helm install keycloak bitnami/keycloak --namespace keycloak --create-namespace
    ```

4. **Check the Keycloak service:**

    ```bash
    kubectl get svc -n keycloak
    ```

5. **Port-forward the Keycloak service to access it locally:**

    ```bash
    kubectl port-forward svc/keycloak 8080:80 -n keycloak
    ```

    This will forward port 8080 on your local machine to port 80 on the Keycloak service. You can then access the Keycloak admin console at:

    ```
    http://localhost:8080
    ```

## Retrieve Admin Password

- **For Windows:**

    Run the following PowerShell command to retrieve the admin password:

    ```powershell
    $secret = kubectl get secret keycloak -n keycloak -o jsonpath="{.data.admin-password}"
    [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($secret))
    ```

- **For Linux:**

    Run the following command to retrieve the admin password:

    ```bash
    kubectl get secret keycloak -n keycloak -o jsonpath="{.data.admin-password}" | base64 --decode
    ```

## Login to Keycloak

Once port-forwarding is complete, you can log into the Keycloak admin console at [http://localhost:8080](http://localhost:8080). 

Use the retrieved admin password to log in.
