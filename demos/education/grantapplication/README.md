# Morf Demo Script: Grant Application

## Aftia Morf / Doc Generation / Sign Demo


### Setup

For this demo you’ll need:

- MS Word with the Document Generation Add-on installed
-	Power Automate with connections setup to your
    -	Adobe PDF Services account
    -	Adobe Sign Account
    -	MS SharePoint account
-	Internet access to reach https://www.getmorf.io/

Import the Power Automate Flow from `MorfSampleGrantApplication_20220422201643.zip` by going to My Flows in the Power Automate sidebar and clicking `Import` at the top of the page.


 ![image](https://user-images.githubusercontent.com/17143489/179748901-3544099f-74ac-40c0-be69-a4ef8c2e4f1e.png)

Select the ﬁle and setup the connections by clicking `Select During Import` for

- SharePoint Connection
- Adobe PDF Services Connection
- Adobe Sign Connection

![image](https://user-images.githubusercontent.com/17143489/179749061-6f165746-881e-4221-bb70-85aa9bb8d7e2.png)


Then import the application. Under My Flows, select the Morf Grant Application you just imported and turn it on.
 

 ![image](https://user-images.githubusercontent.com/17143489/179749136-f9e4f609-4240-4574-8df2-fcd5f86dbbd3.png)


You are now ready to demonstrate building the Morf application.
 
### Demo

#### Word Template


1. Open the edited Grant Application (`GrantApplicationLMTemplate_Editted.docx`) in Microsoft Word
2. Open the Adobe Document Generation Word Add-In and Click continue without JSON
3. Create the following tags:
    - Author
    - Date
    - Organization.name
    - Organization.established
    - Organization.contact
    
Insert `Author` and `Date` on the first page and `Organization.name`, `Organization.established`, and `Organization.contact` on the second page.
NOTE: it doesn’t matter what you name these fields. You could call them `foo` and `foo_bar` if you'd like. The JSON payload from Morf will still match the document.

![image](https://user-images.githubusercontent.com/17143489/179749841-3610332a-20e5-47ad-8259-e99afd040418.png)

3. Scroll to the bottom of the document and insert an Adobe Sign tag for Signer 1 with the field type: Signature

![image](https://user-images.githubusercontent.com/17143489/179749928-2733e833-d2f5-4205-a660-c064a9de3e41.png)

4. Save the word document
5. Tell the customer that for demo purposes the rest of the document has already been tagged. It is that simple you just need to put some fields in with double curly braces by hand or using the Word Add-In.
6. Put the Word file into a SharePoint folder.


#### Conversion to Morf

1.	Go to https://editor.getmorf.io/ and click on `Convert`. Select the Word document you previously tagged.
2.	Show the audience that the Word tags have been turned into form fields!
3.	Edit the Morf form in the left hand pane to change the title and logo if you'd like
    ```
    "head": {
        "title": "Grant Application",   
        "logo": "https://tailwindui.com/img/logos/workflow-mark-indigo-600.svg"
    }
    ```
4. *Optional:* Change the Organization Goals field’s type to textarea to make it a multiline field.
    ```
    {
        "type": "textarea",
        "label": "Organization Goals", "bind": "Organization.Goals"
    }
    ```

Show the customer that the changes happened in real time!

#### Power Automate

1. Edit the flow and copy the HTTP Post URL from the first step.
 

 ![image](https://user-images.githubusercontent.com/17143489/179752274-e9cb2724-33dd-41c0-9efb-cefb567f3851.png)


2. While you are here make sure the Sharepoint step is using the word document you stored there earlier.
3. Explain to the customer the steps in the flow
 
4. Go back to your Morf form and edit the `submit` value under `config`. Paste the URL from the Power Automate flow.
    ```
    {
        "config": {
            "submit": "https://prod-18.canadacentral.logic.azure.com:443/workflows/abcd...",
            "successUrl": "http://getmorf.io/", 
        }
    }
    ```

#### Form Submission

1. Click the `Preview` button in the Morf Editor.
2. Now fill out the form. Fill out as much or as little as you'd like. Just be sure to enter an email address in the Organization email field. This will be picked up by the Power Automate Flow, and the document will be sent there for signature. Click Submit.

#### Signing

1. Open up the inbox of the email address you specified in the Morf Form. You should have an email from Adobe Sign waiting for you.
2. Open it up, show that the document is populated with the information captured in the Morf Form
3. Sign the document.


You are done! You just built an end to end application right in front of the customer’s eyes. How cool is that?

Have questions? Join us on [Slack](https://getmorf.slack.com/join/signup)!
