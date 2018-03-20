# Response Reference

## Response format
Response format for sending dynamic messages:

    {
        "version": "v1",
        "content": {
            "messages": [
                {
                   "type": "text",
                   "text": "simple text"    
                },
                {
                    ...Another messages
                }
            ]
        }
    }
    
Dynamic block API current version `v1`

# Messages format

## Sending text
Use this response for sending text messages. The `"buttons"` property is optional.
`url` and `call` buttons can be used with text message.

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
    
## Sending image
This response is used to send image files. Messenger supports JPG, PNG and GIF images. You can use `url`, `call`, `buy` and `share` buttons.

    {
       "type": "image",
       "url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.png",
       "buttons": [] //optional
    }
    
## Sending video file
This response is used to send video files. Messenger supports videos, which are up to `25MB` in size. You can use `url`, `call`, `buy` and `share` buttons.
    
    {
       "type": "video",
       "url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.mpg",
       "buttons": [] //optional
    }
     
## Sending files
This response is used to send any other files, which are no larger than 25 MB.

    {
       "type": "file",
       "url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.pdf"
    }
    
    
## Sending gallery cards
This response is used to send a horizontal scrollable gallery. You can use `url`, `call`, `buy` and `share` buttons.

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

## Sending lists
This response is used to send a set of items vertically.  There are 2 options of rendering it. `"top_element_style": "large"` renders the first item with a cover image with text overlaid. `"top_element_style": "compact"` renders each item identically and is useful for presenting a list of items where no item is shown prominently.
You can use `url` and `buy` buttons with list message. The number of elements is limited from 2 to 4.

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
     
## Buttons
You can use buttons with each types: `call`, `url`, `share`, `buy`.

    {
        ...
        "buttons": [
            {
                "type": "url",
                "caption": "External link",
                "url": "https://manychat.com"
            },
            {
                "type": "call",
                "caption": "Call me",
                "phone": "+1 (555) 555-55-55"
            },
            {
                "type": "share"
            },
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
        ]
    }