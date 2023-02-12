---
# An instance of the Experience widget.
# Documentation: https://wowchemy.com/docs/page-builder/
widget: experience

# This file represents a page section.
headless: true

# Order that this section appears on the page.
weight: 20

title: Experience
subtitle:

# Date format for experience
#   Refer to https://wowchemy.com/docs/customization/#date-format
date_format: Jan 2006

# Experiences.
#   Add/remove as many `experience` items below as you like.
#   Required fields are `title`, `company`, and `date_start`.
#   Leave `date_end` empty if it's your current employer.
#   Begin multi-line descriptions with YAML's `|2-` multi-line prefix.
experience:
  - title: "Insights & Data Consultant"
    company: "Capgemini"
    company_url:  'https://www.capgemini.com/no-no/'
    location: Oslo, Norway
    date_start: '2021-12-01'
    date_end: ''
    description: |2-
      Consulting on a project involving building a seamless data platform. Data Engineering tasks consisting of building a delta lake using Azure Data Factory and Databricks.

      * Crated dynamic and modularized notebooks using PySpark
      * Incorporated medallion architecture and Unity Catalog 
      * Created orchestration pipelines in ADF 
    
  - title: Junior Data Engineer
    company: HeltHjem
    company_url: 'https://helthjem.no'
    location: Oslo, Norway
    date_start: '2020-11-01'
    date_end : '2021-07-01'
    description: |2-
      Built AWS data warehouse using:

      * SQS
      * S3
      * Athena
      * Glue
      * Lambda
      * CloudWatch Events
      * QuickSight

  - title: Data Consultant
    company: HeltHjem
    company_url: 'https://helthjem.no'
    location: Oslo, Norway
    date_start: '2020-08-01'
    date_end: '2020-11-01'
    description: |2-
      Created tech related MVP's based on feedback from employees ranging from automated scripting of file dwonloads to a website tracking packages. 

design:
  columns: '1'
---
