# Deploy a CRA project to Vercel

In this example, a deployment of a regular CRA project is made to Vercel using Github secrets as env vars. Rather than using Vercel's auto-deployment feature to create a deployment for each commit to the main branch, this strategy uses GitHub Actions and Vercel CLI to deploy on whatever [event that trigger a workflow](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows).

### Get started

1. Create a vercel.json file at the root of your project folder to add [Git configuration](https://vercel.com/docs/concepts/projects/project-configuration/git-configuration#). Set `git.deploymentEnabled` to false which will prevent auto-deployments from commits..
2. Then, let’s add the required values from Vercel as [secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets) in GitHub
3. On your local computer or development environment, install the [Vercel CLI](https://vercel.com/cli) and run `vercel login`
4. Inside your project folder, run `vercel link` to create a new Vercel project or link to an existing one
5. Navigate to the generated `.vercel` folder, and open project.json to find the `projectID` and `orgId`
6. In GitHub, set `VERCEL_PROJECT_ID` to your `projectID` and `VERCEL_ORG_ID` to your `orgID`
7. Retrieve your [Vercel Access Token](https://vercel.com/guides/how-do-i-use-a-vercel-api-access-token) and set it as the value of `VERCEL_TOKEN`
8. Define a Github Action to kick off a deployment based on one of these [examples](https://github.com/danilobjr/vercel-gha/tree/main/.github/workflows)

### Deploy pre-built `build` folder

As you can see in the [deploy-static-pre-built-folder-and-create-pr-comment workflow](https://github.com/danilobjr/vercel-gha/blob/main/.github/workflows/deploy-static-pre-built-folder-and-create-pr-comment.yml), the application is pre built and then uploaded to Vercel.

To make this work properly, you need to change your project settings in Vercel.

1. Go to you project page in Vercel
2. Click in _Settings_
3. On the left menu, make sure _General_ is selected
4. Go to _Build & Development Settings_ section
5. Choose `Other` for `Framework Preset`
6. Leave _Build Command_ field empty
7. Hit `Save` button

This will prevent the build from being attempted and serve your content as-is.
