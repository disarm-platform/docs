# Cache control

Requests made to _Google Cloud Storage_ objects are by default _not cachaeble,_ because the metadata set on each object includes `Cache-Control: private, max-age=0`. To alter this behavior the metadata for each object has to be set to `Cache-Control= public max-age=<amount>.` To avoid needing to manually set this for every new file, a service needs to be added which is reponsible for watching any files added to `gs://ds-faas/` and sets cache headers to enable them to be cached.

## Steps.

1. Copy paths of all objects in the cloud storage by running the command:

   ```text
   gsutil ls "gs://ds-faas/**" | grep -v /$ > files
   ```

   this stores the file paths in a file called files.

2. To alter the metadata of each of the objects in the cloud staorage run the command:

   ```text
   parallel --dry-run -j4 gsutil setmeta -r -h \'Cache-control:public, max-age=10000000\' :::: files
   ```

3. Add a cloud function, which will watch files added to `gs://ds-faas/`:
   * Select edit cloud function.
   * Select the bucket `ds-faas`.
   * Select `inline editor` under source code.
   * Select the `python 3.7` as the runtime.
   * On the `main.py` tab, add the following code.

```python
    from google.cloud import storage

    CACHE_CONTROL = "public, max-age=10000000"

    def set_cache_control(data, context):
        """Background Cloud Function to be triggered by Cloud Storage.
        This function changes Cache-Control meta data.

        Args:
            data (dict): The Cloud Functions event payload.
            context (google.cloud.functions.Context): Metadata of triggering event.
        Returns:
            None; the output is written to Stackdriver Logging
        """

        print('Setting Cache-Control to {} for: gs://{}/{}'.format(
                CACHE_CONTROL, data['bucket'], data['name']))
        storage_client = storage.Client()
        bucket = storage_client.get_bucket(data['bucket'])
        blob = bucket.get_blob(data['name'])
        blob.cache_control = CACHE_CONTROL
        blob.patch()
```

* On the `requirements.txt` tab add:

  ```text
        google-cloud-storage==1.10.0
  ```

* Then click `deploy` to deploy the function.

