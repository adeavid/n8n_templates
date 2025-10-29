# n8n Email Drip Campaign Workflows

This directory contains production-ready n8n workflow templates for automated email drip campaigns based on the research documented in `/research/email.md`.

## Available Workflows

### 1. Welcome & Onboarding Sequence
**File:** `welcome-onboarding-sequence.json`

**Type:** Time-based drip campaign
**Duration:** 7 days
**Emails:** 4 emails

**Trigger:** Daily schedule check (9 AM)

**Flow:**
1. Fetch new signups from Google Sheets
2. Filter users who haven't received emails yet
3. Generate personalized welcome email using AI
4. Wait 2 days → Send value/features email
5. Wait 2 days → Send free resource email
6. Wait 3 days → Send invitation/demo email
7. Mark campaign as completed in Google Sheets

**Key Features:**
- AI-powered email generation using OpenAI
- Personalization based on user data
- Automated tracking in Google Sheets
- Progressive value delivery

**Use Cases:**
- SaaS free trial onboarding
- New customer welcome sequences
- Course/membership onboarding
- Product launch sequences

---

### 2. Abandoned Cart Recovery
**File:** `abandoned-cart-recovery.json`

**Type:** Behavioral trigger campaign
**Duration:** 3 days
**Emails:** 3 emails

**Trigger:** Webhook when cart is abandoned

**Flow:**
1. Receive cart abandonment event via webhook
2. Validate cart data (email, cart value)
3. Log to Google Sheets
4. Wait 1 hour → Send gentle reminder
5. Wait 23 hours → Check if purchased
6. If not purchased → Send social proof email
7. Wait 2 days → Check purchase status again
8. If still not purchased → Calculate dynamic discount
9. Send discount offer (10-20% based on cart value)
10. Update campaign status

**Key Features:**
- Purchase status checking to prevent unnecessary emails
- Dynamic discount calculation based on cart value
- HTML-formatted emails with product details
- Exit conditions when purchase is completed
- Comprehensive cart tracking

**Use Cases:**
- E-commerce cart recovery
- Booking/reservation reminders
- Subscription signup abandonment
- Checkout process optimization

**Discount Logic:**
- Cart value $0-100: 10% discount
- Cart value $100-200: 15% discount
- Cart value $200+: 20% discount

---

### 3. B2B Lead Nurturing Sequence
**File:** `lead-nurturing-b2b.json`

**Type:** Multi-stage nurturing campaign
**Duration:** 24+ days
**Emails:** 4 emails + sales alert

**Trigger:** Webhook when lead form is submitted

**Flow:**
1. Receive lead capture event
2. Validate lead data
3. Create contact in CRM (HubSpot)
4. Enrich company data via API
5. Calculate lead score (0-100)
6. **Route by score:**
   - Hot leads (70+) → Alert sales team immediately
   - All leads continue to nurture sequence
7. Send resource delivery + welcome email
8. Wait 3 days → Send AI-generated educational content
9. Wait 7 days → Send product comparison email
10. Wait 14 days → Check engagement metrics
11. If engaged (2+ opens) → Send personal outreach
12. Update CRM status to Marketing Qualified Lead

**Key Features:**
- Intelligent lead scoring algorithm
- Company data enrichment
- CRM integration (HubSpot)
- AI-generated personalized content
- Engagement-based routing
- Hot lead sales alerts
- Industry-specific customization

**Lead Scoring Factors:**
- Company size (50+ employees: +20 pts, 200+: +30 pts)
- Estimated budget ($10k+: +25 pts)
- Industry match (tech/finance/healthcare: +15 pts)
- Job title (decision-maker roles: +20 pts)

**Segments:**
- **Hot (70-100 pts):** Immediate sales follow-up
- **Warm (40-69 pts):** Standard nurture sequence
- **Cold (0-39 pts):** Extended education sequence

**Use Cases:**
- B2B lead qualification and nurturing
- Whitepaper/ebook download follow-ups
- Webinar attendee nurturing
- Demo request sequences
- Enterprise sales pipelines

---

## Setup Requirements

### Credentials Needed

All workflows require the following n8n credentials to be configured:

1. **SMTP Account** (for sending emails)
   - ID: `smtp-credential`
   - Name: "SMTP account"
   - Required fields: Host, Port, Username, Password

2. **Google Sheets OAuth2** (for data storage)
   - ID: `google-sheets-credential`
   - Name: "Google Sheets account"
   - Required: OAuth2 authentication with Google

3. **OpenAI API** (for AI content generation)
   - ID: `openai-credential`
   - Name: "OpenAI account"
   - Required: OpenAI API key

4. **HubSpot API** (B2B workflow only)
   - ID: `hubspot-credential`
   - Name: "HubSpot account"
   - Required: HubSpot API key

### Google Sheets Structure

#### Welcome/Onboarding Sequence Sheet
**Sheet Name:** "New Signups"

