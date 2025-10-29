# LinkedIn Automation Technical Implementation Guide

## LinkedIn API Configuration

### Rate Limits

**Important:** LinkedIn does not publish specific rate limit numbers publicly. Instead:

1. **Check via Developer Portal**
   - Navigate to your app in the Developer Portal
   - Go to Analytics tab
   - View usage and rate limits for endpoints (must have made at least 1 request today)

2. **Monitoring**
   - Developer Admins receive email alerts at 75% quota usage
   - Monitor response headers for real-time tracking
   - Track remaining quota via API responses

3. **Additive Throttle Limits**
   - APIs with overlapping usage (e.g., UGC Post + Social Actions) have combined limits
   - Plan accordingly when using multiple posting endpoints

4. **Official Documentation**
   - Microsoft Learn: https://learn.microsoft.com/en-us/linkedin/shared/api-guide/concepts/rate-limits

### OAuth 2.0 Authentication Setup

#### Prerequisites
- LinkedIn account
- LinkedIn Company Page (for organization posting)
- LinkedIn Developer App

#### Setup Process

**Step 1: Create LinkedIn Developer App**
```
1. Log into LinkedIn
2. Navigate to LinkedIn Developer Portal
3. Create new app
4. Enter app name (e.g., "n8n integration")
5. Associate with LinkedIn Company Page
```

**Step 2: Configure Products/APIs**
```
1. Go to Products tab
2. Select required APIs:
   - Share on LinkedIn (for posting)
   - Sign In with LinkedIn (for authentication)
   - Marketing Developer Platform (for ads/analytics)
```

**Step 3: Get Credentials**
```
1. Open Auth tab
2. Copy Client ID
3. Copy Primary Client Secret
4. Note your Redirect URI
```

**Step 4: n8n Configuration**

For n8n Cloud:
```
1. Add LinkedIn node to workflow
2. Create new credential
3. Select "Connect my account"
4. Authenticate via browser
```

For Self-Hosted n8n:
```
1. Add LinkedIn node
2. Create new credential
3. Choose OAuth method:
   - Community Management OAuth2 (new apps)
   - OAuth2 (legacy apps)
4. Enter Client ID
5. Enter Client Secret
6. Configure redirect URI: https://your-n8n-instance/rest/oauth2-credential/callback
7. Enable "Organization Support" if posting as company
```

#### Scopes Required

**Personal Profile Posting:**
- `w_member_social` - Write posts as member

**Organization Posting:**
- `w_organization_social` - Write posts as organization
- Requires Community Management App Review approval

**Reading Data:**
- `r_liteprofile` - Read basic profile
- `r_emailaddress` - Read email

### n8n Workflow JSON Structure

#### Basic Structure

```json
{
  "name": "LinkedIn Automation Workflow",
  "nodes": [
    {
      "parameters": {},
      "id": "unique-node-id",
      "name": "Node Name",
      "type": "n8n-nodes-base.nodeName",
      "typeVersion": 1,
      "position": [x, y]
    }
  ],
  "connections": {
    "Source Node": {
      "main": [
        [
          {
            "node": "Target Node",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "settings": {},
  "staticData": null
}
```

#### Connection Patterns

**Linear Flow:**
```json
"connections": {
  "Trigger": {
    "main": [[{"node": "Process", "type": "main", "index": 0}]]
  },
  "Process": {
    "main": [[{"node": "LinkedIn", "type": "main", "index": 0}]]
  }
}
```

**Conditional Split:**
```json
"connections": {
  "IF": {
    "main": [
      [{"node": "True Branch", "type": "main", "index": 0}],
      [{"node": "False Branch", "type": "main", "index": 0}]
    ]
  }
}
```

**Multiple Outputs:**
```json
"connections": {
  "Split": {
    "main": [
      [
        {"node": "LinkedIn", "type": "main", "index": 0},
        {"node": "Email", "type": "main", "index": 0}
      ]
    ]
  }
}
```

#### Data Structure

All data between nodes is an array of JSON objects:

```json
[
  {
    "json": {
      "field1": "value1",
      "field2": "value2"
    },
    "binary": {}
  },
  {
    "json": {
      "field1": "value3",
      "field2": "value4"
    }
  }
]
```

## LinkedIn Node Configuration

### Node Parameters

#### Resource: Post

**Operation: Create**

Required Parameters:
```json
{
  "postAs": "person",  // or "organization"
  "text": "Your post content here"
}
```

Optional Parameters:
```json
{
  "mediaCategory": "none",  // "none", "article", "image"
  "visibility": "PUBLIC",   // "PUBLIC", "CONNECTIONS"
  "urn": "123456789"       // Organization ID (numbers only)
}
```

