# Response Reference

## Response format
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
        ],
        "quick_replies": [ //optional
          {
            "type": "node",
            "caption": "Quick reply text",
            "target": "My Content"
          },
          {
            ...Another quick replies
          }
        ]
      }
    }
    
Dynamic block API current version `v2`
Dynamic block has a limit to have not more than 10 messages in `messages` block, 11 quick replies and 5 actions.
The `"buttons"`, `"actions"`, `"quick_replies"` properties are optional.

# Messages format

## Sending text
Use this response for sending text messages.
`url`, `flow`, `node` and `call` buttons can be used with text message.
The `"buttons"`, `"actions"`, `"quick_replies"` properties are optional.

    {
      "version": "v2",
      "content": {
        "messages": [
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
        ],
        "actions": [],
        "quick_replies": []
      }
    }
    
## Sending image
This response is used to send image files. Messenger supports JPG, PNG and GIF images. You can use `url`, `call`, `buy`, `flow`, `node` and `share` buttons.
The `"buttons"`, `"actions"`, `"quick_replies"` properties are optional.

    {
      "version": "v2",
      "content": {
        "messages": [
          {
            "type": "image",
            "url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.png",
            "buttons": []
          }
        ],
        "actions": [],
        "quick_replies": []
      }
    }
    
## Sending video file
This response is used to send video files. Messenger supports videos, which are up to `25MB` in size. You can use `url`, `call`, `buy`, `flow`, `node` and `share` buttons.
The `"buttons"`, `"actions"`, `"quick_replies"` properties are optional.

    {
      "version": "v2",
      "content": {
        "messages": [
          {
            "type": "video",
            "url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.mpg",
            "buttons": []
          }
        ],
        "actions": [],
        "quick_replies": []
      }
    }
    
## Sending audio file
This response is used to send audio files. Messenger supports audio, which are up to `25MB` in size. You can use `url`, `call`, `buy`, `flow`, `node` and `share` buttons.
The `"buttons"`, `"actions"`, `"quick_replies"` properties are optional.

    {
      "version": "v2",
      "content": {
        "messages": [
          {
            "type": "audio",
            "url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.mp3",
            "buttons": []
          }
        ],
        "actions": [],
        "quick_replies": []
      }
    }
     
## Sending files
This response is used to send any other files, which are no larger than 25 MB.
The `"actions"`, `"quick_replies"` properties are optional.

    {
      "version": "v2",
      "content": {
        "messages": [
          {
            "type": "file",
            "url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.pdf"
          }
        ],
        "actions": [],
        "quick_replies": []
      }
    }
    
    
## Sending gallery cards
This response is used to send a horizontal scrollable gallery. You can use `url`, `call`, `buy`, `flow`, `node` and `share` buttons.
The `"action_url"`, `"buttons"`, `"actions"`, `"quick_replies"` properties are optional.

    {
      "version": "v2",
      "content": {
        "messages": [
          {
            "type": "cards",
            "elements": [
              {
                "title": "Card title",
                "subtitle": "card text",
                "image_url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.png",
                "action_url": "https://manychat.com",
                "buttons": []
              }
            ],
            "image_aspect_ratio": "horizontal"
          }
        ],
        "actions": [],
        "quick_replies": []
      }
    }
    
`action_url` - URLs starting with HTTP may not open in some browsers. We strongly suggest to use HTTPS protocol for your URLs.\
`image_aspect_ratio` -  The aspect ratio used to render cards. You can use `horizontal` or `square` (default `horizontal`).

## Sending lists
This response is used to send a set of items vertically.  There are 2 options of rendering it. `"top_element_style": "large"` renders the first item with a cover image with text overlaid. `"top_element_style": "compact"` renders each item identically and is useful for presenting a list of items where no item is shown prominently.
You can use `url`, `flow`, `node` and `buy` buttons with list message. The number of elements is limited from 2 to 4.
The `"top_element_style"`, `"action_url"`, `"buttons"`, `"actions"`, `"quick_replies"` properties are optional.

    {
      "version": "v2",
      "content": {
        "messages": [
          {
            "type": "list",
            "top_element_style": "compact",
            "buttons": [],
            "elements": [
              {
                "title": "list title1",
                "subtitle": "list substitle2",
                "image_url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.png"
                "action_url": "https://manychat.com",
                "buttons": []
              }
            ]
          }
        ],
        "actions": [],
        "quick_replies": []
      }
    }
     
`action_url` - URLs starting with HTTP may not open in some browsers. We strongly suggest to use HTTPS protocol for your URLs

