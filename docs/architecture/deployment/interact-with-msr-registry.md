# Interact with MSR

You can interact with the Mirantis Secure Registry in the following ways:

- Use the MSR web UI to view, manage, and maintain content.

- Use the CLI for advanced operations:

    - [kubectl](https://kubernetes.io/docs/tasks/tools/) deploys and manages resources in Helm chart-based installations. 
    - [Mirantis Container Runtime (MCR)](https://docs.mirantis.com/mcr/current/overview.html) builds and runs services in
      Compose-based installations.

## Configure Linux (LF) line endings

All MSR tooling requires files that use Linux line endings (LF).
On Windows systems, ensure that all files such as configuration files,
manifests, or scripts use LF line endings only. Files that use Windows
line endings (CRLF) may cause errors.

**Set the line endings in vim**

1. Check the current line ending format in vim:

    ```bash
    :set ff?
    ```

2. If the result is not `unix`, change it by running:

    ```bash
    :set ff=unix
    ```

3. Save the file:

    ```bash
    :w
    ```

**Set the line endings manually**

Open your file in a text editor and ensure that line endings are set to LF.

**Set the line endings using the CLI**

- Use tools like `dos2unix` to convert CRLF to LF:

    ```bash
    dos2unix filename
    ```

- Alternatively, use `sed` to remove carriage returns:

    ```bash
    sed -i 's/\\r$//' filename
    ```