**Media Categories:**

1. **None:** Text-only post
2. **Article:** Include article URL
   - Additional field: `articleUrl`
3. **Image:** Include image
   - Upload via binary data or URL

#### URN Format

For organization posting:
- ✅ Correct: `03262013`
- ❌ Incorrect: `urn:li:company:03262013`

Only use the numeric ID.

### Example Workflow Configurations

#### Simple Text Post

```json
{
  "parameters": {
    "resource": "post",
    "operation": "create",
    "postAs": "person",
    "text": "Check out our latest blog post about automation!"
  },
  "name": "LinkedIn Post",
  "type": "n8n-nodes-base.linkedIn",
  "credentials": {
    "linkedInOAuth2Api": {
      "id": "1",
      "name": "LinkedIn account"
    }
  }
}
```

#### Post with Image

```json
{
  "parameters": {
    "resource": "post",
    "operation": "create",
    "postAs": "person",
    "text": "Our quarterly results are in!",
    "mediaCategory": "image",
    "additionalFields": {
      "visibility": "PUBLIC"
    }
  },
  "name": "LinkedIn Post with Image"
}
```

#### Organization Post

```json
{
  "parameters": {
    "resource": "post",
    "operation": "create",
    "postAs": "organization",
    "text": "We're hiring! Join our team.",
    "person": "",
    "organization": "12345678"
  },
  "name": "Company Post"
}
```

## Complete Workflow Examples

### 1. Scheduled Daily Post from Notion

```json
{
  "name": "Daily LinkedIn Post",
  "nodes": [
    {
      "parameters": {
        "rule": {
          "interval": [{"field": "cronExpression", "expression": "0 9 * * *"}]
        }
      },
      "name": "Schedule Trigger",
      "type": "n8n-nodes-base.scheduleTrigger",
      "position": [250, 300]
    },
    {
      "parameters": {
        "resource": "databasePage",
        "operation": "getAll",
        "databaseId": "your-notion-db-id",
        "filterType": "manual",
        "filters": {
          "conditions": [
            {
              "key": "Status",
              "condition": "equals",
              "value": "Ready to Post"
            }
          ]
        },
        "limit": 1
      },
      "name": "Get Notion Post",
      "type": "n8n-nodes-base.notion",
      "position": [450, 300]
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "name": "postText",
              "value": "={{ $json.properties.Content.rich_text[0].plain_text }}"
            }
          ]
        }
      },
      "name": "Format Content",
      "type": "n8n-nodes-base.set",
      "position": [650, 300]
    },
    {
      "parameters": {
        "resource": "post",
        "operation": "create",
        "postAs": "person",
        "text": "={{ $json.postText }}"
      },
      "name": "Post to LinkedIn",
      "type": "n8n-nodes-base.linkedIn",
      "position": [850, 300]
    },
    {
      "parameters": {
        "resource": "databasePage",
        "operation": "update",
        "pageId": "={{ $('Get Notion Post').item.json.id }}",
        "propertiesUi": {
          "propertyValues": [
            {
              "key": "Status",
              "statusValue": "Posted"
            }
          ]
        }
      },
      "name": "Update Notion Status",
      "type": "n8n-nodes-base.notion",
      "position": [1050, 300]
    }
  ],
  "connections": {
    "Schedule Trigger": {
      "main": [[{"node": "Get Notion Post", "type": "main", "index": 0}]]
    },
    "Get Notion Post": {
      "main": [[{"node": "Format Content", "type": "main", "index": 0}]]
    },
    "Format Content": {
      "main": [[{"node": "Post to LinkedIn", "type": "main", "index": 0}]]
    },
    "Post to LinkedIn": {
      "main": [[{"node": "Update Notion Status", "type": "main", "index": 0}]]
    }
  }
}
```

### 2. AI-Generated Post with Approval

