# Install MSR using Docker Compose

After installing the prerequisites, you can deploy MSR by following the steps
below.

## Download the MSR installer

1. Locate the `.tgz` installer package of the latest release of MSR at
   [Mirantis Packages](https://packages.mirantis.com/?prefix=msr/).  
   The release is available as a single bundle and is suitable only for
   offline installations.

2. Right-click on the installer package and copy the download link.

3. Download the package to your instance:

    ```bash
    wget https://s3-us-east-2.amazonaws.com/packages-mirantis.com/msr/msr-offline-installer-<VERSION>.tgz
    ```

4. Extract the package:

    ```bash
    tar xvf msr-offline-installer-<VERSION>.tgz
    ```

5. Navigate to the extracted folder:

    ```bash
    cd msr
    ```

## Configure MSR

1. Open the ``harbor.yml`` configuration file in your editor of choice, for
   example:

    ```bash
    cp harbor.yml.tmpl harbor.yml
    vim harbor.yml
    ```

2. Modify key parameters:

   1. Set the hostname for MSR to the domain name or IP address where MSR
      will run:

       ```bash
       hostname: <YOUR-DOMAIN.COM>
       ```

   2. Set a password for the MSR admin:

       ```bash
       harbor_admin_password: <YOUR-PASSWORD>
       ```

   3. Ensure the directory where MSR stores its data has enough disk space:

       ```bash
       data_volume: </YOUR/DATA/PATH>
       ```

## Prepare certificates for SSL

To enable SSL, configure paths to your SSL certificate and key:

1. If you do not have an SSL certificate from a trusted certificate authority
   (CA), you can generate self-signed certificates for testing purposes:
      
    ```bash
    openssl req -newkey rsa:4096 -nodes -sha256 -keyout ./<YOUR-DOMAIN.COM>.key -x509 -days 365 -out ./<YOUR-DOMAIN.COM>.crt
    ```

    !!! note

        For production environments, you can acquire the SSL certificates
        through providers like Let's Encrypt or commercial CA vendors.

2. Place the generated ``<YOUR-DOMAIN.COM>.crt`` and ``<YOUR-DOMAIN.COM>.key``
   in a secure directory.
3. Update your ``harbor.yml`` configuration file to point to these certificate
   files:

    ```bash
    certificate: </PATH/TO/YOUR-DOMAIN.COM>.crt
    private_key: </PATH/TO/YOUR-DOMAIN.COM>.key
    ```

4. Verify that your firewall settings allow traffic on port ``443`` as SSL
   communication requires this port to be open.

## Install and start MSR

You can proceed to the MSR installation only after you have configured
`harbor.yml`.

1. Run the installation script:

    ```bash
    sudo ./install.sh
    ```

    This script uses Docker Compose to install the MSR services.

    !!! note

        To enable image scanning, install Trivy along with MSR by running:

        ```bash
        sudo ./install.sh --with-trivy
        ```

2. Verify if the services are running:

    ```bash
    sudo docker compose ps
    ```

    You should be able to see services like `harbor-core`, `harbor-db`,
    `registry`, and so on, running.

## Access MSR

Once the services are running, you can access MSR from a web browser at
`http://<YOUR-DOMAIN.COM>` using the admin credentials set in
`harbor.yml`. You will get redirected to `https` if SSL is enabled
on the instance.
