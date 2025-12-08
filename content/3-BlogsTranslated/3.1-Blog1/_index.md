---
title: "Blog 1"

weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---


# Modernizing Java Applications with Amazon Q Developer and Visual Studio Code




<span style="font-size:13px; color: #737070ff;">
by Vimal Vyas and Shweta Singh | on 01 APR 2025 | in
</span>
<small>
<a href="https://aws.amazon.com/blogs/migration-and-modernization/category/amazon-q/" style="color:#0073bb; text-decoration:none;">Amazon Q</a>, 
<a href="https://aws.amazon.com/blogs/migration-and-modernization/category/amazon-q/" style="color:#0073bb; text-decoration:none;">Amazon Q Developer</a>, 
<a href="https://aws.amazon.com/blogs/migration-and-modernization/category/devops/aws-java-development/" style="color:#0073bb; text-decoration:none;">AWS Java Development</a>, 
<a href="https://aws.amazon.com/blogs/migration-and-modernization/category/devops/" style="color:#0073bb; text-decoration:none;">DevOps</a>, 
<a href="https://aws.amazon.com/blogs/migration-and-modernization/category/post-types/technical-how-to/" style="color:#0073bb; text-decoration:none;">Technical How-to</a> 
| <a href="https://aws.amazon.com/blogs/migration-and-modernization/modernizing-java-applications-with-amazon-q-developer-and-visual-studio-code/" style="color:#0073bb; text-decoration:none;">Permalink</a>
</small>


As time progresses, organizations continue using Java applications that were built many years ago using older versions of Java Development Kits (JDKs). This result in applications running deprecated code with outdated dependencies. This combination of factors might lead to security vulnerabilities, poor application performance and maintenance challenges. These challenges are increasingly difficult to manage in organizations running a large number of Java applications. Developers are looking for a development environment that facilitates running old Java applications with different JDKs; and tools that help migrate the application to the current Java version automatically, replacing the deprecated code and fix missing dependencies.

In April, 2024, Amazon Web Services (AWS) announced the general availability of Amazon Q Developer: Transform for Java. On February 14, 2025, Amazon Q Developer announced support for upgrades to Java 21. With this release, Amazon Q Developer: Transform adds a single-click transformation of old Java 8 and Java 11 applications to Java 21.

This post shows how to set up Visual Studio Code (VSCode) with multiple versions of JDK. Also, VSCode’s integration with Amazon Q Developer: Transform to automate the transformation of Java applications to current versions.

## Overview of the solution
The solution consists of the following steps to set up your development environment:

* Configure Visual Studio Code with multiple JDKs and Maven
* Integrate Visual Studio Code with Amazon Q Developer: Transform 

After you set up the development environment, use Amazon Q Developer: Transform feature to transform Java 8 or Java 11 applications to Java 21.

## Setting Up Your Development Environment
### Configure Visual Studio Code (VSCode) with Multiple JDKs
In VSCode, select the View/Command Palette then chose Java:Configure Java runtime and download JDK versions 8, 11 and 21.
As an option, use Amazon Corretto to download multiple versions of JDK. Amazon Corretto is a no-cost, multiplatform, production-ready distribution of OpenJDK.

![Translate blog 1](/images/3-BlogsTranslated/3.1-Blog1/hi.gif)

To install the Maven plugin, use VSCode Extensions, type or select Maven for Java and select Install.
![Translate blog 1](/images/3-BlogsTranslated/3.1-Blog1/hi1.gif)

Now add your Java applications built on Java 8 and Java 11 to a VSCode workspace. We are using sample java demo applications developed with Java 8 and Java 11 versions for this walkthrough. Make sure that the pom.xml file points to the applicable version of Java as shown in the following image.
![Translate blog 1](/images/3-BlogsTranslated/3.1-Blog1/hi3.gif)
 

### Integrating Visual Studio Code with Amazon Q Developer: Transform
Amazon Q Developer provides integration with multiple integrated development environments (IDEs) and VSCode is one of them. Follow the AWS documentation to integrate VSCode with Amazon Q Developer.

