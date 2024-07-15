# Instructions for AI Gateway Labs

## Option 1 - Using Local Development Environment

- navigate to [AI Gateway Labs - Getting Started](https://github.com/Azure-Samples/AI-Gateway?tab=readme-ov-file#-getting-started)
- Ensure you meet the **Prerequisites**
- Perform the following lab: [Backend Pool Load Balancing](https://github.com/Azure-Samples/AI-Gateway/blob/main/labs/backend-pool-load-balancing/backend-pool-load-balancing.ipynb) 

## Option 2 - Using Github Codespaces

- Create a new Public Repository in your GitHub account called `AI-Gateway-Labs`
- Clone this repo [AI Gateway Labs - Getting Started](https://github.com/Azure-Samples/AI-Gateway?tab=readme-ov-file#-getting-started) to your local machine, by running the following command:

  ```bash
  git clone https://github.com/Azure-Samples/AI-Gateway.git
  ```

- Change the remote URL to point to your newly created repository:

  ```bash
  cd AI-Gateway
  git remote remove origin
  git remote add origin <URL for AI-Gateway-Labs repo>
  git branch -M main
  git push -u origin main
  ```

- On your Github Repositories page, open your repository `AI-Gateway-Labs`in GitHub Codespaces:
    - Click on `Code` and select `Open with Codespaces`
    - Click on `Create new codespace`

- Perform the following lab: [Backend Pool Load Balancing](labs/backend-pool-load-balancing/backend-pool-load-balancing.ipynb)
