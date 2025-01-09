<img width="1084" alt="Screenshot 2025-01-08 at 10 06 12 AM" src="https://github.com/user-attachments/assets/b3469cd4-2858-416f-8492-7df235bd46ff" />

# Setup github on your PC
```zsh
# install git
brew install git
git version

# install nodejs
brew install node
node -v
npm -v
```

# Getting Started with Create React App
```bash
npx create-react-app persion-website
```

## Available Scripts
In the project directory, you can run:
```bash
# Runs the app in the development mode.
# Open [http://localhost:3000](http://localhost:3000) to view it in your browser.
npm start

# Launches the test runner in the interactive watch mode.
npm test

# Builds the app for production to the `build` folder.
npm build
```

<img width="1280" alt="Screenshot 2025-01-08 at 10 29 11 AM" src="https://github.com/user-attachments/assets/e8126d92-e9c3-4349-89c4-6335cfc3bf7b" />

# Setting Up GitHub Webhook with Jenkins
## 1. Install Required Plugins
First, you need to install some plugins in Jenkins to support integration with GitHub:
1.	Open the Jenkins web interface.
2.	Navigate to Manage Jenkins → Manage Plugins.
3.	In the Available tab, search for and install the following plugins:
- GitHub Plugin: Provides bi-directional integration between Jenkins and GitHub.
- Git Plugin: Allows Jenkins to use Git repositories as the source for your project.
- Pipeline Plugin (if you are using pipelines): Enables you to write scripts to define the build process.

![Screenshot 2025-01-09 at 2 40 04 PM](https://github.com/user-attachments/assets/fb37e548-6fe7-4646-ad71-03a896f1d132)

## 2. Create a Personal Access Token on GitHub
1.	Log in to GitHub: Go to github.com and log in to your account.
2.	Access Developer Settings:
- Click on your profile picture in the top-right corner and select Settings.
- In the left sidebar, scroll down and click on Developer settings.
3.	Generate a New Token:
- Click on Personal access tokens, then select Tokens (classic), and click Generate new token.
- Provide a descriptive name for the token to remind you of its purpose.
- Set an expiration date to enhance security.
```bash
1. **repo**: Grants full control over private and public repositories, including read and write permissions.
- This is necessary for Jenkins to access your GitHub repository for cloning, pulling, and pushing operations.
2.	**admin:repo_hook**: Allows management of repository-level webhooks.
- This enables Jenkins to automatically set up and manage webhooks in your repository to trigger builds.
3.	**admin:org_hook (if applicable)**: Allows management of organization-level webhooks.
- This is necessary if you are running Jenkins jobs at the organization level.
4.	**read:org**: Allows reading of organization and team member information.
- This is useful for Jenkins to retrieve organizational structure information for authorization and access control.
5.	**user:email**: Allows reading the user’s primary email address.
- This helps Jenkins verify the user’s identity.
```
![Screenshot 2025-01-09 at 2 48 24 PM](https://github.com/user-attachments/assets/381b3c59-dbdb-4a12-957e-36b65eff9e19)
4. Click `Generate Token`.
![Screenshot 2025-01-09 at 2 50 24 PM](https://github.com/user-attachments/assets/9ea7157d-53dc-45c8-9337-6aac77a25719)
5. Copy the generated token immediately and store it securely. Once you leave this page, you will not be able to view it again.

## 3. Configure GitHub Credentials
1.	Access Jenkins Credentials:
- Log in to your Jenkins instance.
- Navigate to Manage Jenkins → Manage Credentials.
- Select the appropriate domain (e.g., Global credentials (unrestricted)).
2.	Add New Credential:
- Click Add Credentials.
- In the Kind dropdown, select Username with password.
- Enter your GitHub username in the Username field.
- Paste the personal access token in the Password field.
- Provide a description to easily identify this credential.
- Click OK to save.
![Screenshot 2025-01-09 at 2 59 14 PM](https://github.com/user-attachments/assets/af24497a-34d2-4c48-878b-3f363ba7f7c1)

## 4. Setting Up Source Control Management in Jenkins
1.	In the Jenkins dashboard, select the project you want to configure and click Configure.
2.	In the Source Code Management section, select Git, then enter your repository URL.
3.	In the Credentials dropdown menu, select the GitHub credentials you added earlier.
![Screenshot 2025-01-09 at 3 00 36 PM](https://github.com/user-attachments/assets/02b8933c-2ad5-406d-a2ac-db8c957f398f)

## 5. Set Up a Webhook in GitHub:
1.	Go to your GitHub repository and click Settings.
2.	In the left sidebar, select Webhooks, then click Add webhook.
3.	In the Payload URL field, enter the URL of your Jenkins server, followed by /github-webhook/. For example: http://your-jenkins-server.com/github-webhook/.
4.	Set the Content type to application/json.
5.	Under Which events would you like to trigger this webhook?, select Just the push event.
6.	Click Add webhook to save.
![Screenshot 2025-01-09 at 3 03 20 PM](https://github.com/user-attachments/assets/fa749322-e9f4-4368-8fa0-fad5d06bd81e)

## 6. Configure Your Jenkins Job:
1.	In the Jenkins dashboard, select the job you want to configure and click Configure.
2.	In the Source Code Management section, select Git, enter your repository URL, and select the credentials you added earlier.
3.	In the Build Triggers section, check the box for GitHub hook trigger for GITScm polling.
4.	In the Build section, add the appropriate build steps, such as executing a shell script to install dependencies and run tests:
![Screenshot 2025-01-09 at 3 05 38 PM](https://github.com/user-attachments/assets/8c17cbfd-6171-4651-87cc-b77cec5402d3)
