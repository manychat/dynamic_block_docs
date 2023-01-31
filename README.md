{% raw %}

### See also
<a href="https://manychat.github.io/dynamic_block_docs/channels/">Response Reference for Instagram, WhatsApp, and Telegram Automation</a>

# Response Reference for Facebook Automation

## Response format
The response format for sending dynamic messages:

    {
      "version": "v2",
      "content": {
        "messages": [
          {
            "type": "text",
            "text": "simple text"
          },
          {
            ...Other messages
          }
        ],
        "actions": [  //optional
          {
            "action": "add_tag",
            "tag_name": "example tag"
          },
          {
            ...Other actions
          }
        ],
        "quick_replies": [ //optional
          {
            "type": "node",
            "caption": "Quick reply text",
            "target": "My Content"
          },
          {
            ...Other quick replies
          }
        ]
      }
    }

Dynamic Block API's current version is `v2` 

Dynamic Block has a limit of no more than 10 messages in the `messages` block, 11 Quick Replies, and 5 Actions. The `"buttons"`, `"actions"`, and `"quick_replies"` properties are optional.

# Messages format
## Sending text
Use this response for sending text messages.

The `url`, `flow`, and `node` buttons can be used with text messages.

The `"buttons"`, `"actions"`, and `"quick_replies"` properties are optional.

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
    
## Sending images
This response is used to send image files. Messenger supports JPG, PNG, and GIF images. You can use `url`, `call`, `buy`, `flow` and `node` buttons.

The `"buttons"`, `"actions"`, and `"quick_replies"` properties are optional.

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
This response is used to send video files. Messenger supports videos that are up to `25MB` in size. You can use `url`, `call`, `buy`, `flow`, and `node` buttons.

The `"buttons"`, `"actions"`, and `"quick_replies"` properties are optional.

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
This response is used to send audio files. Messenger supports audio files that are up to `25MB` in size. You can use `url`, `call`, `buy`, `flow`, and `node` buttons.

The `"buttons"`, `"actions"`, and `"quick_replies"` properties are optional.

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
This response is used to send any other files, no larger than `25MB` in size.

The `"actions"` and `"quick_replies"` properties are optional.

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
This response is used to send a horizontally scrollable gallery. You can use `url`, `call`, `buy`, `flow`, and `node` buttons.

The `"action_url"`, `"buttons"`, `"actions"`, and `"quick_replies"` properties are optional.

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
    
`action_url` - URLs starting with HTTP may not open in some browsers. We strongly suggest using HTTPS protocol for your URLs.
`image_aspect_ratio` - The aspect ratio used to render cards. You can use `horizontal` or `square` (default `horizontal`).

## Buttons
You can use buttons with each type: `call`, `url`, `flow`, `node`, `buy`. You can provide custom action to be performed with the button. Actions can only be attached to the `url`, `flow`, and `node` button types. Actions for buttons must comply with the same format and restrictions as described in the [Actions format](#actions-format) below. The `"actions"` property is optional.

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
                ...Other buttons
              }
            ]
          },
          {
            ...Other messages
          }
        ],
        "actions": [  //optional
          {
            "action": "add_tag",
            "tag_name": "example tag"
          },
          {
            ...Other actions
          }
        ],
        "quick_replies": [ //optional
          {
            "type": "node",
            "caption": "Quick reply text",
            "target": "My Content"
          },
          {
            ...Other quick replies
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
There are 3 options for `webview_size`: 

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
    
`target` key should be linked to a node existing within the executed Flow. The node name can be found in its header, you need to use a unique name for the node connected with the link. If there are multiple nodes with similar names inside of the same Flow, transition behavior would not meet expectations. Go-to-node buttons are not supported in Public API.
    
### Go to Flow button

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
    
`target` needs flow ID (it can be found in the URL when the Flow is opened).
    
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
                  "contact_name": false,
                  "contact_phone": true,
                  "contact_email": true
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

`shipping_address`, `contact_name`, and `contact_phone` fields are required to configure the payment form.

`product`.`cost` should be set in cents (for example cost value of `$22.5` must be set to `2250`).

`success_target` key should be linked to a node existing within the executed Flow. The node name can be found in its header, you need to use a unique name for the node connected with the link. If there are multiple nodes with similar names inside of the same Flow, transition behavior would not meet expectations.

`buy` button can only be used after Stripe/Paypal account is connected in Manychat Settings.

### Dynamic Block callback button
The `"headers"` and `"payload"` properties are optional.

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
    
`dynamic_block_callback` works the same way as a Dynamic Block in a content node. It will send a request to the server upon clicking, and the server reply will be sent to the contact. External server URL must be mentioned with HTTPS protocol.

# Actions format
The `actions` property of the server response is optional.

## Action add tag
Use this response to add a Tag to a contact. A Tag with the same name must exist in your bot.

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
    
The Tag name sent using the `tag_name` parameter should match one of the existing Tags within the Manychat bot 
    
## Action remove tag
Use this response to remove a Tag from a contact. A Tag with the same name must exist in your bot.

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
    
## Action set contact’s field value
Use this response to set the contact’s field value. A Custom Field with the same name must exist in your bot.

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
    
The filed name sent using `field_name` should match the name of one of the Custom Fields existing within the Manychat bot. You need to control the data type recorded in Custom Fields, data type should match the type of the Custom Field.

Use the following value formats:

- For the `Number` field type, the value should be numeric like `2` or `3.14`, not bounded by double quotation marks;
- For the `Text` field type, the value should be transferred as text: `"some text"`;
- For the `Date` field type, the value should be transferred as text with the date formatted like `YYYY-MM-DD`, i.e. `"2018-03-25"`;
- For the `Date Time` field type, the value should be transferred as text with the date formatted in ISO8601 UTC, i.e `"2018-03-25T13:25:00.000Z"`;
- For the `True/False` field type, the value should be transferred like a boolean `true` or `false` value without quotation marks.

## Action unset contact’s field value
Use this response to unset (clear) the contact’s field value. A Custom Field with the same name must exist in your bot.

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
    
# Quick Replies
`quick_replies` property of server response is optional. Quick Replies cannot be used in the Dynamic Block of a content node if there are other blocks afterward. The Quick Reply description format is the same for buttons, it supports `content`, `node`, and `dynamic_block_callback` types.

## Go to node Quick Reply*

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
    
`target` key should be linked to a node existing within the executed Flow. The node name can be found in its header, you need to use a unique name for the node connected with the link. If there are multiple nodes with similar names inside of the same Flow, transition behavior would not meet expectations. Go-to-node Quick Replies are not supported in Public API.
    
## Go to Flow Quick Reply

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
    
## Dynamic Block callback Quick Reply
The `"headers"` and `"payload"` properties are optional.

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
    
`target` needs Flow ID (it can be found in the URL when the Flow is opened).

**Does not work for the Zapier action “Send Dynamic Message to User”.**

# External Message Callback
The `external_message_callback` property of the server response is optional.

You can ask Manychat to handle the next contact’s message on your side by using the `external_message_callback` property.

The `{{last_input_text}}` variable in the `payload` property will be replaced by the text of the contact’s message.

You can specify the time limit (in seconds) for this callback by using the `timeout` property (the default value is 1 day, and the maximum value is 1 day). If the contact doesn’t send any text messages in this period, the callback will expire.

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
    
`external_message_callback` works the same way as a Dynamic Block in a content node. It will send a request to the server when the contact sends a text message, and the server reply will be sent to the contact. The external server URL must be mentioned with the HTTPS protocol.

# Variables

In the Dynamic Block request body, you can use the `Full Contact Data` variable which contains all contact’s information:

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
{% endraw %}
