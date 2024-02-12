---
layout: page
title: Product Overview
permalink: /product-overview/
toc: true 
---
*The following is an introduction page for a test automation platform. Its purpose is to provide developers a brief overview of the platform and its core concepts.*

*Note: The links in this example are placeholders (not active), to demonstrate how a customer would learn more about a given topic*

## What is Costanza?

Costanza is a test automation platform that runs integration and load tests against your cloud-based applications. It automatically configures your test infrastructure, orchestrates your test runs, and reports your test results all within your cloud account.

## How it works
Costanza is used as an approval workflow in your continuous delivery pipeline. When the approval workflow is triggered, Costanza automatically configures testing resources to create a test execution and reporting infrastructure. 

After setting up the infrastructure, it executes your tests and reports the results back to the approval workflow. If your tests *pass*, the approval workflow succeeds, and your changes are promoted to the next stage in your pipeline. If your tests *fail*, the approval workflow fails, and your changes are not promoted until it runs again and succeeds.

The following is a high-level overview of how Constanza works.

<img src="{{"/assets/costanza_workflow.jpg" | prepend: site.baseurl | prepend: site.url}}" alt="Overview of Constanza workflow" />

## Core Concepts

Before getting started with Costanza, you should become familiar with the following concepts.

### AccessRole
An [AccessRole](link) is an entity that you create in your cloud account to grant permissions to a user or service. Each role is assigned a [permission policy](link) that specifies what the role can and cannot do within the account (for example, create new resources, read/write privileges).

Costanza requires the creation of multiple AccessRoles to automatically configure your testing infrastructure, execute your tests, and report your test results. 

For more information about the specific roles and permission policies, see [Create AccessRoles](link).

### InfrastructureConfiguration
The [InfrastructureConfiguration](link) is a Costanza created entity that automatically configures the testing resources in your cloud account. When the Costanza approval workflow is invoked, it creates the InfrastructureConfiguration using the assigned AccessRoles.

For more information about enabling the InfrastrucutureConfiguration creation process in your approval workflow and the test resources that get created in your account, see [Enable InfrastructureConfiguration](link) and [Manage your Test Resources](link).

### TestDefinition
The [TestDefinition](link) is a collection of test parameters that you declare in your approval workflow. These parameters provide the information that Costanza needs to successfully create your InfrastructureConfiguration, orchestrate your tests runs, and report your test results. 

For more information about creating a TestDefintion and the available parameters, see [Create a TestDefiniton](link).

## Getting started
To start using Costanza, see one of the following guides:

* [Existing Pipeline Setup](link):
    This guide provides step-by-step instructions to add a Costanza approval workflow to an existing pipeline.

* [New Pipeline Setup](link):
    This guide provides an example template to create a new pipeline that includes a Costanza approval workflow.

If you want to learn more about how to use Costanza after getting started, see [Working with Costanza](link).