[200~## Key Concepts Covered

- **Identity and Access Management (IAM):** Understanding what IAM is and its importance in Azure.
- **Authentication vs. Authorization:** Differences and importance in managing access.
- **Roles and Role-Based Access Control (RBAC):** How roles are used to manage permissions.
- **Service Principals and Managed Identities:** Understanding these concepts and their use cases.

---

## Real-life Example

Real-life analogy of an office with different access levels for a DevOps engineer and a network engineer to explain authentication and authorization:

- **Authentication:** Validating identity to enter the office.
- **Authorization:** Determining access levels within the office (e.g., access to the cafeteria vs. the data center).

---

## Azure IAM Basics

### Authentication and Authorization in Azure

- **Authentication:** Ensuring users have valid credentials to access Azure resources.
- **Authorization:** Defining what authenticated users are allowed to do.

### Users, Groups, and Roles

- **Users:** Individual accounts for accessing Azure.
- **Groups:** Collections of users to simplify permission management.
- **Roles:** Predefined sets of permissions assigned to users or groups.

### Microsoft Entra ID (formerly Azure Active Directory)

- Central service for managing authentication and authorization in Azure.
- Provides functionalities like user management, group management, and role assignments.

---

## Demonstration

### Scenario

Access a file in Blob Storage from a Virtual Machine securely using Managed Identities.

### Steps

1. **Create a Resource Group:**
   - Resource groups help manage and organize Azure resources.

2. **Create a Storage Account and Blob Container:**
   - Upload a sample file (e.g., index.html) to the blob container.

3. **Create a Virtual Machine:**
   - Enable system-assigned managed identity for the VM.

4. **Assign Role to Managed Identity:**
   - Assign a role (e.g., Storage Blob Data Owner) to the VM's managed identity to access the storage account.

5. **Access the File from the Virtual Machine:**
   - Use a shell script to fetch the access token and retrieve the file from the blob storage.

---

## Shell Script Example

```bash
# Fetch the access token for the managed identity
access_token=$(curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://storage.azure.com/' -H Metadata:true | jq -r '.access_token')

# Use the access token to access the blob file
curl https://<storage-account>.blob.core.windows.net/<container-name>/<blob-name>? -H "x-ms-version: 2017-11-09" -H "Authorization: Bearer $access_token"
```

---

## Best Practices

- **Use Managed Identities:** Prefer managed identities over service principals for better security and ease of management.
- **Assign Least Privilege Roles:** Grant only the necessary permissions to users and resources.
- **Regularly Review Access:** Monitor and review access assignments to ensure they are still required.

~
