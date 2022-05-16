.github for newscorp-djcs
=========================

This repo contains starter workflows for the newscorp-djcs organization.

## tf_cloudfront.yml

  This workflow supports plan or apply through workflow_dispatch event for cononprodwsjbarrons or conprodwsjbarrons aws accounts.
  It also supports plan for push event for cononprodwsjbarrons or conprodwsjbarrons aws accounts.

  inputs for workflow_dispatch:

      environment:
        type: string
        default: staging
        required: true
        description:
             This is the name of your repo level environment.
             Valid values are staging|production.
             Any of the secrets input values can be defined in org level, repo level or repo-environment level.

      region:
        type: string
        default: 'virginia'
        required: true
        description:
            Text description of aws_region.
            Valid values are virginia, orgeon, or ohio.
            This will be converted to AWS_REGION by the module before initiializing aws.

      action:
        type: string
        default: plan
        required: true
        description:
             Either plan or apply.

      tf_version:
        type: string
        required: false
        default: 1.0.9
        description:
            Allows you to override the terraform version.

      node_version:
        type: string
        required: false
        default: 14
        description:
            Allows you to override the node version.

  secrets are setup in your github environments.

      These values are used by tokenito plugin until we get a new role setup by cloud ops.
      OKTA_USERNAME:
        required: true
        description: your email.
      OKTA_PASSWORD:
        required: true
        description: your password.
      OKTA_MFA_SEED:
        required: true
        description: your token from google auth scan code.
      OKTA_AWS_APP_URL:
        required: true
        description: url of aws okta tile.

      JOB_NAME:
        required: false
        description:
          This is historically the Jenkins job name.  Not always the same as your repo name.
          By default we'll use repo name but if that is not what your jenkins job name was, you
          will have to override it using a repo level secret.
          This is used in the artifactory state file storage path.
          If you get it wrong terraform will complain about missing a state file.

      STAGING_AWS_ROLE_ARN:
        required: true
        description:
           AWS_ROLE_ARN for staging environment.
           This will be set at org level eventually.

      PRODUCTION_AWS_ROLE_ARN:
        required: true
        description:
           AWS_ROLE_ARN for production environment.
           This will be set at org level eventually.

      DJCS_BACKEND_PASSWORD:
        required: true
        description:
           PASSWORD for artifactory.
           This is set at org level environemnt.

      TF_VARS:
        required: false
        description:
            Terraform variables in json format.
            This can be set at repo or repo-environment level.

      SLACK_WEBHOOK_URL:
        required: false
        description:
            If you want slack message set this at repo-environment level.

      CHANGE_MGMT_WEBHOOK:
        required: false
        descripiton:
            Set this if you want change management tickets created for successful production apply actions.
            ex. https://int-prod-change-mgmt.ohi.onservo.com/ticket/<tag-appid-value>
            This was known as remedy_webhook in jenkins.