## Transforming Java Applications
### Java 8 to Java 21 Transformation
The following steps will guide you to perform the code transformation:

1. Choose Amazon Q in the navigation bar from the bottom panel of your VSCode.

2. Then select Open Chat panel from the command palette. In the chat panel, type /transform and then choose the Java 8 project to transform.

3. Now select source code version as 8 and target code version as 21. Choose Confirm.

4. A pop-up window will open titled choose to skip unit tests, select Skip unit tests and choose Confirm. We will skip unit test because there is a technical limitation where the project must be able to build and complete its tests within 55 minutes.

5. A new pop-up window opens and provides options to choose how to receive proposed changes. It provides the options One Diff and Multiple Diffs. Select One Diff for smaller-scale transformations with manageable code changes.

6. A final pop-up window opens to provide the command to find the JDK path. Run the command in a new terminal and then enter the path to JDK 8. Once you enter the JDK path, Amazon Q starts building your project. This can take up to 10 minutes depending on the size of your project.
![Translate blog 1](/images/3-BlogsTranslated/3.1-Blog1/hi4.gif)



### Review Transformation plan
Once Amazon Q Developer uploads and builds your code in a secure build environment, it generates a transformation plan. The transformation plan displays Java code details including lines of code, dependencies to replace, deprecated Java 8 code instances and number of files to be changed.

![Translate blog 1](/images/3-BlogsTranslated/3.1-Blog1/hi5.gif)

### Review Transformation Summary
Upon completion of the transformation, Amazon Q Developer generates a detailed transformation summary listing the dependencies, Java 8 deprecated code instances and list of all the files changed. The following instances of deprecated code were replaced by Amazon Q Developer.

![Translate blog 1](/images/3-BlogsTranslated/3.1-Blog1/hi2.jpg)

Amazon Q Developer summarizes the proposed changes in the Proposed Changes tab, that opens up after the transformation is complete. To accept the changes Amazon Q made, go to the Proposed Changes tab and choose Accept.
![Translate blog 1](/images/3-BlogsTranslated/3.1-Blog1/hi6.gif)


### Java 11 to Java 21 Transformation
To transform Java 11, follow the same steps described above. This time, select Java 11 as the source version. The process includes:

· Project selection and version specification

· Build environment setup

· Transformation plan review

· Accept the final changes

### Unit Testing
Enterprises also face challenges with high defect rates, quality issues, and long development cycles for new features and applications. Amazon Q Developer helps development teams achieve improvements in productivity by automating mundane tasks and reducing technical debt accumulation through the /test feature.

The /test feature in Amazon Q Developer is an automated unit test generation capability that helps developers create comprehensive test suites. The following is an example of creating a unit test:

![Translate blog 1](/images/3-BlogsTranslated/3.1-Blog1/hi7.gif)

To run the tests, navigate to the Testing tab, and select the generated java test class. From this testing tab, you have complete control to run any of the tests, either a single test case or multiple test cases.

## Benefits and Impact
Amazon Q Developer serves as a powerful AI-powered assistant that helps transform and modernize software development across the entire lifecycle delivering the following benefits –

· Accelerate code modernization

· Simplify dependency management

· Reduce technical debt

· Enhance application performance

· Streamline maintenance

## Conclusion
The Amazon Q Developer Agent for Code Transformation (QCT) for Java helps modernize legacy Java applications faster and more efficiently. This tool transforms outdated systems to current frameworks and deploys them as cloud-native applications on AWS. This process minimizes effort, risk, and ongoing maintenance needs. By using Amazon Q Developer, you’ll free up time and resources previously spent managing technical debt, allowing your team to concentrate on innovation and enhancing your newly modernized applications.

As demonstrated in this post, Developers can transform multiple java applications built on different JDK versions using Amazon Q Developer and VSCode. Developers can also leverage /test feature of Amazon Q Developer to quickly generate unit test cases. This tool reduces the complexity and time required to modernize legacy Java applications enabling developers to focus on innovation rather than maintenance.

