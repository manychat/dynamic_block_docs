{% raw %}

### See also
<a href="https://manychat.github.io/dynamic_block_docs/">Response Reference for Facebook Automation</a>

# Response Reference for Instagram, WhatsApp, and Telegram Automation

## Response format
The response format for sending dynamic messages:

    {
      "version": "v2",
      "content": {
        "type": "instagram", // "whatsapp" and "telegram" are also supported
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
        "quick_replies": [ //optional, not supported for WhatsApp and Telegram
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

Dynamic Block has a limit of no more than 10 messages in the `messages` block, 11 Quick Replies, and 5 Actions.
The `"buttons"`, `"actions"`, and `"quick_replies"` properties are optional.

# Messages format

## Sending text
Use this response for sending text messages.
The `url`, `flow`, and `node` buttons can be used with text messages.
The `"buttons"`, `"actions"`, and `"quick_replies"` properties are optional.

    {
      "version": "v2",
      "content": {
        "type": "instagram", // "whatsapp" and "telegram" are also supported
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
This response is used to send image files. The `"actions"` and `"quick_replies"` properties are optional.

    {
      "version": "v2",
      "content": {
        "type": "instagram", // "telegram" is also supported
        "messages": [
          {
            "type": "image",
            "url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.png",
          }
        ],
        "actions": [],
        "quick_replies": []  // not supported for Telegram
      }
    }

## Sending video files
This response is used to send video files. You can use `url`, `buy`, `flow`, and `node` buttons. The `"buttons"` and `"actions"` properties are optional.

**Sending video files is not supported by WhatsApp and Instagram channels.**

    {
        "version": "v2",
        "content": {
            "type": "telegram",
            "messages": [
                {
                    "type": "video",
                    "url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.mpg",
                    "buttons": []
                }
            ],
            "actions": []
        }
    }

## Sending audio files
This response is used to send audio files. You can use `url`, `buy`, `flow`, and `node` buttons. The `"buttons"` and `"actions"` properties are optional.

**Sending audio files is not supported by WhatsApp and Instagram channels.**

    {
        "version": "v2",
        "content": {
            "type": "telegram",
            "messages": [
                {
                    "type": "audio",
                    "url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.mp3",
                    "buttons": []
                }
            ],
            "actions": []
        }
    }

## Sending files
This response is used to send any other files, no larger than `25MB` in size. The `"actions"` property is optional.

**Sending files is not supported by WhatsApp and Instagram channels.**

    {
        "version": "v2",
        "content": {
            "type": "telegram",
            "messages": [
                {
                    "type": "file",
                    "url": "https://manybot-thumbnails.s3.eu-central-1.amazonaws.com/ca/xxxxxxzzzzzzzzz.pdf"
                }
            ],
            "actions": []
        }
    }

## Sending gallery cards
This response is used to send a horizontally scrollable gallery. You can use `url`, `buy`, `flow`, and `node` buttons. The `"action_url"`, `"buttons"`, `"actions"`, and `"quick_replies"` properties are optional.

**Galleries are not supported by WhatsApp and Telegram channels.**

    {
      "version": "v2",
      "content": {
        "type": "instagram",
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
`image_aspect_ratio` - The aspect ratio used to render cards. You can use `horizontal` or `square` (default `horizontal`).

## Buttons
You can use buttons with each type: `url`, `flow`, `node`. You can provide custom actions to be performed with the button. Actions for buttons must comply with the same format and restrictions as described in the [Actions format](#actions-format) below.

The `"actions"` property is optional.

    {
      "version": "v2",
      "content": {
        "type": "instagram", // "whatsapp" and "telegram" are also supported
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
        "quick_replies": [ //optional, not supported for WhatsApp and Telegram
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
    
### Url button
    
    {
      "version": "v2",
      "type": "instagram", // "telegram" is also supported
      "content": {
        "type": "instagram",
        "messages": [
          {
            "type": "text",
            "text": "simple text with button",
            "buttons": [
              {
                "type": "url",
                "caption": "External link",
                "url": "https://manychat.com",
              }
            ]
          }
        ],
        "actions": [],
        "quick_replies": [] // not supported for Telegram
      }
    }

### Go to node button*

    {
      "version": "v2",
      "content": {
        "type": "instagram", // "telegram" is also supported
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
        "quick_replies": [] // not supported for Telegram
      }
    }
    
*`target` key should be linked to a node existing within the executed Flow. The node name can be found in its header, you need to use a unique name for the node connected with the link. If there are multiple nodes with similar names inside of the same Flow, transition behavior would not meet expectations. Go-to-node buttons are not supported in Public API.

    
### Go to Flow button

    {
      "version": "v2",
      "content": {
        "type": "instagram", // "whatsapp" and "telegram" are also supported
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
        "quick_replies": [] // not supported for WhatsApp and Telegram
      }
    }
    
`target` needs Flow ID (it can be found in the URL when the Flow is opened).
    
### Buy button
The `"success_target"` property is optional.

    {
      "version": "v2",
      "content": {
        "type": "instagram", // "telegram" is also supported
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
        "quick_replies": [] // not supported for Telegram
      }
    }
    
`shipping_address`, `contact_name`, and `contact_phone` fields are required to configure the payment form.

`product`.`cost` should be set in cents (for example cost value of `$22.5` must be set to `2250`).

`success_target` key should be linked to a node existing within the executed Flow. The node name can be found in its header, you need to use a unique name for the node connected with the link. If there are multiple nodes with similar names inside of the same Flow, transition behavior would not meet expectations.

`buy` button can only be used after Stripe/Paypal account is connected in Manychat Settings.

# Actions format
`actions` property of server response is optional.

## Action add tag
Use this response to add a Tag to a contact. A Tag with the same name must exist in your bot.

    {
      "version": "v2",
      "content": {
        "type": "instagram", // "whatsapp" and "telegram" are also supported
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
        "quick_replies": [] // not supported for WhatsApp and Telegram
      }
    }
    
The Tag name sent using the `tag_name` parameter should match one of the existing Tags within the Manychat bot 
    
## Action remove tag
Use this response to remove a Tag from a contact. A Tag with the same name must exist in your bot:

    {
      "version": "v2",
      "content": {
        "type": "instagram", // "whatsapp" and "telegram" are also supported
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
        "quick_replies": [] // not supported for WhatsApp and Telegram
      }
    }
    
## Action set contact's field value
Use this response to set a contact’s field value. A Custom Field with the same name must exist in your bot.

    {
      "version": "v2",
      "content": {
        "type": "instagram", // "whatsapp" and "telegram" are also supported
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
        "quick_replies": [] // not supported for WhatsApp and Telegram
      }
    }
    
The filed name sent using `field_name` should match the name of one of the Custom Fields existing within the Manychat bot. You need to control the data type recorded in Custom Fields, data type should match the type of the Custom Field.

Use the following value formats:
- For the `Number` field type, the value should be numeric like `2` or `3.14`, not bounded by double quotation marks;
- For the `Text` field type, the value should be transferred as text: `"some text"`;
- For the `Date` field type, the value should be transferred as text with the date formatted like `YYYY-MM-DD`, i.e. `"2018-03-25"`;
- For the `Date Time` field type, the value should be transferred as text with the date formatted in ISO8601 UTC, i.e `"2018-03-25T13:25:00.000Z"`;
- For the `True/False` field type, the value should be transferred like a boolean `true` or `false` value without quotation marks.

## Action unset contact's field value
Use this response to unset (clear) a contact’s field value. A Custom Field with the same name must exist in your bot.

    {
      "version": "v2",
      "content": {
        "type": "instagram", // "whatsapp" and "telegram" are also supported
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
        "quick_replies": [] // not supported for WhatsApp and Telegram
      }
    }
    
# Quick Replies
`quick_replies` property of server response is optional. Quick Replies cannot be used in the Dynamic Block of a content node if there are other blocks afterward. The Quick Reply description format is the same for buttons, it supports `content` and `node` types.

**Quick Reply buttons are not supported by WhatsApp and Telegram channels.**

## Go to node quick reply*

    {
      "version": "v2",
      "content": {
        "type": "instagram",
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
    
*`target` key should be linked to a node existing within the executed Flow. The node name can be found in its header, you need to use a unique name for the node connected with the link. If there are multiple nodes with similar names inside of the same Flow, transition behavior would not meet expectations. Go-to-node Quick Replies are not supported in Public API.
    
## Go to Flow Quick Reply

    {
      "version": "v2",
      "content": {
        "type": "instagram",
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

# Variables
In the Dynamic Block request body, you can use the `Full Contact Data` variable, which contains all contact’s information:

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
