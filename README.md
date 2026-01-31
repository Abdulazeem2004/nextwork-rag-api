<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Automate Testing with GitHub Actions

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-devops-githubactions)

**Author:** Abdulazeem Badmus  
**Email:** badmusazeem05@gmail.com

---

![Image](http://learn.nextwork.org/grateful_gray_shy_mouse/uploads/ai-devops-githubactions_i1j2k3l4)

---

## Introducing Today's Project!

In this project, I will demonstrate how to automate testing with github actions. I'm doing this project to learn how to use github actions to automaticaly test a code to be deployed in a CI/CD pipepline.

### Key services and concepts

Services I used were Git, GitHub, Github Action. Key concepts I learnt include, Mock LLM, github actions, .gitignore file,  workflow file.

### Challenges and wins

This project took me approximately 1 hour and 30 minutes. The most challenging part was understanding how to correctly define the GitHub Actions workflow, including configuring triggers, setting up the testing environment, and ensuring tests ran automatically and reliably on every push. It was most rewarding to see the workflow execute successfully, with tests running step by step and validating the code automatically, giving confidence that changes are checked before reaching production.

### Why I did this project

I did this project because I wanted to learn how to automate testing using GitHub Actions and understand how continuous integration helps maintain code quality. One thing I’ll apply from this is setting up automated tests on every push so issues are caught early and code changes are validated before deployment.

---

## Setting Up Your RAG API

I'm setting up my RAG API by reviewing the code, database and dependencies and testing it locally. A RAG API retrieves information by using a LLM to go through a knowlegde base to augument replies for a request which gives accurate and up todate responses. This foundation is needed for CI/CD because...

### Local API verification

I tested my RAG API by invoking this command "Invoke-WebRequest -Uri "http://127.0.0.1:8000/query?q=What%20is%20Kubernetes%3F" -Method POST
". The API responded with a succesful 200 status code with a reply to the questrioned asked. This confirms thatRAG API endpoint is up and running and ready to recieve and send responses.

![Image](http://learn.nextwork.org/grateful_gray_shy_mouse/uploads/ai-devops-githubactions_i9j0k1l2)

---

## Initializing Git and Pushing to GitHub

I’m initializing Git by running the command git init. Git tracks changes by taking snapshots of files over time. Version control enables CI/CD to automatically detect code changes, trigger automated workflows such as testing and deployment, and ensure that only validated code progresses through the pipeline.

### Git initialization and first commit

I initialized Git by running the command"git init". Then, I staged and committed by running the command "git add ." and "git commit -m "Initial commit: set up local RAG API project"
". The .gitignore file helps by specifiying the files git should ignore and not to be staged or commited in order to keep the repository cleaner, faster to clone, and prevents conflicts between different development environments!



### Pushing to GitHub for CI/CD

Pushing to GitHub means uploading the git repository on my local machine to a cloud base repository where the code can be viewed and pulled by anyone. This enables CI/CD because github action is on github so pushing this repository to github will make me use the github action for CI/CD.

![Image](http://learn.nextwork.org/grateful_gray_shy_mouse/uploads/ai-devops-githubactions_y5z6a7b8)

---

## Creating Semantic Tests

I'm creating semantic tests that verify the RAG system returns ansers with the right meaning Unlike unit tests that check code logic, semantic tests validate data quality. These tests ensure quality by verifying that theRAG system returns answers with the correct meaning and includes relevant key concepts..

### Non-deterministic output observation

When I ran the query multiple times, I noticed that the response varied with added "orchestration" and sometimes not added due to the non-deterministic behaviour of the LLM. This is a problem because you can't tell if your code is actually broken or if the LLM just happened to generate a slightly different response this time. For CI/CD to work reliably, we need "mock LLM mode". a way to test retrieval quality without relying on LLM generation

---

## Adding Mock LLM Mode

I'm adding mock LLM mode to test the semantic of the reponse generated. This solves the non-determinism problem by sending the full context of the reply without relying on the LLM adding variability. Reliable testing requires getting the same consistent replies when queried.

### How mock mode solves the problem

### Mock LLM mode for CI testing

Mock LLM mode returns the retrieved text directly, which makes tests reliable because consistent replies are generated everytime  the RAG API is queried. Without mock mode, tests would not be reliable due to the non deterministic behaviour of the LLM that creates variabilities in the anwers generated. For automated CI, we need a consistent and reliable testing to guarantee the semantic response of the RAG API is either correct or not which must not depend on the reply of the LLM hence the MOCK LLM help solve this problem.

---

## Creating GitHub Actions Workflow

I'm creating a GitHub Actions workflow file that describe how the automated process should run, from building to testing and deployment. The workflow automates testing by automatically running predefined test suites and validation checks on every code push. . When I push code, it will trigger this automation process and all workflow are done step by step in an ordely manner to ensure that anytime i push a code it is automatically validated preventing issues from reaching production, to maintain the quality of the sytem.

### Workflow automation and CI testing

I created the workflow file in a yaml file "github/workflows/ci.yaml". I pushed it using "git push
". Once on GitHub, the workflow will automatically be initiated and when a modification in any of the file specified in the yaml file is pushed the worflow automation will be begin to run.

---

## Testing Data Quality

I'm triggering the CI workflow by changing the knowledge base of the RAG app. The workflow will test the data quality of the response. I expect it to fail because i intentionally remove some key words in the knowlegde base just to verify the workflow is reliable.

### Data quality and CI protection

The missing keyword was "Orchestration". The semantic test failed because the RAG API response missed this key word in the meaning of kubernetes . Without CI, this degraded content would have been deployed to production and had the RAG system give incomplete answers which will only be noticed when users complain.

![Image](http://learn.nextwork.org/grateful_gray_shy_mouse/uploads/ai-devops-githubactions_i1j2k3l4)

---

## Testing Another Data Quality Issue

### Data quality and CI protection

---

## Scaling with Multiple Documents

I'm restructuring the project to handle multiple knowledge base documents. The new folder structure supports multiple files. This approach scales better becaus real world RAG apps often have hundreds or thousands of documents.

### Docs folder structure and CI scaling

The docs folder organizes files by storing all the knowledge base documents in one folder which allows chroma to embed any updated file in the folder. The embed_docs.py script handles multiple embedding of file that ends with".txt" in the docs folder. CI validated all documents and found that the response from the nextwork file does not pass the semantic test. This structure supports growth by handling multiple knowledge base documents.

![Image](http://learn.nextwork.org/grateful_gray_shy_mouse/uploads/ai-devops-githubactions_g5h6i7j8)

---

---
