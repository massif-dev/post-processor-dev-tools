![Massif Logo](massif-logo.png)

# Massif Post-Processor Developer Guide

A guide on how to setup your Git Repository and how to publish/manage your Post-Processors on the [**Massif Licensing Platform**](https://cps.cadpro.co.nz).

---

### Congratulations! 

You're on your way to becoming a Post-Processor developer on the Massif Licensing Platform! By following these steps, you can be up and running in no time:

1. Registering a Company/Organisation
2. Configuring your Git Repository
3. Structuring your Git branches (the Massif way)
4. Inviting the Massif-Bot to your Repository
5. Creating a Webhook to automate updates
6. Supporting versioning and revision notes
7. Publishing your Post-Processors
8. Managing/Updating your Post-Processors
9. Finances

---

### 1. Registering a Company/Organisation

The first step to becoming a `Vendor` on the Massif Platform is registering the Company or Organisation that you work for. This can be done in two ways:

1. If you or someone at your Company/Organisation has already purchased a product from the Massif App Store, your Company/Organisation will already exist. All you need to do now is ask your Manager to give you `Developer` access to your Company/Organisation.
2. If your Company/Organisation doesn't already exist, you can register your Company/Organisation on our [**Massif Developer Registration**](https://cps.cadpro.co.nz/developer) page. Follow the prompts to create your Client in our system, and in a few short minutes your Company/Organisation will be registered on the Massif Platform.

---

### 2. Configuring your Git Repository

The next step in the process is to configure your Git Repository details on your Vendor Account so that we can automate the delivery of your Post-Processors.

This requires a few quick steps, listed below:

* Sign in to the [**Massif Portal**](https://cps.cadpro.co.nz/admin) (this requires at least Developer privileges, so make sure your Manager has elevated your privileges).
* Choose the Company/Organisation that you want to manage, in the User-Dropdown box in the top-right of the page.
* Navigate to the `Developer` tab in the menu.
* Follow the on-screen instructions to complete your Repository setup (Hint: Check that the URL on-screen matches the URL of your project)
* We apologise if your Repository Manager is not currently supported, we are working on integrating as many Repository Managers as possible. If you don't see your Repository Manager on the list, please email us at support@cadpro.co.nz and let us know, as we would love to get your Post Processors on the Massif App Store.

---

### 3. Structuring your Git Branches (the Massif way)

Here at Massif, we have a strict Git Branch structure that allows us to optimize the delivery of your Post-Processors. We require that you abide by these rules so that we can provide the best service to your customers.

#### Branch Naming:

Branches should be named in the following format for standard Post-Processors:

``` 
vendor/{machine-vendor}/live   or   vendor/{control-vendor}/live
vendor/{machine-vendor}/beta   or   vendor/{control-vendor}/beta
vendor/{machine-vendor}/dev    or   vendor/{control-vendor}/dev

Example: vendor/okuma/live
```

or named in the following format for Client-specific Post-Processors:

``` 
client/{client-name}/live
client/{client-name}/beta
client/{client-name}/dev

Example: client/massif/live
```


where `{machine-vendor}` is the name of the Vendor who created the Machine that the Post-Processor is for, `{control-vendor}` is the name of the Vendor who created the Control that the Post-Processor is for and `{client-name}` is the name of the Client who the Post-Processor is being developed for.

All branch names should not include any whitespace characters, and should consist of all-lowercase letters. Our Platform will not recognise branches with names that do not adhere to these rules.

#### Why this structure?

Our Platform manages the delivery of your Post-Processors by looking at the branch name that Products are pointing to; this enables us to automate the delivery of updates when you push new changes to a branch (this will be covered in a coming section), to allow Customers to approve changes made to a Post-Processor in beta-mode, and allows the Platform to maintain a version history for your Post-Processors.

---

### 4. Inviting the Massif-Bot to your Repository

So that we can automate delivery of your Post-Processors to your customers, we need access to your Post-Processor Repository.

You will need to invite our automated Post-Processor delivery Bot into your Repository with read access so that it can send your Post-Processor code through an encrypted channel to your Customer's Desktop Applications.

Invite `massifbot` into your Post-Processors Repository with read access. 
Massif-Bot is best friends with our Massif-Mascot, Jack (our favourite chicken), hence the avatar photo.

---

### 5. Creating a Webhook to Automate Updates

In order for us to be able to keep your Customers updated, we need to know when new changes have been made available. That's where we introduce Webhooks - an easy way to monitor changes made to your Post-Processor code.

To create a webhook, follow the steps below:
* Navigate to your Repository Settings, and choose 'Webhooks'.
* Click 'Add webhook' (or equivalent), set the Webhook Triggers to 'Repository push' or equivalent, and set the URL to `https://cps.cadpro.co.nz/api/v1/bb/updates`.
* Click 'Save' to confirm creation of the Webhook.

Now any changes you make to Post-Processors in this Repository will be tracked by our Platform. Pretty cool, huh?

---

### 6. Supporting Versioning and Revision Notes

Versioning is an important part of the service that our Platform provides to your Customers, and you, the vendor. Versioning allows us to give your customers the choice to as to what revision of your Post-Processor code they wish to use.

A new Customer will be able to use any version of your Post-Processor, including versions that were created before they purchase a license for it.

Similar to Massif's branch structure and naming requirements, Massif has very strict versioning metadata that you must provide in your Post-Processor `.cps` file. To ensure that versioning will be supported by your Post-Processors, please make sure that this chunk of code below is included at the very top of any Post-Processor in your Post-Processor Repository:

```
/*
    ^^massifInfo: {
        "vendor": "{vendor-name}",
        "version": "v1.0.0",
        "release-notes": "First release."
    }^^
*/

description = "{post-processor-name}";
vendor = "{vendor-name}";
vendorUrl = "{vendor-url}";
longDescription = "{post-processor-description}";
```

where `{vendor-name}` is the name of your Company/Organisation, `{post-processor-name}` is the name of your Post-Processor, `{vendor-url}` is an optional URL to your website, and `{post-processor-description}` is a brief description of the functionality of your Post-Processor.

The first section, that is commented-out, contains the JSON required for the current version of the Post-Processor. Please ensure that this code remains in the same format in all commits. The `version` property should be incremented in every commit (beginning at `v1.0.0` for the first version), according to [Semantic Versioning Standards](https://semver.org/), and the `release-notes` property should contain a short description of the changes made to this version of the Post-Processor.

The variables `description`, `vendor`, `vendorUrl` and `longDescription` are displayed in Autodesk's CAD Applications when you are selecting which Post-Processor to use. These are not required, though they are recommended.

---

### 7. Publishing your Post-Processors

Congratulations! You're now ready to publish your first Post-Processor to the Massif App Store! Savour this moment, there's nothing quite like it!

Here are the steps to publish your Post-Processor:

- Sign in to the [**Massif Portal**](https://cps.cadpro.co.nz/admin) and navigate to the `Products` tab in the menu.
- Click the 'Add New Product' button.
- Complete the Product Registration form:
    * Ensure that you choose `Post Processor` as the product type.
    * Choose the corresponding branch that the Post-Processor is stored in.
    * Choose the correct `.cps` file for the Post-Processor.
    * Make sure to upload images for both a logo and sample NC code from output of the Post Processor (the logo is typically the logo of the `machine-vendor` or `control-vendor`)
    * It is recommended that you complete as many fields in the registration form as possible, as this makes it easier for your potential/existing customers to understand how your Post-Processor works.
    * If you have any issues with this process, please contact us at support@cadpro.co.nz
- Visit the [**Massif App Store**](https://cps.cadpro.co.nz/post-processors) and check that your Post-Processor is now available for purchase with the correct pricing and information.

Nice one! Now licenses for your Post-Processor are available to anyone on the Platform! We hope that you have an influx of sales and that you continue to develop more Post-Processors to sell on our platform.

Before you're done, please read these last two important sections (one of which involves payments).

---

### 8. Managing/Updating your Post-Processors

Once your Post-Processor has been published, you can update the information about the Post-Processor at any time, including the price. 

#### Please Note: We encourage you to consider what customers would be willing to pay for your Post-Processors before modifying the price.

You can update your Post-Processor information at any time through the [**Massif Portal**](https://cps.cadpro.co.nz/admin) in the `Products` tab.

As mentioned earlier, please make sure that any new commits for a Post-Processor in the `live` branch contain an updated version number and updated release notes.

> We are committed to making the process of managing and maintaining your Post-Processors as easy as possible. That is why we have a range of useful tools in development that we hope will make this process easier for you. Updates on these tools can be seen on the developer page on the [**Massif App Store**](https://cps.cadpro.co.nz/developer).

---

### 9. Finances

As we transition to a fully-fledged E-Commerce Platform, we are also transitioning to an automated funds delivery model for our Vendors through the tech giant, [**Stripe**](https://stripe.com).

However, this is not a simple or easy transition, and we want to make sure that we get it right the first time. It is for this reason that we are choosing not to offer any automated delivery of funds to our Vendors at this time. We will keep all of our developers up-to-date with our progress on automated fund-delivery on our developer page on the [**Massif App Store**](https://cps.cadpro.co.nz/developer). 

As an alternative to automated-delivery of funds, our accountants will manage all payments for licenses for your Post-Processors, and will transfer the required funds into your bank account. Please review the Massif Licensing Margins in the table below:

> | Developer Margin | Reseller Margin | Platform Margin |
> | :--------------: | :-------------: | :-------------: |
> | 70%              | 20%             | 10%             |

#### Disclaimers

- Any local or international tax is to be paid by the Developer, not the Reseller or the Platform, as specified in the Developer Registration Terms and Conditions.
- Massif Limited is not responsible for changes in market rates, resulting in unexpected fluctuations in currency-conversion rates. This is a known risk.

---

## Good luck, see you on the Platform!

---

## License

Copyright 2019 - **Massif Limited.**