---
slug: quickstart-managed-scans
append_help_link: true
title: "Quickstart: Managed Scans"
hide_title: true
description: Set up Semgrep Managed Scans when you sign in to Semgrep for the first time.
toc_max_heading_level: 2
tags:
  - Quickstart
  - Semgrep AppSec Platform
---

import SmsSupport from "/src/components/reference/_sms-support.mdx"
import GitlabRequirements from "/src/components/reference/_gitlab-sms-requirements.mdx"

# Quickstart for Semgrep Managed Scans

Semgrep Managed Scans (beta) is the fastest method to scan projects at scale with Semgrep. A **project** is any codebase, repository, or folder within a monorepo that is added to Semgrep for scanning.

With Semgrep Managed Scans, instead of adding Semgrep to your CI/CD pipeline, which requires a configuration file for each repository, Semgrep handles the scan process for all of the repositories you add.

## Supported source code managers

<SmsSupport />

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Add projects to Semgrep Managed Scans

<Tabs
    defaultValue="gh"
    values={[
    {label: 'Azure DevOps', value: 'ado'},
    {label: 'Bitbucket', value: 'bb'},
    {label: 'GitHub', value: 'gh'},
    {label: 'GitLab', value: 'gl'}
    ]}
>

<TabItem value='ado'>

### Prerequisites

You must have admin access to your Azure DevOps organization.

