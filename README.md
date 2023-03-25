# AWS SAM Frontend

## Description

This package allows you to deploy any frontend personal project that uses a JS framework. Just drop the directories/files into the [frontend](./packages/frontend) package of this mono repo and you can then deploy it directly to AWS using Cloudfront and S3 with one command. Your frontend project must have a `package.json` and `build script`. It's as simple as that. The resulting stack will be given a unique url that you can add to your CV, Linkedin profile or share directly with prospective employers to showcase your skills.

Why use this over alternatives like Heroku? Well it's fully customisable, it can be extended to add apis/dbs and gives you full control. It can also be a great tool to upskill yourself on cloud services and client/server infrastructure.

## Setup

### Prerequisites

- [node](https://nodejs.org/en/)
- [yarn](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable)
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-mac.html)
- [AWS SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install-mac.html)
- [An AWS account](https://aws.amazon.com/)

### Steps

1. Sign up for AWS and [set a budget limit with alerts](https://acloudguru.com/videos/acg-fundamentals/how-to-set-up-an-aws-billing-and-budget-alert?utm_source=google&utm_medium=paid-search&utm_campaign=cloud-transformation&utm_term=ssi-global-acg-core-dsa&utm_content=free-trial&gclid=Cj0KCQjwlPWgBhDHARIsAH2xdNc1B2rjJN2i4mgEEG6hLWxB21yhBJuF7rsHKoqzw-TFMhUdGL9dv3kaAh9-EALw_wcB). Hosting your demo will be free as you shouldn't be expecting any significant traffic and will comfortably fall within Free Tier usage. A budget prevents any unexpected charges if there is a spike in traffic. Be safe and set a budget limit!

2. Once your account is setup. Navigate to 'Security Credentials' to [create an access key](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html). This access key will allow your shell to read/write to AWS. Make a note of these as they will be used in step 3. Remember to keep these safe and not to share these publicly in VCS like github.

3. Use AWS CLI to configure your shell by running the command below. It will ask you to enter the `access key id` and `security key id` that you created in step 2. It will also ask for region and output. These will be `eu-west-2` and `json` respectively. Note: these are stored in your root directory in an .aws folder if you ever need to find them. 

```
aws configure
```

4. Open the aws-sam-frontend repo in your IDE. Search for 'project-name' and replace it with your personal project's name. Be sure to use rope case.

5. Copy all the files and directories within your personal project's root folder and add them to the [frontend](./packages/frontend) package of this repo.

6. In the root of this repo, run the following:

```
make lazyLoad ENV=<add an environment name>
```

The ENV param allows you to deploy an infinite number of versions of your project as long as you change this flag. Common examples include ENV=dev, ENV=int, ENV=prod or if you're fancy ENV=banana. This flag just ensures that AWS resources have a unique name, which is one of their requirements.

### BEEP BOP BOOP 

You're personal project should now have been deployed and opened in your browser with a public url. Deploy as many frontend projects as your heart desires by completing step 4, 5 and 6 - rinse and repeat.

PSSSST - you know what else is really neat? This package can be used to create production sites. Just add Route53 which will then point to your custom domain.

### Making changes

If you have already completed the above steps and your frontend is deployed but you want to make changes then you can run one of the commands below. Onmce you are happy with your local frontend changes, run either:

```
make lazyLoad ENV=<same environment name as step 6>
```

OR

```
make appSync ENV=<same environment name as step 6>
```

`appSync` is recommended for frontend only changes as it's quicker. It does not check for changes in the infrastructure and instead just deploys your new build to S3. If you have made changes to the cloudformation templates in the [sam](./packages/sam) package then you'll need to run `lazyLoad`.