| Column | Field | Description |
|--------|-------|-------------|
| A | email | User email address |
| B | name | Full name |
| C | signup_date | ISO date of signup |
| D | source | Signup source/campaign |
| E | email_sent | Status flag (empty = not sent) |
| F | completed_date | When sequence completed |

#### Abandoned Cart Sheet
**Sheet Name:** "Abandoned Carts"

| Column | Field | Description |
|--------|-------|-------------|
| A | email | Customer email |
| B | cart_items | JSON or text of items |
| C | cart_value | Total cart value |
| D | abandoned_at | Timestamp |
| E | status | pending/sequence_completed |
| F | last_email_sent | Last email timestamp |

### Webhook Configuration

For **Abandoned Cart** and **B2B Lead Nurturing** workflows:

1. Import the workflow into n8n
2. Activate the workflow
3. Copy the webhook URL from the webhook trigger node
4. Configure your application to send POST requests to the webhook URL

**Webhook Payload Examples:**

**Abandoned Cart:**
```json
{
  "email": "customer@example.com",
  "customer_name": "John Doe",
  "cart_items": [
    {"name": "Product A", "price": 29.99, "qty": 2},
    {"name": "Product B", "price": 49.99, "qty": 1}
  ],
  "cart_value": 109.97,
  "cart_url": "https://shop.com/cart/abc123",
  "cart_items_html": "<div>Product A x2</div><div>Product B x1</div>",
  "order_id": "order_12345"
}
```

**Lead Capture:**
```json
{
  "email": "lead@company.com",
  "first_name": "Jane",
  "last_name": "Smith",
  "company": "Acme Corp",
  "job_title": "Director of Marketing",
  "phone": "+1-555-0123",
  "industry": "Technology",
  "company_size": 150,
  "estimated_budget": 50000,
  "source": "whitepaper_download",
  "resource_name": "2025 Marketing Automation Guide",
  "resource_url": "https://company.com/downloads/guide.pdf"
}
```

---

## Customization Guide

### Modifying Email Content

All email nodes have editable HTML templates. Key customization points:

1. **Subject lines** - Update in each Email Send node's "subject" field
2. **From addresses** - Change "fromEmail" parameter
3. **Branding** - Replace `[Company Name]` placeholders
4. **CTAs** - Update button URLs and text
5. **Images** - Add `<img>` tags to email HTML

### Adjusting Wait Times

Each Wait node can be configured:
- Change "amount" parameter (number)
- Change "unit" parameter (hours, days, weeks)

**Recommended timings:**
- **Welcome sequences:** 2-3 days between emails
- **Abandoned cart:** 1 hour, then 24 hours, then 3 days
- **B2B nurturing:** 3-7-14 day intervals

### AI Content Generation

The OpenAI nodes use GPT-3.5 by default. To customize:

1. **Temperature** (0-1): Controls creativity
   - 0.7 = balanced (recommended)
   - 0.9 = more creative
   - 0.5 = more focused

2. **System Message**: Defines AI persona and style
3. **Prompt**: Specific instructions for content generation

Example customization:
```
"systemMessage": "You are a friendly, casual brand voice expert. Write like you're talking to a friend."
"prompt": "Create a fun, emoji-filled welcome email for {{$json.name}}..."
```

### Lead Scoring Customization

Edit the "Calculate Lead Score" Code node to adjust scoring:

```javascript
let leadScore = 0;

// Customize point values
if (companySize > 100) leadScore += 30;  // Change threshold/points
if (budget > 50000) leadScore += 40;      // Adjust budget criteria
if (industry === 'your-target-industry') leadScore += 25;

// Change segment thresholds
let segment = 'cold';
if (leadScore >= 80) segment = 'hot';     // More selective
else if (leadScore >= 50) segment = 'warm';
```

---

## Monitoring & Analytics

### Key Metrics to Track

1. **Email Deliverability**
   - Open rates
   - Click-through rates
   - Bounce rates
   - Unsubscribe rates

2. **Campaign Performance**
   - Conversion rates per sequence
   - Time to conversion
   - Revenue generated
   - ROI per campaign

3. **Technical Metrics**
   - Workflow execution success rate
   - Failed email sends
   - Webhook delivery failures
   - API rate limiting issues

### n8n Workflow Monitoring

- **Executions tab**: View all workflow runs
- **Webhook logs**: Check incoming webhook data
- **Error notifications**: Configure alerts for failed executions
- **Execution data**: Inspect data flowing through each node

### Recommended Integrations

Enhance monitoring by connecting:
- **Google Analytics**: Track email click conversions
- **Mixpanel/Amplitude**: User behavior analytics
- **Slack**: Real-time alerts for hot leads or errors
- **DataDog/Sentry**: Technical monitoring and error tracking

---

## Best Practices

### Email Deliverability

1. **Warm up your sending domain** - Start with low volume
2. **Clean email lists** - Remove bounces and invalid emails
3. **Authenticate** - Set up SPF, DKIM, DMARC records
4. **Monitor sender reputation** - Use tools like SenderScore
5. **Avoid spam triggers** - Test emails with Mail-Tester

### Content Optimization

