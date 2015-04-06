# Introduction

Many of Salsify’s customers come to Salsify with lots of various data in lots of various data sources. These sources might be digital assets (manuals, product images, color swatches, etc) stored in a digital asset management system (best), a shared drive (better), or on a particular employee’s laptop (worse), or they may be product information stored in an enterprise resource planner, an Excel spreadsheet, or a series of PDF files, among other sources and systems.

Consequently some of the work we do in Customer Success Engineering is helping customers integrate with existing business systems (and/or business processes). Which brings us to this exercise.

In this exercise you’ll build code/an integration to upload digital assets to a customer Salsify account. As part of it you’ll learn to upload product data into Salsify, how to work with Salsify’s APIs, and how to handle an integration of asset data with products in Salsify.

# Specification

Your code should, given a set of products and a library of digital assets:
* Determine what products are in the system
* Determine what assets are available in the library (we’re providing you with a ZIP file)
* Upload the assets that match the product name to the product in the system

Products have an associated external identifier, or ‘sku’. Images are named after this ‘sku’, like so:
* `sku`_Primary.jpg is the primary image for the product identified by `sku`
* `sku`_LeftSideView.jpg is the Left side view image for the product identified by `sku`
  
Images without a sku prefix, or with a sku that isn’t found shouldn’t be uploaded.

You are free to use whatever language and framework you would like, however, we primarily use Ruby (on Rails), Scala, and Javascript.

# Salsify API Documentation
Go here: http://help.salsify.com/category/56-category

In general, Salsify allows you to export product information in CSV form and then import it back in CSV form (or in Excel, but CSV should be a bit easier to handle programmatically). 

# What you should submit

A zip file or an invitation to a source code repository we may access (BitBucket provides free Git hosting) that contains:

1.  A file, build.sh that will do any pre-run steps to setup an environment (build code, run Ant, maven, bundle, etc).
2.  A file, run.sh that will actually upload images to salsify. We expect it to:
  1.  Contact Salsify via an API to determine what products are in the system
  2.  Access it’s image library via a directory, images, that is relative to itself
  3.  Provide some information to the user as to what it accomplished.
3.  A file, README, which documents the general approach to what your code does. In it you should cover:
  1.  How does your system work? (if not addressed in comments in source)
  2.  How will your system perform with 100 products? 1000 Images? 10,000 products and 1 million images?
  3.  What documentation, websites, papers, etc did you consult in doing this assignment?
  4.  What third-party libraries or other tools does the system use? How did you choose each library or framework you used?
  5.  What was your testing strategy? What automated tests did you write? What would you test if given more time?
  6.  How long did you spend on this exercise? If you had unlimited time to spend on this, how would you spend it and how would you prioritize each item?
  7.  If you were to critique your code, what would you have to say about it?
4.  The rest of the files should be the source code to the system.

# Hints and tips

* Salsify doesn’t have an exposed direct image upload API. You can import and export data, but image files can’t directly be uploaded via a public API. In order to upload images in bulk you must upload a CSV or Excel file with publically accessible URLs of images assigned to products (see the sample .csv file).
* To get publically accessible URLs for images some service must be used. We recommend Amazon S3 (which has a great Ruby API), and you can get a free account here: https://aws.amazon.com/free/
* Imports in Salsify overwrite existing data (for properties specified in the import file). If you need to clear all the data in the account however, you can click on your name in the top right, go to Organization, then Data, and click on 'Clear All Data'

# General suggested approach

* Accept your invitation link to Salsify (it will be provided)
* Checkout the product and the sample data provided (`product_data.csv` in this repository; it will already be imported into the account)
* Write code to:
  * Download the product data as Salsify sees it using the ephemeral export API
  * Upload images for products in the export to get publically accessible urls (sample simples in `assets.zip` in this repository)
  * Attach those images to products in Salsify by importing the public asset urls (via the Product Bulk Import API)

# What you’ll be judged on

* Did you complete the task assigned? Are the images uploaded and attached to the right products?
* Were you able to clearly document how the system works and any gotchas associated with it?
* Is the design scalable? In performance and in feature set? How easy is it to understand the code?