Read access is granted through an access token you generate on Azure DevOps. You can provide this token by [adding Azure DevOps as a source code manager](/deployment/connect-scm#connect-to-cloud-hosted-orgs).

Semgrep recommends setting up and configuring Semgrep with an Azure DevOps service account, not a personal account. Regardless of whether you use a personal or service account, the account must be assigned the **Owner** or **Project Collection Administrator** role for the organization. During setup and configuration, you must provide a personal access token generated by this account. This token must be authorized with **Full access**. Once you have Managed Scanning fully configured, you can update the token provided to Semgrep to one that's more restrictive. The scopes you must assign to the token include:

- `Code: Read`
- `Code: Status`
- `Member Entitlement Management: Read`
- `Project and Team: Read & write`
- `Pull Request Threads: Read & write`

### Add a project

<!-- vale off -->
1. Sign in to [Semgrep AppSec Platform](https://semgrep.dev/login)
2. Navigate to **Projects**, and click **Scan new project > Semgrep Managed Scan**.
3. In the **Enable Managed Scans for repos** page, select the repositories you want to add to Semgrep Managed Scans.
4. Click **Enable Managed Scans**. The **Enable Managed Scans** dialog appears. By default, Semgrep runs both full and diff-aware scans.
5. Click **Enable**. You are taken to the **Projects** page as your scans begin.
<!-- vale on -->

</TabItem>

<TabItem value='gh'>

### Prerequisites

You must have admin access to your GitHub organization.

To enable and use this feature, you must grant Semgrep **Read access** to your code. Steps are provided in [Add projects to Semgrep Managed Scans](#add-projects-to-semgrep-managed-scans).

Read access is permitted through a private Semgrep app that you create and register yourself. See [Managed Scans > Security](/deployment/managed-scanning/overview#security) for more information on how Semgrep handles your code.

### Add a project

<!-- vale off -->
<!-- Our in-product text reads "repos" -->

1. Navigate to [Semgrep AppSec Platform](https://semgrep.dev/login), and sign up by clicking on **Sign in with GitHub**. Follow the on-screen prompts to [grant Semgrep the necessary permissions](/deployment/checklist/#permissions) and proceed.
1. Provide the **Organization display name** you'd like to use, then click **Create new organization**.
1. When asked **Where do you want to scan?** click **GitHub**.
1. Follow the steps in the **Connect GitHub to Semgrep** page. These steps install a public GitHub app, which handles PR comments, and a private GitHub app, which handles code access. You are able to select which repositories these apps have access to, and have full control over removing them or revoking their permissions.
1. Click **Set up projects**. You are taken to the **Enable Managed Scans for repos** page.
1. Select all the repositories you want to add to Semgrep Managed Scans for scanning.
1. Click **Enable Managed Scans**. You are taken to the **Projects** page as your scans begin.

<!-- vale on -->

</TabItem>
<TabItem value='gl'>

### Prerequisites

<GitlabRequirements />

### Add a project

<!-- vale off -->
1. Navigate to [Semgrep AppSec Platform](https://semgrep.dev/login), and sign up by clicking on **Sign in with GitLab**. Follow the on-screen prompts to proceed.
2. When prompted, click **Scan new project > Semgrep Managed Scan**.
4. In the **Enable Managed Scans for repos** page, select the repositories you want to add to Semgrep Managed Scans.
5. Click **Enable Managed Scans**. The **Enable Managed Scans** dialog appears. By default, Semgrep runs both full and diff-aware scans.
6. Click **Enable**. You are taken to the **Projects** page as your scans begin.
<!-- vale on -->

</TabItem>

<TabItem value='bb'>

### Prerequisites

You must have admin access to your Bitbucket organization.

#### Bitbucket Cloud

- Read access is granted through a [workspace access token](https://support.atlassian.com/bitbucket-cloud/docs/workspace-access-tokens/) you generate on Bitbucket. You can provide this token by [adding Bitbucket as a source code manager](/deployment/connect-scm#connect-to-cloud-hosted-orgs).
- The user generating the workspace token must be a **Product Admin** for the workspace. The scopes you must assign to the token include:
  - `webhook (read and write)`
  - `repository (read and write)`
  - `pullrequest (read and write)`
  - `project (admin)`
  - `account (read)`

#### Bitbucket Data Center

- V8.8 or above for diff-aware scans.
- Read access is granted through an [HTTP access token](https://confluence.atlassian.com/bitbucketserver/http-access-tokens-939515499.html) you generate on Bitbucket. You can provide this token by [adding Bitbucket as a source code manager](/deployment/connect-scm#connect-to-on-premise-orgs-and-projects).
- The user generating the workspace token must be a **Product Admin** for the workspace. The token must be created with `PROJECT_ADMIN` permissions.

### Add a project

<!-- vale off -->
1. Sign in to [Semgrep AppSec Platform](https://semgrep.dev/login)
2. Navigate to **Projects**, and click **Scan new project > Semgrep Managed Scan**.
3. In the **Enable Managed Scans for repos** page, select the repositories you want to add to Semgrep Managed Scans.
4. Click **Enable Managed Scans**. The **Enable Managed Scans** dialog appears. By default, Semgrep runs both full and diff-aware scans.
5. Click **Enable**. You are taken to the **Projects** page as your scans begin.
<!-- vale on -->

</TabItem>

</Tabs>

You have finished setting up a Semgrep managed scan.

Here are some behaviors and characteristics of a managed scan:

- After enabling Managed Scans, Semgrep performs a full scan in batches on all the repositories that have been added to it.
- In general, once a git repository has been added to Semgrep AppSec Platform, it becomes a **project**. A project in Semgrep AppSec Platform includes all the findings, history, and scan metadata of that repository.
- Projects scanned through Managed Scans are tagged with `managed-scan`.

## Next steps

Once a scan has finished, you can view your findings by clicking any of the following on the navigation menu:

- [<i class="fas fa-external-link fa-xs"></i>  Code](https://semgrep.dev/orgs/-/findings?tab=open&primary=true) for SAST findings
- [<i class="fas fa-external-link fa-xs"></i> Secrets](https://semgrep.dev/orgs/-/secrets?tab=open&validation_state=confirmed_valid,validation_error,no_validator) for secrets findings
- [<i class="fas fa-external-link fa-xs"></i> Supply Chain](https://semgrep.dev/orgs/-/supply-chain/vulnerabilities?primary=true&tab=open) for SCA findings

To learn more about how Semgrep manages your scans, read the in-depth [Semgrep Managed Scans documentation](/deployment/managed-scanning/overview).
