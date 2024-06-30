This is a [Kobweb](https://github.com/varabyte/kobweb) project bootstrapped with the `app/empty` template.

This template is useful if you already know what you're doing and just want a clean slate. By default, it
just creates a blank home page (which prints to the console so you can confirm it's working)

If you are still learning, consider instantiating the `app` template (or one of the examples) to see actual,
working projects.

## Getting Started

First, run the development server by typing the following command in a terminal under the `site` folder:

```bash
$ cd site
$ kobweb run
```

Open [http://localhost:8080](http://localhost:8080) with your browser to see the result.

You can use any editor you want for the project, but we recommend using **IntelliJ IDEA Community Edition** downloaded
using the [Toolbox App](https://www.jetbrains.com/toolbox-app/).

Press `Q` in the terminal to gracefully stop the server.

### Live Reload

Feel free to edit / add / delete new components, pages, and API endpoints! When you make any changes, the site will
indicate the status of the build and automatically reload when ready.

## Exporting the Project

When you are ready to ship, you should shutdown the development server and then export the project using:

```bash
kobweb export
```

When finished, you can run a Kobweb server in production mode:

```bash
kobweb run --env prod
```

If you want to run this command in the Cloud provider of your choice, consider disabling interactive mode since nobody
is sitting around watching the console in that case anyway. To do that, use:

```bash
kobweb run --env prod --notty
```

Kobweb also supports exporting to a static layout which is compatible with static hosting providers, such as GitHub
Pages, Netlify, Firebase, any presumably all the others. You can read more about that approach here:
https://bitspittle.dev/blog/2022/staticdeploy


# Deploy to AWS

Steps:
- create Aws account
- in Iam create user you will use for the gitlab runner and give it permissions to:
  - AmazonECS_FullAccess
  - AWSAppRunnerFullAccess
  - AWSAppRunnerServicePolicyForECRAccess
  - EC2InstanceProfileForImageBuilderECRContainerBuilds
  - IAMFullAccess
  I gave full access to each, which is over-provisioned...
- when the GitLab runner user is created, create an Access key for it with the key id and secret
- also in Iam, create role you will use when pushing to the App runner, i added the same permissions to the role as to the user, which is also over-provisioned...
- in the Elastic Container Registry, in Repositories, create new repository "kobweb-app"
- in the github repo add secrets:
  - AWS_ACCESS_KEY_ID=your_key
  - AWS_SECRET_ACCESS_KEY=your_secret
  - AWS_REGION=your_region
  - ECR_REPOSITORY=name of the ECR repository created in the previous step
  - ROLE_ARN=arn to the role you cerated in the earlier step
  - APP_RUNNER_SERVICE_NAME=chosen name for the app runner service