## Buttons
You can use buttons with each types: `call`, `url`, `share`, `flow`, `node`, `buy`.
You can provide custom action to be performed with the button.  
Actions can only be attached to `url`, `flow` and `node` button types.
Actions for buttons must comply with same format and restrictions as described in [Actions format](#actions-format) bellow.
The `"actions"` property is optional.

    {
      "version": "v2",
      "content": {
        "messages": [
          {
            "type": "text",
            "text": "simple text",
            "buttons": [
              {
                "type": "url",
                "caption": "External link",
                "url": "https://manychat.com",
                "actions": [] //optional
              },
              {
                ...Another buttons
              }
            ]
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
        ],
        "quick_replies": [ //optional
          {
            "type": "node",
            "caption": "Quick reply text",
            "target": "My Content"
          },
          {
            ...Another quick replies
          }
        ]
      }
    }

### Call button

    {
      "version": "v2",
      "content": {
        "messages": [
          {
            "type": "text",
            "text": "simple text with button",
            "buttons": [
              {
                "type": "call",
                "caption": "Call me",
                "phone": "+1 (555) 555-55-55"
              }
            ]
          }
        ],
        "actions": [],
        "quick_replies": []
      }
    }
    
### Url button
There are 3 options of `webview_size`: 

`full` - (100%), 

`medium` - (75%), 

`compact` - (50%)

The `"webview_size"` property is optional.
    
    {
      "version": "v2",
      "content": {
        "messages": [
          {
            "type": "text",
            "text": "simple text with button",
            "buttons": [
              {
                "type": "url",
                "caption": "External link",
                "url": "https://manychat.com",
                "webview_size": "full"
              }
            ]
          }
        ],
        "actions": [],
        "quick_replies": []
      }
    }
    
### Share button

    {
      "version": "v2",
      "content": {
        "messages": [
          {
            "type": "text",
            "text": "simple text with button",
            "buttons": [
              {
                "type": "share"
              }
            ]
          }
        ],
        "actions": [],
        "quick_replies": []
      }
    }
    
### Go to node button*

    {
      "version": "v2",
      "content": {
        "messages": [
          {
            "type": "text",
            "text": "simple text with button",
            "buttons": [
              {
                "type": "node",
                "caption": "Show",
                "target": "My Content"
              }
            ]
          }
        ],
        "actions": [],
        "quick_replies": []
      }
    }
    
`target` key should be linked to a node existing within executed flow. Node name can be found in its header, you need to use unique name for node connected with link. If there are multiple nodes with similar names inside of the same flow, transition behaviour would not meet expectations. 
Go to node buttons are not supported in Public API.

    
### Go to flow button

    {
      "version": "v2",
      "content": {
        "messages": [
          {
            "type": "text",
            "text": "simple text with button",
            "buttons": [
              {
                "type": "flow",
                "caption": "Go",
                "target": "content20180221085508_278589"
              }
            ]
          }
        ],
        "actions": [],
        "quick_replies": []
      }
    }
    
`target` needs flow ID (it can be found in URL when flow is opened) 
    
### Buy button
The `"success_target"` property is optional.

    {
      "version": "v2",
      "content": {
        "messages": [
          {
            "type": "text",
            "text": "simple text with button",
            "buttons": [
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
                  "cost": 2250
                },
                "success_target": "My Content"
              }
            ]
          }
        ],
        "actions": [],
        "quick_replies": []
      }
    }
    
`shipping_address`, `contact_name`, `contact_phone` fields are required to configure payment form;

`product`.`cost` should be set in cents (for example cost value of `$22.5` must set to `2250`); 

`success_target` key should be linked to a node existing within executed flow. Node name can be found in its header, you need to use unique name for node connected with link. If there are multiple nodes with similar names inside of the same flow, transition behaviour would not meet expectations;

`buy` button can only be used after Stripe account is connected in ManyChat settings. This button is in Beta mode.

### Dynamic block callback button
The `"headers"`, `"payload"` properties are optional.

    {
      "version": "v2",
      "content": {
        "messages": [
          {
            "type": "text",
            "text": "simple text with button",
            "buttons": [
              {
                "type": "dynamic_block_callback",
                "caption": "Dynamic content",
                "url": "https://your-service.com/dynamic",
                "method": "post",
                "headers": {
                  "x-header": "value"
                },
                "payload": {
                  "key": "value"
                }
              }
            ]
          }
        ],
        "actions": [],
        "quick_replies": []
      }
    }
    
`dynamic_block_callback` works the same way as dynamic block in a content node, it will send a request to the server upon click, server reply will be sent to user. External server URL must be mentioned with HTTPS protocol.
   
# Actions format
`actions` property of server response is optional.
## Action add tag
Use this response to add a tag to a subscriber. Tag with the same name must exist in your bot:

    {
      "version": "v2",
      "content": {
        "messages": [
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
        ],
        "actions": [
          {
            "action": "add_tag",
            "tag_name": "your tag",
          }
        ],
        "quick_replies": []
      }
    }
    
Tag name sent using `tag_name` parameter should match one of existing tags within ManyChat bot 
    
## Action remove tag
Use this response to remove a tag from a subscriber. Tag with the same name must exist in your bot:

    {
      "version": "v2",
      "content": {
        "messages": [
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
        ],
        "actions": [
          {
            "action": "remove_tag",
            "tag_name": "your tag",
          }
        ],
        "quick_replies": []
      }
    }
    
