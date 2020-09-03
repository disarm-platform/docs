# Cache control for data file storage

We use _Google Cloud Storage_ to store some data files used by functions. These objects are by default _not cacheable,_ because the metadata set on each object includes `Cache-Control: private, max-age=0`. To alter this behavior the metadata for each object has to be set to `Cache-Control= public max-age=<amount>.` To avoid needing to manually set this for every new file, a service needs to be added which is responsible for watching any files added to the bucket and sets cache headers to enable them to be cached.

In the below, we're using the `gs://ds-faas/` bucket.

## Steps

### 1. Automatically set cache headers for any new files added to bucket

We're going to add a Google Cloud Function, which will watch files added to bucket, and update the headers:

* Create a new _Google Cloud Function_.
* Select _Cloud Storage_ trigger, and choose the bucket `ds-faas`.
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

1. Update any existing files in the bucket:
   1. Copy paths of all file objects in the cloud storage by running the command: `gsutil ls "gs://ds-faas/**" | grep -v /$ > files` \(ignore any ending in `/`\)
   2. Update the metadata of each \(using [GNU parallel](https://www.gnu.org/software/parallel/)\): `parallel --dry-run -j4 gsutil setmeta -r -h \'Cache-control:public, max-age=10000000\' :::: files`

