# Deploying a Static Website in AWS: The Cloud Resume Challenge.

## Table of Contents.
- [Introduction](#introduction)
- [Step-by-Step Guide](#step-by-step-guide)
  - [Writing HTML and CSS Resume](#1-writing-html-and-css-resume)
  - [Deploying on AWS](#2-deploying-on-aws)
      -  [Creating an Architecture Diagram](#2-creating-an-architecture-diagram)
      -  [Hosting Resume on S3](#3-hosting-resume-on-s3)
      -  [Setting Up Route 53](#4-setting-up-route-53)
      -  [Securing the Site with ACM and CloudFront](#5-securing-the-site-with-acm-and-cloudfront)
- [Challenges Faced](#challenges-faced)
- [Key Takeaways](#key-takeaways)
- [Resources](#resources)
- [Outcome](#outcome)

## Introduction.
The Cloud Resume Challenge was created as a projects for beginners in the cloud to practice deploying resources in the cloud, so as to gain hands-on experience. It is a great way to demonstrate your understanding of the cloud, and many have landed roles as Junior Cloud Engineers due to this project. 
The challenge aims to host a static website on AWS using ervices such as S3, CloudFront and Route 53. This guide details the steps taken to complete this challenge including code snippets, configurations, and screenshots. By following this guide, you can create and host your own cloud-based resume.

**View my Resume [here](meghanmaina.buzz)

## Step-by-Step Guide.

### 1. Writing HTML and CSS Resume.
Create your resume using HTML and CSS. You can use an IDE such as Visual Studio Code to do this.
#### Steps:
1. **Set up your project directory**:
   ```sh
    mkdir cloud-resume
    cd cloud-resume
    ```
2. **Initialize a Git repository**:
    ```sh
    git init
    ```
3. **Create HTML and CSS files**.
   - You can view my files above for reference:[HTML](https://github.com/celineMaina/AWS-Cloud-Resume/blob/main/index.html) and [CSS](https://github.com/celineMaina/AWS-Cloud-Resume/blob/main/styles.css)
4. **Push the code to GitHub**:
    ```sh
    git add .
    git commit -m "Initial commit"
    git remote add origin <your-repo-url>
    git push -u origin master
    ```
## 2. Deploying on AWS.

### 1. Create an Architecture Diagram.
You can use tools like [draw.io](https://draw.io/) and [LucidChart](https://www.lucidchart.com/pages/) to draw a diagram that illustrates your cloud environment and how the components interact with each other. 
#### Architecture
![Cloud Resume Architecture drawio](https://github.com/user-attachments/assets/28ebb4f3-e205-4ed0-93b7-b742b03dab8d)

When a user searches for your domain name on their browser, Route 53 translates the domain name into the correct IP address and directs the request to the Cloudfront distribution. Cloudfront then quickly retrieves the resume files from the nearest edge location ensuring fast delivery. These files are stored in Amazon s3 securely and are secured by a secure HTTPS connection managed by Amazon Certificate Manager (ACM).

### 2. Hosting your Resume on S3.

1. **Create an S3 bucket**:
   - Go to the S3 console.
    - Click "Create bucket".
    - Enter a unique bucket name and select your region. Your bucket name should be the same name as your domain.
    - Disable "Block all public access" and acknowledge the warning.
2. **Upload your website files**:
    - Click on your bucket name.
    - Click "Upload" and add your `index.html` and `styles.css` files.

3. **Enable static website hosting**:
    - Go to the bucket properties.
    - Click "Edit" in the Static website hosting section.
    - Select "Enable" and set the index document to `index.html`.

 ### 3. Setting up Route 53.
 Route 53 is used as a DNS provider. Make sure you have a custom domain name as free domains on platforms such as Netlify are good, but won't work in this case. Here are the steps for setting up Route 53:
 1. **Create a hosted zone** in Route 53:
    - Go to the Route 53 console.
    - Click "Create hosted zone".
    - Enter your domain name and click "Create".

2. **Update nameservers**:
    - Go to your domain registrar.
    - Replace the default nameservers with those provided by Route 53.
  
### 4. Secure your Site with ACM and Create your CloudFront Distribution.
You might notice that your website is not secure. To secure it, request a free certificate from Amazon Certificate Manager by following these steps:
**Request a certificate in ACM**:
    - Go to the ACM console.
    - Click "Request a certificate".
    - Enter your domain name and follow the validation steps.

You use CloudFront to deliver your website content: [CloudFront Docs](https://aws.amazon.com/blogs/networking-and-content-delivery/amazon-s3-amazon-cloudfront-a-match-made-in-the-cloud/)
1. **Create a CloudFront distribution**:
    - Go to the CloudFront console.
    - Click "Create Distribution".
    - Select "Web" and enter your S3 bucket as the origin.
    - In the "SSL Certificate" section, select the ACM certificate you created.

2. **Update Route 53 records**:
    - Go to your hosted zone in Route 53.
    - Create an alias record that points to your CloudFront distribution.
  
## Challenges Faced.
During this project, I encountered several issues:
- **CloudFront Distribution Setup**. I encountered an issue when I tried to create my CloudFront distribution. I solved this but contacting support and requesting for a limit increase.

![Cloudfront error](https://github.com/user-attachments/assets/3d77b015-ae17-4c2f-8425-7897c8556f43)

## Key Takeaways.
From this challenge, I learned:
- How to use various AWS services together to host a static website.
- How to secure your site with SSL/TLS certificates.
- How to use Route 53 for DNS management.

## Resources.
- [Cloud Resume Tutorial](https://youtu.be/NiCZSdWucZE?si=DdrygfBilOfALuY6)
- [Hosting](https://www.hostafrica.ke/)

## Outcome.
By completing this challenge, I gained practical experience with AWS services and enhanced my understanding of cloud architecture. This documentation serves as a comprehensive guide for anyone looking to undertake the Cloud Resume Challenge.
