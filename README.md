# django-github-actions-aws
demonstrates how to set up a CI/CD Pipeline with GitHub Actions and AWS in a Django project

# What is a CI/CD Pipeline?
A CI/CD Pipeline is simply a development practice. It tries to answer this one question: How can we ship quality features to our production environment faster? In other words, how can we hasten the feature release process without compromising on quality?

The diagram below depicts a typical feature delivery cycle with or without the CI/CD pipeline.
<img style="height:400px; " src="https://github.com/ELIJAHKUNGU/django-github-actions-aws/blob/master/Activity-diagram.jpeg" />


# What are GitHub Actions?
In the CI/CD Pipeline, GitHub Actions is the entity that automates the boring stuff. Think of it as some plugin that comes bundled with every GitHub repository you create.

The plugin exists on your repo to execute whatever task you tell it to. Usually, you'd specify what tasks the plugin should execute through a YAML configuration file. Whatever command you add to the configuration file, will translate to something like this in plain English:

"hey GitHub Actions, each time a PR is opened on X branch, automatically build and test the new change. And each time a new change is merged into or pushed to X branch, deploy that change to Y server."

At the core of GitHub Actions lies five concepts: jobs, workflows,  events, actions, and runners.

Jobs are the tasks you command GitHub Actions to execute through the YAML config file. A job could be something like telling GitHub actions to build your source code, run tests, or deploy the code that has been built to some remote server.

Workflows are essentially automated processes that contain one or more logically related jobs. For example, you could put the build and run tests jobs into the same workflow, and the deployment job into a different workflow.

Remember, we mentioned that you tell GitHub Actions what job(s) to execute through a configuration file right? GitHub Actions considers each configuration file that you put in some folder in your repo a workflow. We will talk more about this folder in the next part.

So, to create a separate workflow for the deployment job and then a different workflow that combines the build and tests jobs, you'd have to add two config files to your repo. But if you are merging all the three jobs into a single workflow, then you'd need to add just one config file.

Events are literally the events that trigger the execution of a job by GitHub Actions. Recall we mentioned passing jobs to be executed through a config file? In that config file you'd also have to specify when a job should be executed.

For example, is it on-PR to main? Is it on-push to main? is it on-merge to main? A job can only be executed by a GitHub Action when some event happens.

Okay, let me quickly correct myself. It's not always the case that some event has to happen before a job could be executed. You could schedule jobs too.

For example, in your config file, instead of specifying that the event that should trigger the execution of, let's say, the build-and-test job, you could schedule it to happen a 2am everyday. In fact, you could both schedule a job and specify an event for that same job.

Actions are the reusable commands that you can reuse in your config file. You can write your custom actions or use existing ones.

A runner is the remote computer that GitHub Actions uses to execute the jobs you tell it to.

For example, when the build-and-test job is triggered based on some event, GitHub Actions will pull your code to that computer and execute the job.

The same thing happens in the case of the deployment job. The runner triggers the deployment of the built code to some remote server you specify. In our case, we will be using a service called AWS.


# What is AWS?
AWS stands for Amazon Web Services. It is a platform owned by Amazon, and this platform allows you access to a broad range of cloud computing services.

Cloud computing – I thought you said no big words? Most times businesses and even individual developers build applications just so other people can use them. For that reason, these applications have to be available on the interwebs.


# Prerequisites
A Django project setup locally with at least one view that returns some response defined.
A testcase written for the view(s) you've defined.
I have created a demo Django project which you can grab from this repository:


```  
  git clone https://github.com/Nyior/django-github-actions-aws 
 
```

After you download the code, create a virtualenv and install the requirements via pip:
```
pip install -r requirements.txt

```