## Action set subscriber's field value
Use this response to set subscriber's field value. Custom field with the same name must exist in your bot

    {
      "version": "v2",
      "content": {
        "messages": [
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
        ],
        "actions": [
          {
            "action": "set_field_value",
            "field_name": "your field name",
            "value": "some value"
          }
        ],
        "quick_replies": []
      }
    }
    
Filed name sent using `field_name` should match with name of one of custom fields existing within ManyChat bot
You need to control data type recorded in custom fields, data type should match type of custom field

Use following value formats:
- For `Number` field type value should be numeric like `2` or `3.14` not bounded by double quotation marks;
- For `Text` field type value should be transferred as text `"some text"`;
- For `Date` field type value should be transferred as text with date formatted like `YYYY-MM-DD`, i.e. `"2018-03-25"`;
- For `Date Time` field type value should be transferred as text with date formatted in ISO8601 UTC, i.e `"2018-03-25T13:25:00.000Z"`
- For `True/False` field type value should be transferred like boolean `true` or `false` without quotation marks

## Action unset subscriber's field value
Use this response to unset (clear) subscriber's field value. Custom field with the same name must  exist in your bot

    {
      "version": "v2",
      "content": {
        "messages": [
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
        ],
        "actions": [
          {
            "action": "unset_field_value",
            "field_name": "your field name"
          }
        ],
        "quick_replies": []
      }
    }
    
# Quick replies
`quick_replies` property of server response is optional.
Quick replies cannot be used in dynamic block of a content node if there are other blocks exist afterwards.
Quick reply description format is the same for buttons, it supports `content`, `node`, `dynamic_block_callback` types.

## Go to node quick reply*

    {
      "version": "v2",
      "content": {
        "messages": [
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
        ],
        "actions": [],
        "quick_replies": [
          {
            "type": "node",
            "caption": "Show",
            "target": "My Content"
          }
        ]
      }
    }
    
`target` key should be linked to a node existing within executed flow. Node name can be found in its header, you need to use unique name for node connected with link. If there are multiple nodes with similar names inside of the same flow, transition behaviour would not meet expectations. 
Go to node quick replies are not supported in Public API.
    
## Go to flow quick reply

    {
      "version": "v2",
      "content": {
        "messages": [
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
        ],
        "actions": [],
        "quick_replies": [
          {
            "type": "flow",
            "caption": "Go",
            "target": "content20180221085508_278589"
          }
        ]
      }
    }
    
## Dynamic block callback quick reply
The `"headers"`, `"payload"` properties are optional.

    {
      "version": "v2",
      "content": {
        "messages": [
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
        ],
        "actions": [],
        "quick_replies": [
          {
            "type": "dynamic_block_callback",
            "caption": "Dynamic content",
            "url": "https://your-service.com/dynamic",
            "method": "post",
            "headers": {
              "x-header": "value"
            },
            "payload": {
              "key": "value"
            }
          }
        ]
      }
    }
    
`target` needs flow ID (it can be found in URL when flow is opened) 


\* - does not work for Zapier action "Send Dynamic Message to User"

# External Message Callback
`external_message_callback` property of server response is optional.

You can ask ManyChat to handle the next subscriber's message on your side by using the `external_message_callback` property.

`{{last_input_text}}` variable in the `payload` property will be replaced by the text of the subscriber's message.

You can specify the time limit (in seconds) for this callback by using `timeout` property (default value is 1 day, maximum value is 1 day). If subscriber will not send text message in this period, callback will expire.

    {
      "version": "v2",
      "content": {
        "messages": [
          {
            "type": "text",
            "text": "Hello! How are you?"
          }
        ],
        "actions": [],
        "quick_replies": [],
        "external_message_callback": {
            "url": "https://your-service.com/dynamic",
            "method": "post",
            "headers": {
              "x-header": "value"
            },
            "payload": {
              "id": "{{user_id}}",
              "last_input_text": "{{last_input_text}}",
              "key": "value"
            },
            "timeout": 600
        }
      }
    }

# Variables

In dynamic block request body, you can use `Full Subscriber Data` variable, that contains all subscriber's information:

    {
        "id": 13245647xxxxxxxxx,
        "key": "user:13245647xxxxxxxxx",
        "page_id": 234564657xxxxxxxx,
        "status": "active",
        "first_name": "Subscriber",
        "last_name": "Lastname",
        "name": "Subscriber Lastname",
        "gender": "male",
        "profile_pic": "https://xxxxxxxxx.com/subscribers/big_xxxxxxxxxxxxxxxx.jpg",
        "locale": "en_US",
        "language": "English",
        "timezone": "UTC-07",
        "live_chat_url": "https://manychat.com/fb234564657xxxxxxxx/chat/13245647xxxxxxxxx",
        "last_input_text": "Last subscriber's input text",
        "last_growth_tool": null,
        "subscribed": "2018-07-02T00:00:00+00:00",
        "last_interaction": "2018-07-02T00:00:00+00:00",
        "last_seen": "2018-07-02T00:00:00+00:00",
        "custom_fields": {
            "customField": 0.75,
            "customDate": "2018-05-31",
            "customBool": true,
            ...
        }

    }
