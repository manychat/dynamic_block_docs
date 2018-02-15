#Response Reference

##Response format
Use this response format for sending dynamic messages:

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
    
Current version of dynamic block API `v1`

#Messages format

##Sending text
Use this response to send text messages. The `"buttons"` property is optional.
With text message you can use `url` and `call` buttons.

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
Use this response to send image files. Messenger supports JPG, PNG and GIF images. You can use `url`, `call` and `share` buttons.

    {
       "type": "image",
       "url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.png",
       "buttons": [] //optional
    }
    
##Sending video file
Use this response to send video files. Messenger supports videos, which are up to `25MB` in size. You can use `url`, `call` and `share` buttons.
    
    {
       "type": "video",
       "url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.mpg",
       "buttons": [] //optional
    }
     
##Sending files
Use this response to send any other files, which are no larger than 25 MB.

    {
       "type": "file",
       "url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.pdf"
    }
    
    
##Sending gallery cards
Use this response to send a horizontal scrollable gallery. You can use `url`, `call` and `share` buttons.

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
Use this response to send a set of items vertically. It can be rendered in two different ways. `"top_element_style": "large"` renders the first item with a cover image with text overlaid. `"top_element_style": "compact"` renders each item identically and is useful for presenting a list of items where no item is shown prominently.
With list message you can use only `url` type buttons.

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
You can use buttons with each types: `call`, `url`, `share`.

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
            }
        ]
    }