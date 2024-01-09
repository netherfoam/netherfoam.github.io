+++
title = 'Workforce Mobility'
date = 2016-01-01
draft = false
+++

## Role
I was the technical lead for the project (2016-2019), leading a development team of 4. We used an Scrum / Agile 
methodology and worked in person. I was responsible for the architecture of the system, as well as the development of 
the backend services. This was the first project where I was responsible for the code architecture, and I learnt a lot
about what worked well here.

## Tech Stack
* Java / Springboot / Hibernate
* PostgreSQL / ElasticSearch / Redis
* Docker / Mesos / AWS

## Background
The Workforce Mobility product was developed by RedEye Apps, a Brisbane based startup that develops software for large
asset owners. The product was responsible for managing a workforce which surveyed and maintained assets in the field.
These workers were often in remote locations with poor internet connectivity, so the product had to work offline via
iOS and Android mobile apps. The offline capability was always a significant challenge, determining what data to take
offline and how to recover during sync. The backend was my responsibility and was built on top of a Java / Springboot
stack, with a PostgreSQL database. We used ElasticSearch for searching and Redis for caching. The backend was deployed
through Docker containers on Mesos, and hosted on AWS.

The product pivoted into digital asset management using Autodesks Forge platform, which presented significant challenges
dealing with poorly constructed 3D models that were never intended to be viewed in a web browser. Nonetheless, we were
successful in delivering a product that allowed users to view and interact with 3D models in the browser. We even built
tools to automate the ingestion of 3D models as assets, picking apart internal objects and creating a searchable database
of assets from them that could be viewed, linked and edited through the platform.

## Challenges & Solutions
**3D model previews** was a significant challenge. To generate previews, we used the Forge Viewer inside a web browser,
running inside a docker container, which loaded and targeted components within the 3D model, and created a screenshot.
This was all done in batch ahead-of-time. This was a tricky project, as browsers typically aren't designed to run in
headless mode! For this, we made use of Puppeteer, which is normally a testing framework for browser control.

**Searching** was not a trivial problem either. We needed quality results, often with fuzzy matching and ranking. For
this, we leaned on ElasticSearch. We tracked changes in the PostgreSQL database and pushed updates to ElasticSearch.
This allowed us to have a fast, responsive search experience for users.

An **event driven architecture** was used to allow the code to scale. Since the project was a monolithic Springboot
application, we made use of Spring Events which allowed us to decouple components and scale them independently. With
a Maven multi-module project, we could easily enforce a classpath separation between components, and use Spring Events
to communicate between them. This meant modules were independant, unless explicitly stated, and could be added/removed
without any significant refactor of the application. This was a fantastic way to scale the application, and allowed us
to try out new concepts without significantly refactoring the codebase.

