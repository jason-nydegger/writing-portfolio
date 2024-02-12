---
layout: page
title: Program Overview
permalink: /program-overview/
---
*The following is a vision for a Technical Documentation Program. Its purpose is to describe the program scope and provide an overview of the documentation development infrastructure and tooling. This is intended to be landing page for an internal site (e.g., SharePoint, Wiki) for a technical documentation team and internal customers.*

*Note: The links in this example are placeholders (not active) to demonstrate how a customer would learn more about a given topic*

# Introduction
The Technical Documentation Program **manages the development of our internal and external facing technical documentation.** It implements content standards, operational processes, and development tools to create quality documentation in a consistent, efficient, trackable, and scalable manner.

# Mission
Our mission is to **establish a technical documentation center of excellence** that uses the latest technologies and best practices to deliver a world-class content experience to our customers.

# Guiding Principle
**Documentation is a product.** The development process follows a product development lifecycle—applying similar methodologies used to develop and manage software products. By aligning development practices, we create an environment where documentation is seamlessly integrated into product development consistently and efficiently.

# Overview
To deliver a world-class experience, we implement a **development and operations (DevOps) infrastructure** for planning, writing, managing, and releasing documentation. Using software development tools (for example, continuous integration and continuous deployment (CI/CD) workflows, Git), we are able to deliver consistent, efficient, trackable, and scalable documentation to our customers.

The following image is a functional overview of the Technical Documentation Program framework.

<img src="{{"/assets/tech_doc_program.jpg" | prepend: site.baseurl | prepend: site.url}}" alt="Overview of the technical documentation program" />

The DevOps infrastructure is built on a set of [Standards and Requirements](link) that define the scope, operations, and best practices for the program; this includes the program charter, style guide, DevOps requirements, and technical references. 

To create and deliver documentation, we use a [Development Platform](link). The platform includes the following components:

* Git repository for source control and collaborative development via branching.
* Dev environment to write and build documentation before committing (for example, local or virtual machine)
* Document builder to compile and render Markdown, XML, and API files into PDF or HTML files (for example, DocFX, Jekyll, Sphinx).
* CI/CD pipeline to build, test, and deploy the PDF or HTML files for publication.

To manage activities and program deliverables, we follow a [Documentation Development Lifecycle](link) (plan, research, develop, review, and release). Using DevOps tooling, we create and prioritize deliverables using a work item backlog and a delivery board to assign, track, and report the status of active work items.

To ensure we deliver the best documentation experience, we manage a [Customer Advocacy Program](link) that implements different methods to collect feedback and issues from our customers. The methods include an online ticketing system, on-page feedback options, customer outreach, and customer to stakeholder feedback loop.

# Getting Started
Before you start contributing, we recommend reading the following resources:

* [Style Guide](link)
* [Best Practices](link)

To start contributing, see the following how-to resources:

* [Contribute to existing documents](team)
* [Create new documents](team)
* [Perform a document review](team)
* [Troubleshooting](team)

# Contact us

We’re here to help! If you have questions or want to chat about documentation, contact us using the following:

* Email: [techdocs@awesome.com](link)
* Teams Channel: TechDocs
* [Submit a documentation request](team)
