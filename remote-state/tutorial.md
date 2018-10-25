# Remote state - Terraform

## Setup

<walkthrough-author name="adam@kiwi.com" analyticsId="UA-125550242-1" tutorialName="tf_remote_state" repositoryUrl="https://github.com/adam-janis/terraform-me"></walkthrough-author>

Welcome to Terraform in Google Cloud Shell! We need you to let us know what project you'd like to use with Terraform.

<walkthrough-project-billing-setup></walkthrough-project-billing-setup>

Terraform provisions real GCP resources, so anything you create in this session will be billed against this project.

## Terraforming!

Let's use {{project-id}} with Terraform! Click the Cloud Shell icon below to copy the command
to your shell, and then run it from the shell by pressing Enter/Return. Terraform will pick up
the project name from the environment variable.

```bash
export GOOGLE_CLOUD_PROJECT={{project-id}}
```

After that, let's get Terraform started. Run the following to pull in the providers.

```bash
terraform init
```

With the providers downloaded and a project set, you're ready to use Terraform. Go ahead!

```bash
terraform apply
```

Terraform will show you what it plans to do, and prompt you to accept. Type "yes" to accept the plan.

```bash
yes
```


## Terraform state

### Local 

Now you've provisioned your resources with Terraform! If you run a "plan", you should see no changes needed.

```bash
terraform plan
```

Let's have a look what is inside your state file.

```bash
cat terraform.tfstate
```

### Remote state file

Best practise is to store state remotely so the team can easily collaborate, so let's move it!

First of all, let's create Google storage bucket
```bash
gsutil mb gs://tf-state-terraform-me-YOUR_NAME
```

Then, open `providers.tf` file <walkthrough-editor-open-file filePath="providers.tf"></walkthrough-editor-open-file> and uncomment backend configuration. (+ change **bucket** to match your created bucket name)

Afterwards you can run an init, which will do the migration to the remote backend for you.
```bash
terraform init
```

```bash
yes
```

## Cleanup

Run the following to remove the resources Terraform provisioned:

```bash
terraform destroy
```
```bash
yes
```
