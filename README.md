# Actor - BBB Scraper

## BBB scraper

Since BBB doesn't provide a good and free API, this actor should help you to retrieve data from it.

The BBB data scraper supports the following features:

-   Search any keyword - You can search any keyword you would like to have and get the results

-   Scrape companies - Extract any company information with all of its detail.

-   Scrape categories - Gather businesses for each of the categories.

-   Search for anything - If you want to get filtered data for the search results, just type the URL.

-   Retrieve reviews - BBB Scraper provides reviews for all the companies.

## Bugs, fixes, updates and changelog

This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/epctex/BBB-scraper/issues).

## Input Parameters

The input of this scraper should be JSON containing the list of pages on BBB that should be visited. Possible fields are:

- `search`: (Optional) (String) Keyword that you want to search on BBB.

- `country`: (Optional) (String) Country you want to search.

- `location`: (Optional) (String) Location you want to search.

- `startUrls`: (Optional) (Array) List of BBB URLs. You should only provide news list, jobs list or detail URLs.

- `includeReviews`: (Optional) (Boolean) This will add all the reviews that BBB provides inside the book object. Please keep in mind that the time and resources the actor uses will increase proportionally by the number of reviews.

- `endPage`: (Optional) (Number) Final number of page that you want to scrape. Default is `Infinite`. This is applies to all `search` request and `startUrls` individually.

- `maxItems`: (Optional) (Number) You can limit scraped items. This should be useful when you search through the big lists or search results.

- `proxy`: (Required) (Proxy Object) Proxy configuration.

