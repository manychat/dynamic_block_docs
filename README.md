#Response Reference

##Response format
Response format for sending dynamic messages:

    {
        "version": "v2",
        "content": {
            "messages": [
                {
                   "type": "text",
                   "text": "simple text"    
                },
                {
                    ...Another messages
                }
            ],
            "actions": [  //optional
                {
                    "action": "add_tag",
                    "tag_name": "example tag"
                },
                {
                    ...Another actions
                }
            ]
        }
    }
    
Dynamic block API current version `v2`

#Messages format

##Sending text
Use this response for sending text messages. The `"buttons"` property is optional.
`url`, `flow`, `node` and `call` buttons can be used with text message.

    {
       "type": "text",
       "text": "simple text with button",
       "buttons": [
            {
                "type": "url",
                "caption": "External link",
                "url": "https://manychat.com"
            }
       ]
    }
    
##Sending image
This response is used to send image files. Messenger supports JPG, PNG and GIF images. You can use `url`, `call`, `buy`, `flow`, `node` and `share` buttons.

    {
       "type": "image",
       "url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.png",
       "buttons": [] //optional
    }
    
##Sending video file
This response is used to send video files. Messenger supports videos, which are up to `25MB` in size. You can use `url`, `call`, `buy`, `flow`, `node` and `share` buttons.
    
    {
       "type": "video",
       "url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.mpg",
       "buttons": [] //optional
    }
     
##Sending files
This response is used to send any other files, which are no larger than 25 MB.

    {
       "type": "file",
       "url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.pdf"
    }
    
    
##Sending gallery cards
This response is used to send a horizontal scrollable gallery. You can use `url`, `call`, `buy`, `flow`, `node` and `share` buttons.

    {
       "type": "cards",
       "elements": [
            {
              "title": "Card title",
              "subtitle": "card text",
              "image_url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.png",
              "buttons": [] //optional
            },
            {
                ...
            }
       ]
    }

##Sending lists
This response is used to send a set of items vertically.  There are 2 options of rendering it. `"top_element_style": "large"` renders the first item with a cover image with text overlaid. `"top_element_style": "compact"` renders each item identically and is useful for presenting a list of items where no item is shown prominently.
You can use `url`, `flow`, `node` and `buy` buttons with list message. The number of elements is limited from 2 to 4.

    {
       "type": "list",
       "top_element_style": "compact", //optional, default "compact"
       "buttons": [], //optional
       "elements": [
         {
            "title": "list title1",
            "subtitle": "list substitle2",
            "image_url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.png"
            "action_url": "https://manychat.com", //optional
            "buttons": [] //optional
         },
         {
            ...
         }
       ]
     }
     
##Buttons
You can use buttons with each types: `call`, `url`, `share`, `flow`, `node`, `buy`.
Buttons format:

    {
        "buttons": [
            {
                "type": "url",
                "caption": "External link",
                "url": "https://manychat.com"
            },
            {
                ...Another buttons
            }
        ]
    }

###Call button

    {
        "type": "call",
        "caption": "Call me",
        "phone": "+1 (555) 555-55-55"
    }
    
###Url button

    {
        "type": "url",
        "caption": "External link",
        "url": "https://manychat.com"
    }
    
###Share button

    {
        "type": "share"
    }
    
###Go to node button

    {
        "type": "node",
        "caption": "Show",
        "target": "My Content"
    }
    
`target` key should be linked to a node existing within executed flow. Node name is can be found in its header, you need to use unique name for node connected with link. If there are multiple nodes with similar names inside of the same flow, transition behaviour would not meet expectations. 
    
###Go to flow button

    {
        "type": "flow",
        "caption": "Go",
        "target": "content20180221085508_278589"
    }
    
`target` needs flow ID (it can be found in URL when flow is opened) 
    
###Buy button

    {
        "type":    "buy",
        "caption": "Buy",
        "customer": {
            "shipping_address": true,
            "contact_name":     false,
            "contact_phone":    true
        },
        "product": {
            "label": "T-shirt",
            "price": "22.50"
        }
    }
    
`shipping_address`, `contact_name`, `contact_phone` fields are required to configure payment form
`buy` button can only be used after Stripe account is connected in ManyChat settings. This button is in Beta mode.
   
#Actions format
`actions` property of server response is optional.
##Action add tag
Use this response for add tag for subscriber. Tag with same name must be exists in your bot:

    {
        "action": "add_tag",
        "tag_name": "your tag",
    }
    
Tag name sent using `tag_name` parameter should match one of existing tags within ManyChat bot 
    
##Action remove tag
Use this response for remove tag for subscriber. Tag with same name must be exists in your bot:

    {
        "action": "remove_tag",
        "tag_name": "your tag",
    }
    
##Action set subscriber's field value
Use this response for set subscriber's field value. Custom field with same name must be exists in your bot

    {
        "action": "set_field_value",
        "field_name": "your field name",
        "value": "some value"
    }
    
Filed name sent using `field_name` should match with name of one of custom fields existing within ManyChat bot
You need to control data type recorded in custom fields, data type should match type of custom field

Use following value formats:
- For `Number` field type value should be numeric like `2` or `3.14` not bounded by double quotation marks;
- For `Text` field type value should be transferred as text `"some text"`;
- For `Date` field type value should be transferred as text with date formatted like `YYYY-MM-DD`, i.e. `"2018-03-25"`;
- For `Date Time` field type value should be transferred as text with date formatted in ISO8601 UTC, i.e `"2018-03-25T13:25:00.000Z"`
- For `True/False` field type value should be transferred like boolean `true` or `false` without quotation marks

##Action unset subscriber's field value
Use this response for unset (clear) subscriber's field value. Custom field with same name must be exists in your bot

    {
        "action": "unset_field_value",
        "field_name": "your field name"
    }