1. **Mobile-first design** - 60%+ open on mobile
2. **Clear CTAs** - One primary action per email
3. **Preview text** - First 90 characters matter
4. **Personalization** - Use name, company, behavior data
5. **A/B testing** - Test subject lines and content variants

### Technical Reliability

1. **Error handling** - Add try/catch nodes for critical operations
2. **Webhook validation** - Verify incoming data format
3. **Rate limiting** - Add delays for API-heavy workflows
4. **Backup data** - Export workflow configurations regularly
5. **Test mode** - Use test email addresses before going live

### Compliance

1. **CAN-SPAM Act** (US)
   - Include physical address
   - Clear unsubscribe link
   - Honest subject lines

2. **GDPR** (EU)
   - Obtain explicit consent
   - Allow data export/deletion
   - Document data processing

3. **CASL** (Canada)
   - Express or implied consent
   - Clear identification
   - Unsubscribe mechanism

---

## Troubleshooting

### Common Issues

**Problem:** Emails not sending
- Check SMTP credentials
- Verify sender domain authentication
- Review n8n execution logs for errors
- Test SMTP connection manually

**Problem:** Webhooks not triggering
- Confirm workflow is activated
- Check webhook URL is correct
- Verify payload format matches expected structure
- Review webhook logs in n8n

**Problem:** AI content generation failing
- Verify OpenAI API key is valid
- Check API usage limits
- Review prompt for formatting errors
- Ensure temperature is between 0-1

**Problem:** Wait nodes not resuming
- Verify webhook IDs are unique
- Check n8n has persistent storage configured
- Ensure workflow hasn't been deactivated
- Review execution history for stuck workflows

**Problem:** Google Sheets updates failing
- Confirm OAuth2 credentials are valid
- Check sheet name matches exactly
- Verify column headers exist
- Review API quota limits

### Debug Mode

Enable detailed logging:
1. Click workflow settings (gear icon)
2. Enable "Save Execution Progress"
3. Set "Save Data on Error"
4. Run workflow and inspect execution data

---

## Performance Optimization

### For High Volume (1000+ emails/day)

1. **Batch processing** - Process leads in groups
2. **Queue management** - Use RabbitMQ or Redis Queue nodes
3. **Rate limiting** - Add delays to respect API limits
4. **Parallel execution** - Split workflows for different segments
5. **Caching** - Store frequently accessed data in memory

### Resource Management

- **Reduce AI calls** - Pre-generate templates when possible
- **Optimize sheet operations** - Batch updates instead of row-by-row
- **Webhook response time** - Return 200 immediately, process async
- **Memory usage** - Clear unnecessary data between nodes

---

## Scaling Considerations

### When to Split Workflows

Consider breaking workflows into smaller pieces when:
- Execution time exceeds 5 minutes regularly
- Handling multiple campaign types in one workflow
- Different teams manage different parts
- Need independent testing/deployment

### Architecture Patterns

**Pattern 1: Centralized Queue**
```
Webhook → Queue → Worker Workflows (multiple)
```

**Pattern 2: Event-Driven**
```
Trigger → Event Bus → Specialized Workflows
```

**Pattern 3: Microservices**
```
Lead Capture → Scoring Service → Routing Service → Email Service
```

---

## Migration & Updates

### Importing Workflows

1. Open n8n interface
2. Click "Workflows" → "Import from File"
3. Select `.json` file
4. Update all credential references
5. Test with sample data
6. Activate workflow

### Updating Existing Workflows

1. **Export current version** (backup)
2. Make changes in test environment
3. Test thoroughly with production-like data
4. Document changes in workflow notes
5. Schedule deployment during low-traffic period
6. Monitor executions closely after update

### Version Control

Recommended practices:
- Store workflow JSON files in git
- Use semantic versioning (v1.0.0, v1.1.0)
- Include changelog in README
- Tag releases in git
- Keep last 3 versions accessible

---

## Support & Resources

### Official Documentation
- [n8n Documentation](https://docs.n8n.io/)
- [n8n Workflow Templates](https://n8n.io/workflows/)
- [n8n Community Forum](https://community.n8n.io/)

### Email Marketing Resources
- See `/research/email.md` for comprehensive email drip campaign research
- [Mailchimp Email Marketing Benchmarks](https://mailchimp.com/resources/email-marketing-benchmarks/)
- [Really Good Emails](https://reallygoodemails.com/) - Design inspiration

### Technical Support
- n8n GitHub Issues
- n8n Discord Community
- Stack Overflow (tag: n8n)

---

## Changelog

### Version 1.0.0 (2025-10-29)
- Initial release
- Welcome & Onboarding Sequence workflow
- Abandoned Cart Recovery workflow
- B2B Lead Nurturing Sequence workflow
- Complete documentation and setup guides

---

## License & Usage

These workflow templates are provided as-is for use in n8n automation projects. Feel free to customize and adapt for your specific use cases.

**Created by:** Claude B
**Date:** October 29, 2025
**Based on research:** `/research/email.md`