```json
{
  "name": "AI LinkedIn Post with Approval",
  "nodes": [
    {
      "parameters": {},
      "name": "Manual Trigger",
      "type": "n8n-nodes-base.manualTrigger",
      "position": [250, 300]
    },
    {
      "parameters": {
        "operation": "get",
        "sheetId": "your-sheet-id",
        "range": "Sheet1!A:C"
      },
      "name": "Get Topics from Sheets",
      "type": "n8n-nodes-base.googleSheets",
      "position": [450, 300]
    },
    {
      "parameters": {
        "operation": "message",
        "messages": {
          "messages": [
            {
              "role": "user",
              "content": "Write a professional LinkedIn post about: {{ $json.Topic }}"
            }
          ]
        }
      },
      "name": "Generate with OpenAI",
      "type": "n8n-nodes-base.openAi",
      "position": [650, 300]
    },
    {
      "parameters": {
        "fromEmail": "automation@company.com",
        "toEmail": "manager@company.com",
        "subject": "LinkedIn Post Approval Required",
        "text": "=Please review:\\n\\n{{ $json.choices[0].message.content }}\\n\\nApprove: {{$workflow.url}}/approve\\nReject: {{$workflow.url}}/reject"
      },
      "name": "Send Approval Email",
      "type": "n8n-nodes-base.emailSend",
      "position": [850, 300]
    },
    {
      "parameters": {
        "httpMethod": "POST",
        "path": "approve",
        "responseMode": "lastNode"
      },
      "name": "Webhook Approval",
      "type": "n8n-nodes-base.webhook",
      "position": [1050, 200]
    },
    {
      "parameters": {
        "conditions": {
          "string": [
            {
              "value1": "={{ $json.approved }}",
              "value2": "true"
            }
          ]
        }
      },
      "name": "Check Approval",
      "type": "n8n-nodes-base.if",
      "position": [1250, 300]
    },
    {
      "parameters": {
        "resource": "post",
        "operation": "create",
        "postAs": "person",
        "text": "={{ $('Generate with OpenAI').item.json.choices[0].message.content }}"
      },
      "name": "Post to LinkedIn",
      "type": "n8n-nodes-base.linkedIn",
      "position": [1450, 200]
    }
  ],
  "connections": {
    "Manual Trigger": {
      "main": [[{"node": "Get Topics from Sheets", "type": "main", "index": 0}]]
    },
    "Get Topics from Sheets": {
      "main": [[{"node": "Generate with OpenAI", "type": "main", "index": 0}]]
    },
    "Generate with OpenAI": {
      "main": [[{"node": "Send Approval Email", "type": "main", "index": 0}]]
    },
    "Send Approval Email": {
      "main": [[{"node": "Webhook Approval", "type": "main", "index": 0}]]
    },
    "Webhook Approval": {
      "main": [[{"node": "Check Approval", "type": "main", "index": 0}]]
    },
    "Check Approval": {
      "main": [
        [{"node": "Post to LinkedIn", "type": "main", "index": 0}],
        []
      ]
    }
  }
}
```

### 3. Lead Generation with AI Scoring

```json
{
  "name": "LinkedIn Lead Generation",
  "nodes": [
    {
      "parameters": {
        "rule": {
          "interval": [{"field": "hours", "hoursInterval": 6}]
        }
      },
      "name": "Schedule Trigger",
      "type": "n8n-nodes-base.scheduleTrigger",
      "position": [250, 300]
    },
    {
      "parameters": {
        "url": "https://api.anyscale.com/linkedin/search",
        "authentication": "genericCredentialType",
        "options": {
          "queryParameters": {
            "parameters": [
              {"name": "keywords", "value": "Software Engineer"},
              {"name": "location", "value": "San Francisco"}
            ]
          }
        }
      },
      "name": "Search LinkedIn Profiles",
      "type": "n8n-nodes-base.httpRequest",
      "position": [450, 300]
    },
    {
      "parameters": {
        "batchSize": 10,
        "options": {}
      },
      "name": "Split in Batches",
      "type": "n8n-nodes-base.splitInBatches",
      "position": [650, 300]
    },
    {
      "parameters": {
        "operation": "message",
        "messages": {
          "messages": [
            {
              "role": "system",
              "content": "Score this lead 1-10 based on fit for our SaaS product."
            },
            {
              "role": "user",
              "content": "=Name: {{ $json.name }}\\nHeadline: {{ $json.headline }}\\nCompany: {{ $json.company }}"
            }
          ]
        }
      },
      "name": "AI Lead Scoring",
      "type": "n8n-nodes-base.openAi",
      "position": [850, 300]
    },
    {
      "parameters": {
        "conditions": {
          "number": [
            {
              "value1": "={{ parseInt($json.choices[0].message.content) }}",
              "operation": "largerEqual",
              "value2": 7
            }
          ]
        }
      },
      "name": "Filter High-Quality Leads",
      "type": "n8n-nodes-base.if",
      "position": [1050, 300]
    },
    {
      "parameters": {
        "resource": "contact",
        "operation": "create",
        "properties": {
          "propertyValues": [
            {"name": "firstname", "value": "={{ $json.firstName }}"},
            {"name": "lastname", "value": "={{ $json.lastName }}"},
            {"name": "linkedin_url", "value": "={{ $json.profileUrl }}"},
            {"name": "lead_score", "value": "={{ $json.score }}"}
          ]
        }
      },
      "name": "Add to CRM",
      "type": "n8n-nodes-base.hubspot",
      "position": [1250, 200]
    }
  ],
  "connections": {
    "Schedule Trigger": {
      "main": [[{"node": "Search LinkedIn Profiles", "type": "main", "index": 0}]]
    },
    "Search LinkedIn Profiles": {
      "main": [[{"node": "Split in Batches", "type": "main", "index": 0}]]
    },
    "Split in Batches": {
      "main": [[{"node": "AI Lead Scoring", "type": "main", "index": 0}]]
    },
    "AI Lead Scoring": {
      "main": [[{"node": "Filter High-Quality Leads", "type": "main", "index": 0}]]
    },
    "Filter High-Quality Leads": {
      "main": [
        [{"node": "Add to CRM", "type": "main", "index": 0}],
        []
      ]
    },
    "Add to CRM": {
      "main": [[{"node": "Split in Batches", "type": "main", "index": 0}]]
    }
  }
}
```

