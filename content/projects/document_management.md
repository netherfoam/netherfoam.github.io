+++
title = 'RedEye DMS'
date = 2015-05-11
draft = false
+++

### Role
I was a junior developer on the RedEye DMS project. I was responsible for feature development and bug fixes. As I had a
talent for MySQL having used it a number of times before, I was also responsible for optimisation of some complex MySQL 
queries.

## Tech Stack
* PHP 5.4+ / Symfony 2.6+
* MySQL / ElasticSearch / Redis

## Background
RedEye DMS is a document management system for engineering drawings. It is used by large engineering firms to manage
their drawings and revisions. It is a web application that allows users to upload, download, view and edit drawings.
These drawings come in an enormous variety of formats. Including images, PDFs, TIFFs, AutoCAD files, and many more.
A significant part of this product is about the workflow management of these drawings and the ability to track their
lifecycle.

## Challenges & Solutions
**Workflow Queue Optimisation** was a personal challenge for myself. The users workflow queues became very slow as the
product grew. Whenever a new client was onboarded, they would bring all of their drawings with them. This meant at
one point, there were millions of drawings being imported every week. The workflow queues were not optimised for this
scale of data, as they were written early in the product's life. I was able to optimise the workflow queues by using
my knowledge of MySQL behaviour and some integration tests to ensure that the optimisations improved load speed and
did not break any existing functionality. This was more than just adding indexes, but included changing the way many
of the queries were written to be more efficient.

