# Zip to CF

GitHub Actions Workflow for Static ZIP File to Cloudflare Pages Deployment

This repository contains a GitHub Actions workflow that automates the deployment of a static site from a ZIP file on a server to Cloudflare Pages. The workflow fetches the latest ZIP file, processes it, and uploads it to Cloudflare Pages daily.

## Features

- **Automated Daily Deployment**: The workflow runs daily at midnight UTC to fetch the latest ZIP file.
- **Manual Trigger**: The workflow can be triggered manually as well.
- **File Processing**: Includes steps to rename and move the 404 page to the root directory.
- **Redundancy Check**: Checks if the latest ZIP file has already been processed to avoid redundant uploads.

## Workflow Details

The GitHub Actions workflow is defined in `.github/workflows/deploy.yml`. Below are the key steps:

1. **Checkout Repository**: Checks out the repository using `actions/checkout@v3`.
2. **Set up SSH Key**: Configures the SSH key for accessing the server.
3. **Fetch Latest ZIP**: Fetches the latest static site ZIP file from the server.
4. **Check for Redundant Uploads**: Checks if the latest ZIP file has already been processed.
5. **Download and Extract ZIP**: Downloads and extracts the latest ZIP file.
6. **Modify 404 Page**: Renames the `404/index.html` to `404.html` and moves it to the root directory.
7. **Deploy to Cloudflare Pages**: Deploys the processed site to Cloudflare Pages.
8. **Save Processed ZIP**: Saves the latest processed ZIP file name to avoid redundant uploads in the future.
9. **Commit and Push**: Commits and pushes the updated state to the repository.

## Running Your Own Instance

### Prerequisites

- A server with static site ZIP export capabilities.
- A Cloudflare Pages project.
- GitHub repository secrets set up for the following variables:
  - `ZIP_DIR`: Directory where the ZIP file is stored on your server.
  - `PERSONAL_ACCESS_TOKEN`: Your GitHub Personal Access Token.
  - `SSH_PRIVATE_KEY`: Your SSH private key.
  - `SSH_USERNAME`: Your SSH username.
  - `SSH_HOSTNAME`: Your SSH hostname.
  - `CF_API_TOKEN`: Your Cloudflare API token.
  - `CF_ACCOUNT_ID`: Your Cloudflare Account ID.
  - `CF_PROJECT_NAME`: Your Cloudflare Pages project name.


To run your own private instance of this repository, follow these steps:

1. **Fork the Repository:**
   - Go to the GitHub page of this repository.
   - Click the "Fork" button on the top right corner to create your own copy of the repository.

2. **Clone Your Forked Repository:**
   - Clone the forked repository to your local machine.
   ```bash
   git clone https://github.com/<your-username>/zip-to-cf.git
   cd zip-to-cf

3. **Set Up Secrets:**
   - Add the necessary secrets in your forked GitHub repository settings (`Settings > Secrets and variables > Actions`).

4. **Customize Workflow:**
   - Modify the `.github/workflows/deploy.yml` file if necessary to match your specific setup.

5. **Commit and Push Changes:**
   - Commit and push any changes to your forked repository.
   ```bash
   git add .
   git commit -m "Customizing for my setup"
   git push origin main```

6. **Merging Updates:**
   - When the original repository is updated, you can merge these changes into your fork. Since secrets are stored in the repository settings and not in the code, they will remain unaffected and continue to work.
   - By following these steps, you can run your own instance of this deployment workflow. If you have any issues or need help, feel free to open an issue in the original repository.