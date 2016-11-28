# Microsoft Translator API flow

First get a translator API key from Azure portal, click on New, search for 'Cognitive Services' and hit enter. 

![azurenew](http://i.imgur.com/KyMbdK8.png)

You should see Cognitive Services APIs. Click on it and then click create. 

![searchres](http://i.imgur.com/8gvOp5I.png)

![cognitivetype](http://i.imgur.com/fTVktm7.png)

Wait a little while for it to get set up and deployed. Once it's done, click into 'All resources' blade down the left, and click into the Cognitive Service account you just created. Click into 'keys' and you'll see this:

![luiskeys](http://i.imgur.com/NpvgyXT.png)

To use the Microsoft Translation API you need to put a token in the Authorization header that lasts 10 minutes. To get this token make a *POST request* to the following API endpoint:

`'https://api.cognitive.microsoft.com/sts/v1.0/issueToken?subscription-key=' + TRANSLATIONKEY`

YOURTRANSLATIONKEY is the key you got from the Azure portal. You'll need to get a new token every 10 minutes. After you get the token, you can now call the translator API by making a *GET request* to:

`'http://api.microsofttranslator.com/v2/Http.svc/Translate'+'?text=' + urlencodedtext + '&from=' + FROMLOCALE +'&to=' + TOLOCALE`

The list of locales (i.e. languages codes) is here: https://msdn.microsoft.com/en-us/library/hh456380.aspx. You need to url encode the text you want to translate, and remember to put "Bearer " before the token string in the Authorization header of the GET request. I think the response comes back in XML. 