- `extendOutputFunction`: (Optional) (String) Function that takes a JQuery handle ($) as argument and returns object with data.

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use [Apify Proxy](https://www.apify.com/docs/proxy).

## Tip

**Please keep in mind that BBB.org blocks all the requests that are not coming from Canada, US and Mexico. That's why you should select a proper proxy group according to that.**

When you want to have a scrape over a specific listing URL, just copy and paste the link as one of the **startUrl**.

If you would like to scrape only the first page of a list then put the link for the page and have the `endPage` as 1.

With the last approach that explained above you can also fetch any interval of pages. If you provide the 5th page of a list and define the `endPage` parameter as 6 then you'll have the 5th and 6th pages only.

### Compute Unit Consumption

The actor optimized to run blazing fast and scrape many as listings as possible. Therefore, it forefronts all listing detail requests. If actor doesn't block very often it'll scrape 100 listings in 2 minutes with ~0.03-0.05 compute units.

### BBB Scraper Input example

```json
{
    "startUrls": [
        "https://www.bbb.org/us/ny/new-york/category/home-improvement",
        "https://www.bbb.org/us/ny/new-york/categories",
        "https://www.bbb.org/us/ny/new-york/profile/home-builders/jf-hughes-builders-inc-0121-87134180",
        "https://www.bbb.org/search?find_country=USA&find_entity=66005-000&find_id=1099_2800-400-1100&find_latlng=40.762801%2C-73.977818&find_loc=New%20York%2C%20NY&find_text=Clean%20Up%20Services&find_type=Category&page=1&sort=Relevance"
    ],
    "search": "business",
    "location": "new york",
    "country": "USA",
    "includeReviews": true,
    "proxy": {
        "useApifyProxy": true
    },
    "endPage": 5,
    "maxItems": 100
}
```

## During the Run

During the run, the actor will output messages letting you know what is going on. Each message always contains a short label specifying which page from the provided list is currently specified.
When items are loaded from the page, you should see a message about this event with a loaded item count and total item count for each page.

If you provide incorrect input to the actor, it will immediately stop with failure state and output an explanation of what is wrong.

## BBB Export

During the run, the actor stores results into a dataset. Each item is a separate item in the dataset.

You can manage the results in any languague (Python, PHP, Node JS/NPM). See the FAQ or <a href="https://www.apify.com/docs/api" target="blank">our API reference</a> to learn more about getting results from this BBB actor.

## Scraped BBB Output

The structure of each item in BBB looks like this:

### Business Detail

```json
{
    "type": "Business",
    "URL": "https://www.bbb.org/us/ny/new-york/profile/cleaning-services/bes-services-ny-llc-0121-185529/details",
    "Logo": "https://www.bbb.orghttps://www.bbb.org/ProfileImages/639c1a3e-a8d1-4649-a705-41dca8bee2ea.png",
    "Company Name": "BES Services NY LLC",
    "Categories": ["Cleaning Services"],
    "Social Links": null,
    "Address": {
        "Country": "USA",
        "City": "New York",
        "State": "NY",
        "Zip Code": "10032",
        "Address": "725 W 172nd St. Suite 23",
        "Latitude": "40.839194",
        "Longitude": "-73.942591",
        "Phone Number": "(718) 915-5148"
    },
    "Contact": "Ms. Barbara Brown, undefined",
    "BBB File Opened:": "10/1/2019",
    "Years in Business:": "2",
    "Business Started:": "3/15/2019",
    "Business Incorporated:": "3/15/2019",
    "Accredited Since:": "10/15/2019",
    "Type of Entity:": "Limited Liability Company (LLC)",
    "Description": "BES Services NY LLC offer residential and commercial cleaning services.&nbsp",
    "Business Rating": "A",
    "Headquarters URL": null,
    "Accreditation": true,
    "reviews": [
        {
            "author": "Ivonne M",
            "rating": "(5 stars)",
            "date": "03/03/202003/06/2020",
            "body": "This company is the best . So grateful and pleased with their job . I really recommend it . They are just insuperableThank you so much for your feedback. Our goal is to keep our customer satisfied."
        },
        {
            "author": "Paula S",
            "rating": "(5 stars)",
            "date": "11/23/201911/26/2019",
            "body": "The women did a wonderful job. I was very satisfied with their work, their pleasant personality, their willingness to satisfy me. I highly recommend this cleaning company.Thank you so much for your kind words. We really appreciate you taking the time out to share your experience with us. We count ourselves lucky for customers like you. We look forward to working with you again!"
        },
        {
            "author": "JONATHAN ALBERTO T",
            "rating": "(5 stars)",
            "date": "11/09/201911/15/2019",
            "body": "Is the best cleaning service that i ever had in my apartmentThank you so much for doing business with us."
        },
        {
            "author": "Juan E",
            "rating": "(5 stars)",
            "date": "11/05/201911/15/2019",
            "body": "Excellent & reliability... Came to prepare our home before moving in and they did an excellent job... ThanksDear *** *******, thanks for leaving us such a wonderful review. We are thrilled that you loved your experience; our staff will definitely be happy to read what you wrote. We put customer experience and satisfaction as our priority, and your review reaffirms the hard work we put in every day. So thanks for your kind words and we look forward to seeing you again."
        }
    ],
    "averageRating": "5"
}
```

### Charity Detail

```json
{
    "type": "Charity",
    "URL": "https://www.bbb.org/charity-reviews/upstate-new-york/vascular-birthmarks-foundation-in-latham-ny-235975279",
    "Charity Name": "Vascular Birthmarks Foundation",
    "Accreditation": true,
    "Conclusion": "Vascular Birthmarks Foundation meets the 20 Standards for Charity Accountability.",
    "Purpose": "Year, State Incorporated\n                        1994, NY\n        \n        \n            \n                Stated Purpose\n            \n            VBF\nis an international charitable organization that networks families affected by\na vascular birthmark, anomaly, tumor, or associated syndrome to the appropriate\nmedical professionals for evaluation and/or treatment, provides informational\nresources, as well as sponsors physician education, mobilizes medical missions,\ncollaborates on research, and supports programs that promote acceptance.",
    "Programs": "The Vascular Birthmarks\nFoundation (VBF) is an international charitable organization that networks\nfamilies affected by a vascular birthmark, tumor, or syndrome to appropriate\nmedical professionals for evaluation and/or treatment. \n\nVBF partners with the American Academy of Pediatrics and similar organizations\nto provide information and educational materials to patients and their families\nand to treatment specialists in the U.S. and globally. Resources are\ndistributed directly by the Foundation and via its passionate network of VBF\nGlobal Ambassadors.\n\nVBF hosts an annual no-cost conference and clinic for patients and their\nfamilies to meet with medical experts, attend lectures on the latest diagnosis\nand treatment techniques, and seek mutual support from other families affected\nby vascular birthmarks. \n\nVBF’s research mission is dedicated to finding a cause and a cure for vascular\nanomalies. \n\nVBF’s international physician education program includes intensive, one-on-one\nresidencies for foreign physicians with VBF’s U.S.-based expert physicians and\nmission trips to train physicians in other countries. The mission trips include\nno-cost clinics so attendees can be evaluated by expert physicians.  \n\nVBF sponsors the annual Vascular Birthmarks Month of Awareness each May and the\nVBF International Day of Awareness on May 15th.  Through coordinated\nsocial media campaigns, local and regional events, VBF educates families and\nphysicians worldwide about the importance of early diagnosis and available\ntreatment options.  Awareness activities continue year round along with\nthe Foundation’s “Ask/Accept” anti-bullying program that promotes acceptance\nfor individuals living with a vascular birthmark. \n    For the year ended December 31, 2018, Vascular Birthmarks Foundation program expenses were:\n    \n        \n            Program services\n            $331,967\n        \n        \n            Program Expenses\n            $331,967",
    "Governance": "CEO\n            \n            \n                Dr. Linda  Rozell-Shannon, President / Founder\n            \n        \n        \n            \n                Compensation*\n            \n             $72,808.00\n        \n                \n            \n                Board Chair\n            \n            \n                Ms. Corinne  Barinaga, Chairperson\n            \n        \n        \n            \n                Chair's Profession / Business Affiliation\n            \n\n        \n\n        \n            \n                Board Size\n            \n            13\n        \n\n        \n            \n                Paid Staff Size\n            \n            7\n        \n\n    \n\n    Governance\n    * Compensation includes annual salary and, if applicable, benefit plans, expense accounts and other allowances.",
    "Fundraising": "Method(s) Used: \n            Invitations to fundraising events, Internet, Appeals via Social Media (Facebook, etc.).\n        \n\n            % of Related Contributions on Fundraising: 7.93%",
    "Tax Status": "This organization is tax-exempt under section 501(c)(3) of the Internal Revenue Code. It is eligible to receive contributions deductible as charitable donations for federal income tax purposes.",
    "Financial": "The following information is based on Vascular Birthmarks Foundation's Audited financial statements for the fiscal year ending December 31, 2018\n        \n            Source of Funds\n                    \n                        Grants\n                        $275,000\n                    \n                    \n                        Contributions\n                        $236,983\n                    \n                    \n                        Conference income\n                        $74,408\n                    \n                    \n                        Federated fundraising\n                        $5,822\n                    \n                    \n                        Special event income\n                        $4,196\n                    \n                    \n                        Scholarship income\n                        $3,000\n                    \n                    \n                        Interest income\n                        $2,641\n                    \n                    \n                        Product sales\n                        $733\n                    \n                    \n                        Library subscriptions\n                        $200\n                    \n\n                \n                    Total Income\n                    $602,983\n                \n        \n\n    Breakdown of Expenses\n        \n            \n                \n                \n            \n            \n                \n                \n            \n        \n    \n            \n                Total Income\n                $602,983\n            \n                    \n                Total Expenses:\n                $429,338\n            \n                    \n                Program Expenses\n                $331,967\n            \n                    \n                Fundraising Expenses\n                $41,396\n            \n                    \n                Administrative Expenses\n                $55,975\n            \n                    \n                Other Expenses\n                $0\n            \n        \n            \n                Income in Excess of Expenses\n                $173,645\n            \n                            \n                Beginning Net Assets\n                $742,305\n            \n                    \n                Other Changes In Net Assets\n                $0\n            \n                    \n                Ending Net Assets\n                $915,950\n            \n                    \n                Total Liabilities\n                $9,341\n            \n                    \n                Total Assets\n                $925,291",
    "Standards": [
        {
            "name": "Board Oversight",
            "meetsStandards": true
        },
        {
            "name": "Board Size",
            "meetsStandards": true
        },
        {
            "name": "Board Meetings",
            "meetsStandards": true
        },
        {
            "name": "Board Compensation",
            "meetsStandards": true
        },
        {
            "name": "Conflict of Interest",
            "meetsStandards": true
        },
        {
            "name": "Effectiveness Policy",
            "meetsStandards": true
        },
        {
            "name": "Effectiveness Report",
            "meetsStandards": true
        },
        {
            "name": "Program Expenses",
            "meetsStandards": true
        },
        {
            "name": "Fundraising Expenses",
            "meetsStandards": true
        },
        {
            "name": "Accumulating Funds",
            "meetsStandards": true
        },
        {
            "name": "Audit Report",
            "meetsStandards": true
        },
        {
            "name": "Detailed Expense Breakdown",
            "meetsStandards": true
        },
        {
            "name": "Accurate Expense Reporting",
            "meetsStandards": true
        },
        {
            "name": "Budget Plan",
            "meetsStandards": true
        },
        {
            "name": "Truthful Materials",
            "meetsStandards": true
        },
        {
            "name": "Annual Report",
            "meetsStandards": true
        },
        {
            "name": "Website Disclosures",
            "meetsStandards": true
        },
        {
            "name": "Donor Privacy",
            "meetsStandards": true
        },
        {
            "name": "Cause Marketing Disclosures",
            "meetsStandards": true
        },
        {
            "name": "Complaints",
            "meetsStandards": true
        }
    ],
    "Address": "PO Box 106\n                        Latham, NY 12110\n                    \n                        PO Box 106\n                        Latham, NY 12110",
    "Phone Number": "877-823-4646\n                        \n                            877-823-4646"
}
```
