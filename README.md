<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Secure Secrets with Secrets Manager

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-secretsmanager)

**Author:** Abdulrahman Abdulkadir  
**Email:** abdabdulkadir62@gmail.com

---

![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-security-secretsmanager_r7s8t9u0)

---

## Introducing Today's Project!

In this project, I will demonstrate Securing Secrets with Secrets Manager  I'm doing this project to learn how to use AWS Secrets Manager to securely store and retrieve secrets.

### Tools and concepts

Services I used were **AWS Secrets Manager**, **Amazon S3**, **Amazon GuardDuty**, **CloudWatch**, and **GitHub**. Key concepts I learnt include securely managing secrets, avoiding hardcoded credentials, detecting malware in S3 using GuardDuty, understanding how GitHub secret scanning protects exposed keys, and resolving Git merge conflicts. This project helped reinforce best practices for cloud security and secure application development.


### Project reflection

This project took me approximately 3 hours to complete. The most challenging part was resolving the Git merge conflict during the rebase,  especially while ensuring no sensitive data was accidentally committed. It was most rewarding to successfully integrate AWS Secrets Manager into the web app, replacing hardcoded credentials with a secure retrieval method, and seeing GitHub's secret scanning in action.


I did this project today to better understand how to manage secrets securely in cloud-based applications. It aligned perfectly with my goal of learning real-world AWS security practices, especially integrating Secrets Manager with code. The project met my goals by showing both insecure and secure methods, highlighting best practices and how services like GitHub and AWS work together to protect credentials.


---

## Hardcoding credentials

 In this project, a sample web app is exposing AWS credentials directly in the code. It is unsafe to hardcode credentials because anyone with access to the code—especially if it’s on a public repository—can steal those credentials and misuse them, leading to data breaches, resource abuse, or account compromise. Secure practices like using environment variables or AWS Secrets Manager are recommended instead.

 I've set up the initial configuration with fake AWS credentials in the `config.py` file, including an `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`. These credentials are just examples because they simulate a real-world scenario where sensitive keys are accidentally hardcoded into code—a major security risk that attackers often exploit when scanning public repositories.


![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-security-secretsmanager_j2k3l4m5)

---

## Using my own AWS credentials

---

## Pushing Insecure Code to GitHub

 Once I updated the web app code with credentials, I forked the repository because forking creates a separate copy of the original repository under my own GitHub account, allowing me to make changes and push code independently. A fork is different from a clone because a clone simply downloads the repository to my local machine, while a fork creates a new online version I can edit and push to directly on GitHub. This setup was necessary to see how GitHub handles exposed secrets in publicly shared code.

✍️ To connect my local repository to the forked repository, I used `git remote add origin` to set the destination where my code will be pushed on GitHub. Then I used `git add` and `git commit` tostage and save my changes locally, including the hardcoded credentials. Finally, `git push` uploads those committed changes from my computer to the forked GitHub repository, making the code publicly available online.


GitHub blocked my push because its secret scanning detected that I was trying to upload hardcoded AWS credentials. This is a good security feature because it helps prevent accidental exposure of sensitive information that could be exploited by attackers, even if the code was meant to be public. It acts as a safeguard to stop developers from unintentionally leaking secrets online.

![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-security-secretsmanager_o2p3q4r5)

---

## Secrets Manager

Secrets Manager is a secure AWS service used to store, manage, and retrieve sensitive information like API keys, passwords, and AWS credentials. I'm using it to store my AWS access key and secret access key securely, instead of hardcoding them into my application. Other common use cases include storing database credentials, third-party service tokens, and securing environment variables for cloud-native apps.


Another feature in Secrets Manager is secret rotation, which means automatically changing the stored secret on a regular schedule without needing manual updates. It's useful in situations where credentials need to be frequently refreshed for security, such as database passwords, API keys, or when following compliance requirements to reduce the risk of long-term credential exposure or misuse.


Secrets Manager provides sample code in various languages, like Python, JavaScript, and Java. This is helpful because it allows developers to easily retrieve secrets securely within their applications without writing complex code from scratch. It also ensures best practices are followed when accessing credentials, reducing the risk of accidentally exposing sensitive information.


![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-security-secretsmanager_h2i3j4k5)

---

## Updating the web app code

I updated the `config.py` file to retrieve AWS credentials securely from Secrets Manager instead of having them hardcoded. The `get_secret()` function will connect to AWS Secrets Manager, fetch the stored secret using the secret name, and parse the credentials (like access key and secret key) from the response so the application can use them safely.


I also added code to `config.py` to extract the access key ID and secret access key from the retrieved secret JSON. This is important because it allows the app to authenticate securely with AWS services without exposing credentials directly in the code, reducing the risk of accidental leaks or misuse.


![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-security-secretsmanager_v0w1x2y3)

---

## Rebasing the repository

Git rebasing is the process of moving or combining a sequence of commits to a new base commit. I used it to update my local branch history so it aligns with the upstream repository. This was necessary because the original repository had changes that I needed to integrate cleanly into my project, without creating unnecessary merge commits.


A merge conflict occurred during rebasing because both my local changes and the upstream repository modified the same part of the code, specifically the config.py file. I resolved the merge conflict by manually reviewing the conflicting code, keeping the secure implementation that retrieves credentials from AWS Secrets Manager, and removing the outdated hardcoded version. After editing, I marked the conflict as resolved using `git add` and continued the rebase with `git rebase --continue`.


Once the merge conflict was resolved, I verified that my hardcoded credentials were out of sight in the repository by checking the `config.py` file to ensure it no longer contained any plaintext keys. I also reviewed my Git commit history and confirmed that no sensitive information was present. Finally, I pushed the updated code to GitHub and verified that the Secrets Manager integration was in place and no security warnings were triggered.


![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-security-secretsmanager_t5u6v7w8)

---

---
