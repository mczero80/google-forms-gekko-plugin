# Google Forms Gekko Plugin
A gekko plugin for live trading that submits all trades to a google spreadsheet through Forms

**Very Alpha** I've only tested this for a few days so far... but then there isn't much too it :) Any feedback/merge requests appreciated!

Setup of this plugin is a little involved, but it works for me and I've seen others asking for simillar functionality, so here's a share.

## What it does
Each time gekko completes a trade (live or paper) it updates a google sheet with the trade price and new balances. One form can be used to submit data from all bots, a new sheet is automatically created for each pair and exchange combination. Each pair sheet has a basic list of trades and overall P/L as well as % profitable trades. Note that the % profitable counts any multiple trades in response to one bit of advice as gekko adjusts it's buy/sell price, so won't align with % profitable advice.

It should look something like this:
![alt text](https://i.imgur.com/U2K3QPn.png "Unrealistically Successful Example")

## Setup in Gekko
* Download/Clone this repo.
* Copy the gforms.js into gekko/plugins - this is the main plugin code.
* Copy the contents of the downloaded plugins.js file into gekko/plugins.js between the existing plugins. This registers the plugin with Gekko
* Copy the code from the downloaded sample-config.js into your CLI config file.

Finally, the 'require' module is needed - in your gekko root run
```
npm i require
```

## Setup in Google Drive
* Make a copy of [this google form](https://drive.google.com/open?id=1DlRinAn1aix3yNOMrook3m5_B7k_d676) (Right Click, Make Copy) into your google drive. 

   **OR**
* In your Google Drive, create a new Form.
* Add these questions to the form, each of type 'Short Text'
  * Exchange
  * Currency
  * Asset
  * Action
  * Asset Held 
  * Price 
  * Currency Held
  * Initial Balance
  * Portfolio Balance
  
NOTE - First version of readme had these in the wrong order which will result in the wrong values in the final sheet - if you followed that, please create a new form with the above order.
   
* Once you have copied or created the form, link it to a spreadsheet (small green button in responses tab), and rename the responses sheet (tab at the bottom) "Form Responses" (Important it's exact as the code reffers to that sheet by name)
* Open the google script editor (Tools> Script Editor) 
  * Copy in the code from googleSheetsScript.gs. Save it.
  * Go to Edit>Current Project's Triggers. From the dropdowns set it to Run "onFormSubmit" Trigger From "Spreadsheet" "OnFormSubmit" (Theoretically the onFormSubmit function in code should be triggered by this anyway, but it didn't seem to work until I added the trigger manually... ymmv)
  
## Link the two!
* Go back to the google form edit screen. In the three dot menu, select Get Pre-filled link.
* A new form will open. Fill in each field with the name of the question above it so we can identify it in the next steps.
* Click Get Link, then Copy link in the bottom left popup.
* Paste this link as a comment in your CLI settings file. Copy the form ID and each question ID into the gforms.config object in your command line config file.

All done, take it for a spin :) 

Note that it will take a couple of sells before all the sparkline graphs start working properly - until then they'll all read #NA.


___
If you want to leave a tip, go give it to askmike and support gekko! If you've already done that and still want to leave a tip, thanks!

LTC: Lapmuu1Th2BGBMG6vVyM83swoT8Qc6PiZP
