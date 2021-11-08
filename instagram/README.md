{% raw %}

### See also
<a href="https://manychat.github.io/dynamic_block_docs/">Response Reference for Facebook Automation</a>

# Response Reference for Instagram Automation

## Response format
Response format for sending dynamic messages:

    {
      "version": "v2",
      "content": {
        "type": "instagram",
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
        "quick_replies": []
      }
    }
    
## Sending image
This response is used to send image files. Messenger supports JPG, PNG and GIF images. You can use `url`, `call`, `buy`, `flow` and `node` buttons.
The `"buttons"`, `"actions"`, `"quick_replies"` properties are optional.

    {
      "version": "v2",
      "content": {
        "type": "instagram",
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

## Sending gallery cards
This response is used to send a horizontal scrollable gallery. You can use `url`, `call`, `buy`, `flow` and `node` buttons.
The `"action_url"`, `"buttons"`, `"actions"`, `"quick_replies"` properties are optional.

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
`image_aspect_ratio` -  The aspect ratio used to render cards. You can use `horizontal` or `square` (default `horizontal`).

## Buttons
You can use buttons with each types: `url`, `flow`, `node`.
You can provide custom action to be performed with the button.
Actions for buttons must comply with same format and restrictions as described in [Actions format](#actions-format) bellow.
The `"actions"` property is optional.

    {
      "version": "v2",
      "content": {
        "type": "instagram",
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
    
### Url button
    
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
                "url": "https://manychat.com",
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
        "type": "instagram",
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
        "type": "instagram",
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
   
# Actions format
`actions` property of server response is optional.
## Action add tag
Use this response to add a tag to a subscriber. Tag with the same name must exist in your bot:

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
Quick reply description format is the same for buttons, it supports `content`, `node` types.

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
    
`target` key should be linked to a node existing within executed flow. Node name can be found in its header, you need to use unique name for node connected with link. If there are multiple nodes with similar names inside of the same flow, transition behaviour would not meet expectations. 
Go to node quick replies are not supported in Public API.
    
## Go to flow quick reply

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

In dynamic block request body, you can use `Full Subscriber Data`    variable, that contains all subscriber's information:

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
