# Getting started with {{ certificate-manager-name }}

By following this guide, you will add your first [Let's Encrypt certificate](../concepts/managed-certificate.md) to {{ certificate-manager-name }} and use it to [set up HTTPS access](../../storage/operations/hosting/certificate.md) to a static website hosted in {{ objstorage-full-name }}.

## Getting started {#before-you-begin}

To get started with {{ certificate-manager-name }}, you need:

1. Folder in {{ yandex-cloud }}. If there is no folder yet, create one:

    {% include [create-folder](../../_includes/create-folder.md) %}

1. Third-level (or higher) domain that the Let's Encrypt certificate is issued for.

    {% note info %}

    To pass the domain rights check, you must have the management access to the domain.

    {% endnote %}

1. Public bucket in Object Storage with exactly the same name as the domain. If you do not have a bucket yet, create one:

    {% list tabs group=instructions %}

    - Management console {#console}

        1. In the [management console]({{ link-console-main }}), select the folder you want to create a [bucket](../../storage/concepts/bucket.md) in.
        1. Select **{{ ui-key.yacloud.iam.folder.dashboard.label_storage }}**.
        1. Click **{{ ui-key.yacloud.storage.buckets.button_create }}**.
        1. Enter exactly the same name for the bucket as the domain name.
        1. Select the `{{ ui-key.yacloud.storage.bucket.settings.access_value_public }}` [access](../../storage/concepts/bucket.md#bucket-access) type.
        1. Select the default [storage class](../../storage/concepts/storage-class.md).
        1. Click **{{ ui-key.yacloud.storage.buckets.create.button_create }}** to complete the operation.

    {% endlist %}

1. Set up [hosting](../../storage/operations/hosting/setup.md) in your bucket:

    {% list tabs group=instructions %}

    - Management console {#console}

        1. In the [management console]({{ link-console-main }}), select **{{ ui-key.yacloud.iam.folder.dashboard.label_storage }}**.
        1. On the **{{ ui-key.yacloud.storage.switch_buckets }}** tab, click the bucket with the same name as the domain.
        1. In the left-hand panel, select **{{ ui-key.yacloud.storage.bucket.switch_settings }}**.
        1. Open the **{{ ui-key.yacloud.storage.bucket.switch_website }}** tab.
        1. Select `{{ ui-key.yacloud.storage.bucket.website.switch_hosting }}` and specify the website's homepage.
        1. Click **{{ ui-key.yacloud.storage.bucket.website.button_save }}** to complete the operation.

    {% endlist %}

1. Set up an [alias](../../storage/operations/hosting/own-domain.md) for the bucket through your DNS provider or on your own DNS server.

    For instance, for the `www.example.com` domain, add the following record:

    ```text
    www.example.com CNAME www.example.com.{{ s3-web-host }}
    ```

1. Install and configure the AWS CLI by following [this guide](../../storage/tools/aws-cli.md#before-you-begin).

## Create a request for a Let's Encrypt certificate {#request-certificate}

{% list tabs group=instructions %}

- Management console {#console}

    1. Go to the [management console]({{ link-console-main }}).
    1. Select **{{ ui-key.yacloud.iam.folder.dashboard.label_certificate-manager }}**.
    1. Click **{{ ui-key.yacloud.certificate-manager.button_empty-action }}**.
    1. In the menu that opens, select **{{ ui-key.yacloud.certificate-manager.action_request }}**.
    1. In the window that opens, enter a name for the certificate.
    1. (Optional) Add a description for the certificate.
    1. In the **{{ ui-key.yacloud.certificate-manager.request.field_domains }}** field, specify the domains you want to issue the certificate for.
    1. Select the [domain rights check type](../concepts/challenges.md) for `{{ ui-key.yacloud.certificate-manager.request.challenge-type_label_http }}`. 
    1. Click **{{ ui-key.yacloud.certificate-manager.request.button_request }}**.

{% endlist %}

## Passing the domain rights check {#validate}

### Creating a check file {#create-file}

{% list tabs group=instructions %}

- Management console {#console}

  1. In the [management console]({{ link-console-main }}), select **{{ ui-key.yacloud.iam.folder.dashboard.label_certificate-manager }}**.
  1. Select a certificate with the `Validating` status in the list and click it.
  1. Under **{{ ui-key.yacloud.certificate-manager.overview.section_challenges }}**:
      1. Copy the URL from the **{{ ui-key.yacloud.certificate-manager.overview.challenge_label_http-url }}** field:
          * The `http://example.com/.well-known/acme-challenge/` part of the link is the file path.
          * The second part, `rG1Mm1bJ...`, is the file name you should use.
      1. Copy the **{{ ui-key.yacloud.certificate-manager.overview.challenge_label_http-content }}** field to the file.

{% endlist %}

### Uploading the file and performing the check {#upload-and-check}

{% list tabs group=instructions %}

- Management console {#console}

  1. In the [management console]({{ link-console-main }}), select **{{ ui-key.yacloud.iam.folder.dashboard.label_storage }}**.
  1. On the **{{ ui-key.yacloud.storage.switch_buckets }}** tab, click the bucket with the same name as the domain.
  1. At the top right, click **{{ ui-key.yacloud.storage.bucket.button_create }}** and create a directory named `.well-known`.
  1. Under `.well-known`, create the `acme-challenge` directory.
  1. In `acme-challenge`, click **{{ ui-key.yacloud.storage.button_upload }}**.
  1. In the window that opens, select the file with a record and click **Open**.
  1. Click **{{ ui-key.yacloud.storage.button_upload }}**.
  1. Wait until the certificate's status changes to `Issued`.

     For more information on the status, see the certificate page. To do this, click **Viewing logs** next to **Validation**. 
  1. Go to `acme-challenge`.
  1. Click ![image](../../_assets/options.svg) to the right of the file and select **{{ ui-key.yacloud.common.delete }}**.
  1. Confirm the deletion.

- AWS CLI {#cli}

  1. Upload your file to the bucket so that it resides in the `.well-known/acme-challenge` subdirectory:

      ```bash
      aws --endpoint-url=https://{{ s3-storage-host }} \
        s3 cp <file_name> s3://<bucket_name>/.well-known/acme-challenge/<file_name>
      ```

  1. Wait until the certificate's status changes to `Issued`.
  1. Delete the file you created from the bucket:

      ```bash
      aws --endpoint-url=https://{{ s3-storage-host }} \
         s3 rm s3://<bucket_name>/.well-known/acme-challenge/<file_name>
      ```

{% endlist %}

{% note warning %}

To renew a certificate, you have to perform certain actions. Keep track of the lifecycle of your certificates to renew them on time. For more information, see [Renew a certificate](../concepts/managed-certificate.md#renew).

{% endnote %}

## Set up static website access over HTTPS {#hosting-certificate}

{% list tabs group=instructions %}

- Management console {#console}

    1. Log in to the [management console]({{ link-console-main }}).
    1. Select **{{ ui-key.yacloud.iam.folder.dashboard.label_storage }}**.
    1. On the **{{ ui-key.yacloud.storage.switch_buckets }}** tab, click the bucket with the same name as the domain.
    1. In the left-hand panel, select **{{ ui-key.yacloud.storage.bucket.switch_security }}**.
    1. Go to the **{{ ui-key.yacloud.storage.bucket.switch_https }}** tab.
    1. Click **{{ ui-key.yacloud.storage.bucket.https.button_action-configure }}** at the top right.
    1. In the **{{ ui-key.yacloud.storage.bucket.https.field_source }}** field, select `{{ ui-key.yacloud.storage.bucket.https.value_method-certificate-manager }}`.
    1. In the **{{ ui-key.yacloud.storage.bucket.https.field_certificate-manager }}** field, select the certificate from the list that opens.
    1. Click **{{ ui-key.yacloud.storage.bucket.https.button_save }}**.

{% endlist %}


#### See also {#see-also}

- [{#T}](../concepts/managed-certificate.md)
- [{#T}](../concepts/challenges.md)
- [Set up HTTPS in a bucket](../../storage/operations/hosting/certificate.md)
