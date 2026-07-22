# Qualtrics Switchboard Survey

A Qualtrics framework for linking multiple surveys through a single anonymous survey link while preserving participant confidentiality. Download the template Qualtrics files (.qsf) and try it out yourself!

# Overview

The Switchboard Survey is a Qualtrics-based system that allows researchers to connect responses across multiple surveys without creating and managing large numbers of Qualtrics personal links.

# The Switchboard Survey works by:

Generating a unique participant identifier (UniqueID).

Embedding one or more Qualtrics surveys (Endpoint Surveys) using iframes.
Passing the UniqueID to each Endpoint Survey through URL parameters.
Storing data separately within each Endpoint Survey.
Allowing researchers to merge datasets later using the shared UniqueID.

# This approach enables:

Longitudinal studies
Pre/post intervention studies
Multi-participant household studies
Screening and recruitment workflows
Separation of identifying information from survey responses

# How It Works
## Switchboard Survey

The Switchboard Survey acts as a container survey that presents one or more Endpoint Surveys within a single participant experience.

## Endpoint Surveys

Endpoint Surveys are standard Qualtrics surveys embedded into the Switchboard Survey via iframes.

# Quick Implementation Guide: Qualtrics Switchboard Survey

## Before You Begin

* Create all Qualtrics surveys that will serve as **Endpoint Surveys** (e.g., consent, demographics, weekly survey).
* Create a separate blank Qualtrics survey that will serve as the **Switchboard Survey**.

## Step 1: Create the UniqueID Embedded Variable

* Open **Survey Flow** in the Switchboard Survey.
* Add an **Embedded Data** element.
* Create a field named **UniqueID**.
* Move the Embedded Data element to the top of the Survey Flow.
* Repeat this process in every Endpoint Survey that will receive the UniqueID.

## Step 2: Generate a UniqueID

* In your first question in the Switchboard Survey.
* Open the question's **JavaScript Editor**.
* Paste the UniqueID generation JavaScript.
* Save the code.
* As the UniqueID cannot be passed in the same page as it is generated you must have multiple pages in your survey.

## Step 3: Obtain Endpoint Survey Links

* Open each Endpoint Survey.
* Navigate to **Distributions**.
* Select **Get a Single Reusable Link**.
* Copy the **Anonymous Link**.
* Save these links for use in the iframe code.

## Step 4: Embed the First Endpoint Survey

* Add a **Text/Graphic** question to the Switchboard Survey.
* Open **HTML View**. Note: You must always edit these questions in HTML View. Editing them in the normal Rich Text Editor will cause the HTML to truncate, losing it's functionality.
* Paste the iframe template.
* Replace "PASTE LINK HERE" with the Endpoint Survey anonymous link.
* Confirm that the URL is followed by:

  * `?UniqueID=${e://Field/UniqueID}`

## Step 5: Add Completion Trigger to the Endpoint Survey

* Open the final question of the Endpoint Survey.
* Open the **JavaScript Editor**.
* Paste the completion-trigger JavaScript.
* Save the code.
* Publish the Endpoint Survey.

## Step 6: Add Additional Endpoint Surveys (Optional)

* Create another Text/Graphic question in the Switchboard Survey.
* Insert a new iframe template.
* Replace the link with the next Endpoint Survey.
* Repeat for all Endpoint Surveys.

## Step 7: Implement Branching or Loop & Merge (Optional)

### For Different Respondent Types

* Create a question that determines respondent type (e.g., age group, participant role, password).
* Use **Survey Flow Branch Logic** to display the appropriate Endpoint Surveys.

### For Repeated Surveys

* Create a question that determines the number of repetitions.
* Enable **Loop & Merge** on the Endpoint Survey block.
* Configure loops using the question.

## Step 8: Test the Survey

* Preview the Switchboard Survey.
* Confirm that:

  * A UniqueID is generated.
  * The Endpoint Survey appears inside the iframe.
  * The Switchboard "Next" button remains hidden until the Endpoint Survey is completed.
  * The correct Endpoint Surveys appear based on branching logic.
  * Loop & Merge functions as expected.

## Step 9: Publish and Distribute

* Publish the Switchboard Survey.
* Distribute only the Switchboard Survey anonymous link.
* Participants should never receive Endpoint Survey links directly.

## Step 10: Analyze and Merge Data

* Download data from each Endpoint Survey separately.
* Locate the **UniqueID** variable in each dataset.
* Merge datasets using UniqueID in Excel Power Query, R, SPSS, SAS, or another statistical package.
* Verify that records match correctly across Endpoint Surveys.

If you use the Switchboard Survey in your research, please cite:
Atkinson, E., et al. The Switchboard Survey: The Solution to Tracking Personal Links Across Qualtrics Surveys. (Manuscript in review).
