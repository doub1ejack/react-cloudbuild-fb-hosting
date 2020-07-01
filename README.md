# Sample Cloudbuild React app

## About this repo
This is an exercise in learning how to deploy a simple React app to firebase hosting. This repo contains the following:

- React.js app (working dummy app from create-react-app)
- TypeScript
- Google Cloud Build config file

Once you've got the Google services enabled and configured, pushing changes to this repo should build your react app, run the tests, and deploy your changes to the firebase hosting.  The CI process takes about 90 seconds for me.

You should be able to set up & run this repo without incuring any charges.

## To use this yourself...
There are a few configuration steps you'll need to take in your Google Cloud Platform account:

1. Enable services
1. Create Firebase build-steps for Cloud Build
1. Connect github repo to Cloud Build
1. Enable Service Account permissions
1. Create Cloud Build trigger
1. Manually run the trigger

### Enable Google Services
You'll need a Google Cloud Platform account with these services enabled:

- Cloud Build API
- Firebase Hosting API
- Cloud Functions API
- Google Container Registry

### Create Firebase build-steps for Cloud Build
When I walked through this process, GCP didn't have the Cloud Build build steps for firebase available by default - I had to use the community version. Basically it's a simple matter of following the instructions to deploy a docker container to the Google Container Registry. Once you do this, Cloud Build will have what it needs in order to deploy your react app to Firebase hosting.

See: https://github.com/GoogleCloudPlatform/cloud-builders-community

### Enable Service Account permissions
After creating the initial cloud build config, and building the firebase container, it was also necessary to set up a Service Account to give cloud build the necessary permissions.

In Cloud Build, go down to "Settings" in the side nav and enable permissions for Firebase and Cloud Functions. (On a real project you'll likely want to get more granular with permissions, but this is enough to get the build running.)

### Connect github repo to Cloud Build
Just go to Cloud Build, click "Triggers" in the side nav and you should see a button to connect a repository. Follow the instructions.

### Create Cloud Build trigger
After connecting your repository, look for a "Create Trigger" link.  This is pretty intuitive:
- under "**Event**" select `Push to a branch`
- under "**Source**" use `^master$` to target the master branch

### Manually run the trigger
For testing purposes, on the "Triggers" page, there is a `Run Trigger` button.

### Firebase
There shouldn't be any setup to do here, but this is where you can go to see your hosted app.  Go to the [Hosting](https://console.firebase.google.com/u/0/project/) link in the side-nav and if your build was successful you'll see some automatic domains configured like https://[your-project-id].web.app

## References

* This is a solid overview of the basics of deploying to firebase hosting: https://cloud.google.com/cloud-build/docs/deploying-builds/deploy-firebase