## Best Practices

### Error Handling

**Add Error Workflow:**
```json
{
  "parameters": {
    "workflowId": "error-handler-workflow-id"
  },
  "name": "Error Trigger",
  "type": "n8n-nodes-base.errorTrigger"
}
```

**Retry Logic:**
```json
{
  "retryOnFail": true,
  "maxTries": 3,
  "waitBetweenTries": 1000
}
```

### Rate Limiting Protection

**Add Wait Node:**
```json
{
  "parameters": {
    "amount": 2,
    "unit": "seconds"
  },
  "name": "Wait",
  "type": "n8n-nodes-base.wait"
}
```

**Batch Processing:**
```json
{
  "parameters": {
    "batchSize": 5,
    "options": {
      "reset": false
    }
  },
  "name": "Split in Batches",
  "type": "n8n-nodes-base.splitInBatches"
}
```

### Logging

**Add to Google Sheets:**
```json
{
  "parameters": {
    "operation": "append",
    "sheetId": "log-sheet-id",
    "columns": {
      "mappings": [
        {"column": "Timestamp", "value": "={{ $now }}"},
        {"column": "Status", "value": "={{ $json.status }}"},
        {"column": "Message", "value": "={{ $json.message }}"}
      ]
    }
  },
  "name": "Log to Sheets",
  "type": "n8n-nodes-base.googleSheets"
}
```

### Security Considerations

1. **Credential Management**
   - Store all credentials in n8n's credential manager
   - Never hardcode API keys in workflow JSON
   - Use environment variables for sensitive data

2. **Webhook Security**
   - Enable webhook authentication
   - Use HTTPS only
   - Validate incoming payloads

3. **Data Sanitization**
   - Validate user input
   - Escape special characters in text
   - Sanitize URLs before posting

## Troubleshooting

### Common Issues

**OAuth Connection Failures:**
- Verify redirect URI matches exactly
- Check app has required scopes enabled
- Ensure LinkedIn app is not in draft mode

**Rate Limit Errors:**
- Implement exponential backoff
- Add delays between requests
- Monitor usage in Developer Portal

**Post Not Appearing:**
- Verify visibility settings
- Check account permissions
- Confirm URN format for organizations

**Image Upload Failures:**
- Ensure proper MIME type
- Check file size limits (5MB max)
- Verify binary data encoding

### Debug Mode

Enable in workflow settings:
```json
{
  "settings": {
    "saveExecutionProgress": true,
    "saveManualExecutions": true,
    "saveDataErrorExecution": "all",
    "saveDataSuccessExecution": "all"
  }
}
```

## Performance Optimization

### Caching Strategy

**Use Static Data:**
```javascript
// In Function node
const cache = $workflow.staticData;
if (!cache.tokens) {
  cache.tokens = {};
}
```

**Database Caching:**
- Store frequently accessed data in Redis
- Cache API responses with TTL
- Implement cache invalidation logic

### Parallel Processing

**Split Execution:**
```json
{
  "parameters": {
    "mode": "parallel",
    "batchSize": 10
  }
}
```

### Resource Management

1. Limit concurrent executions
2. Use queue mode for high-volume workflows
3. Implement cleanup for old execution data
4. Monitor memory usage

## Next Steps

1. Review workflow templates on n8n.io
2. Set up development environment
3. Test with LinkedIn sandbox (if available)
4. Implement monitoring and alerts
5. Document custom workflows
6. Train team on best practices
