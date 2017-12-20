# Google Cloud Container Builder community images

This repository contains source code for community-contributed Docker images. You can use these images as build steps for
[Google Cloud Container Builder](https://cloud.google.com/container-builder/docs/).

These are not official Google products.

## How to use a community-contributed build step

Google Container Builder executes a build as a series of build steps. Each build step is run in a Docker container. See
the [Container Builder documentation](https://cloud.google.com/container-builder/docs/overview) for more details
about builds and build steps.

### Before you begin

1.  Select or create a [Google Cloud project](https://console.cloud.google.com/cloud-resource-manager).
2.  Enable [billing for your project](https://support.google.com/cloud/answer/6293499#enable-billing).
3.  Enable [the Container Builder API](https://console.cloud.google.com/flows/enableapi?apiid=cloudbuild.googleapis.com).
4.  Install and initialize [the Cloud SDK](https://cloud.google.com/sdk/docs/).

### Build the build step from source

To use a community-contributed Docker image as a build step, you need to download the source code from this
repo and build the image.

The example below shows how to download and build the image for the `packer` build step on a Linux or Mac OS X workstation:

1. Clone the `cloud-builders-community` repo:

   ```sh
   $ git clone http://github.com/GoogleCloudPlatform/cloud-builders-community
   ```

2. Go to the directory that has the source code for the `packer` Docker image:

   ```sh
   $ cd cloud-builders-community/packer
   ```

3. Build the Docker image:

   ```
   $ gcloud container builds submit --config cloudbuild.yaml .
   ```

4. View the image in Google Container Registry:

   ```sh
   $ gcloud container images list --filter packer
   ```

### Use the build step with Container Builder build

Once you've built the Docker image, you can use it as a build step in a Container Builder build.

For example, below is the `packer` build step in a YAML
[config file](https://cloud.google.com/container-builder/docs/build-config), ready to be used in a Container Builder build:

   ```yaml
   - name: 'gcr.io/$PROJECT_ID/packer'
     args:
     - build
     - -var
     - project_id=$PROJECT_ID
     - packer.json
   ```

Each build step's `examples` directory has an example of how you can use the build step. See the
[example for the `packer` builder](https://github.com/GoogleCloudPlatform/cloud-builders-community/tree/master/packer/examples/gce).

## Contributing

We welcome contributions!  See [CONTRIBUTING](CONTRIBUTING.md) for more information on how to get started.
Please include a `cloudbuild.yaml` and at least one working example in your
[pull request](https://help.github.com/articles/about-pull-requests/).

## License

This source code is licensed under Apache 2.0. Full license text is available in [LICENSE](LICENSE).

## Support

*   File issues here in GitHub about the community build steps.
*   Email `gcr-contact@google.com` if you have questions about build steps or Google Cloud Container Builder.
