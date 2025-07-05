# n8n Workflow Documentation

This document provides a detailed analysis of the n8n workflows. Each section outlines the purpose, trigger, and operational flow of a specific workflow.

---

## 1. 2/Government_NGO/public_record_email_update.json

**Workflow:** Public Record Email Update

This workflow automates the processing of public record email updates. It is triggered by an HTTP POST request, processes the incoming text data using a Retrieval-Augmented Generation (RAG) pipeline, and logs the results in a Google Sheet.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/public-record-email-update`

### Workflow Steps

1.  **Webhook Trigger:** Receives incoming data to initiate the workflow.
2.  **Text Splitter:** Breaks down the input text into smaller, manageable chunks.
3.  **Embeddings (Cohere):** Converts the text chunks into vector embeddings using the `embed-english-v3.0` model.
4.  **Pinecone Insert:** Stores the generated embeddings in a Pinecone vector database under the `public_record_email_update` index.
5.  **Pinecone Query:** Retrieves relevant vector data from the Pinecone index to be used as context.
6.  **RAG Agent (OpenAI):** Combines the retrieved vector context with a chat model to process the data and generate a meaningful response.
7.  **Append Sheet:** Appends the output from the RAG Agent to a Google Sheet named "Log".
8.  **Error Handling:** If any step in the RAG agent process fails, a notification is sent to the `#alerts` channel in Slack.

---

## 2. 2/Government_NGO/public_form_auto_triage.json

**Workflow:** Public Form Auto Triage

This workflow is designed to automatically triage public form submissions. It uses a RAG pipeline with a Supabase vector store and an Anthropic chat model to process and categorize form data, with the final output logged in a Google Sheet.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/public-form-auto-triage`

### Workflow Steps

1.  **Webhook Trigger:** Starts the workflow upon receiving a form submission.
2.  **Text Splitter:** Divides the form data into smaller text segments.
3.  **Embeddings (Cohere):** Creates vector embeddings from the text segments using the `embed-english-v3.0` model.
4.  **Supabase Insert:** Inserts the embeddings into a Supabase vector store in the `public_form_auto_triage` index.
5.  **Supabase Query:** Queries the Supabase index to retrieve contextual information.
6.  **RAG Agent (Anthropic):** Processes the form data using the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Logs the agent's output in a Google Sheet named "Log".
8.  **Error Handling:** Sends an alert to the `#alerts` Slack channel if the RAG agent encounters an error.

---

## 3. 2/DevOps/github_commit_jenkins.json

**Workflow:** GitHub Commit Jenkins

This workflow automates processes related to GitHub commits, potentially for CI/CD pipelines involving Jenkins. It processes commit data through a RAG pipeline using Supabase and OpenAI, and logs the outcome.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/github-commit-jenkins`

### Workflow Steps

1.  **Webhook Trigger:** Initiated by a webhook, likely from a GitHub repository on a new commit.
2.  **Text Splitter:** Breaks down the commit message or related data into smaller chunks.
3.  **Embeddings (OpenAI):** Generates vector embeddings from the text chunks using the `text-embedding-3-small` model.
4.  **Supabase Insert:** Stores the embeddings in a Supabase vector store under the `github_commit_jenkins` index.
5.  **Supabase Query:** Retrieves relevant data from the Supabase index.
6.  **RAG Agent (OpenAI):** Processes the commit data with context from the vector store and an OpenAI chat model.
7.  **Append Sheet:** Appends the result to a Google Sheet named "Log".
8.  **Error Handling:** If the agent fails, a notification is sent to the `#alerts` Slack channel.

---

## 4. 2/Email_Automation/auto_reply_to_faqs.json

**Workflow:** Auto Reply to FAQs

This workflow provides automated responses to frequently asked questions. It leverages a RAG pipeline with Pinecone and Anthropic to understand and answer queries, logging each interaction.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/auto-reply-to-faqs`

### Workflow Steps

1.  **Webhook Trigger:** Receives a query, likely from an email or chat interface.
2.  **Text Splitter:** Splits the incoming query into smaller text chunks.
3.  **Embeddings (Cohere):** Converts the text chunks into vector embeddings.
4.  **Pinecone Insert:** Stores the embeddings in a Pinecone vector store under the `auto_reply_to_faqs` index.
5.  **Pinecone Query:** Retrieves relevant FAQ answers or context from the Pinecone index.
6.  **RAG Agent (Anthropic):** Generates a response using the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Logs the interaction details in a Google Sheet named "Log".
8.  **Error Handling:** Sends an error message to the `#alerts` Slack channel upon failure.

---

## 5. 2/Email_Automation/product_launch_email.json

**Workflow:** Product Launch Email

This workflow automates tasks related to sending out product launch emails. It uses a RAG pipeline with Supabase and OpenAI to generate or manage email content, and logs the activity.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/product-launch-email`

### Workflow Steps

1.  **Webhook Trigger:** Initiated by an event, such as a new product being added or a scheduled launch.
2.  **Text Splitter:** Processes incoming text data related to the product launch.
3.  **Embeddings (Cohere):** Creates vector embeddings from the text data.
4.  **Supabase Insert:** Stores the embeddings in a Supabase vector store in the `product_launch_email` index.
5.  **Supabase Query:** Retrieves contextual information from the Supabase index.
6.  **RAG Agent (OpenAI):** Generates email content or performs other tasks using the retrieved context and an OpenAI chat model.
7.  **Append Sheet:** Records the outcome in a Google Sheet named "Log".
8.  **Error Handling:** Notifies the `#alerts` Slack channel if the RAG agent fails.
---

## 6. 2/Email_Automation/mailchimp_campaign_tracking.json

**Workflow:** Mailchimp Campaign Tracking

This workflow automates the tracking of Mailchimp campaigns. It is triggered by a webhook, processes campaign data using a RAG pipeline with Supabase and Anthropic, and logs the results in a Google Sheet.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/mailchimp-campaign-tracking`

### Workflow Steps

1.  **Webhook Trigger:** Receives data from Mailchimp to start the workflow.
2.  **Text Splitter:** Breaks down the campaign data into smaller text chunks.
3.  **Embeddings (OpenAI):** Converts the text chunks into vector embeddings using the `text-embedding-3-small` model.
4.  **Supabase Insert:** Stores the embeddings in a Supabase vector store under the `mailchimp_campaign_tracking` index.
5.  **Supabase Query:** Retrieves relevant data from the Supabase index for context.
6.  **RAG Agent (Anthropic):** Processes the campaign data with the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Appends the agent's output to a Google Sheet named "Log".
8.  **Error Handling:** Sends an alert to the `#alerts` Slack channel if the RAG agent fails.

---

## 7. 2/Email_Automation/auto_archive_promotions.json

**Workflow:** Auto Archive Promotions

This workflow automates the archiving of promotional emails. It uses a RAG pipeline with Pinecone and OpenAI to process email data and logs the outcome.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/auto-archive-promotions`

### Workflow Steps

1.  **Webhook Trigger:** Initiated by an incoming email or a similar event.
2.  **Text Splitter:** Splits the email content into smaller text segments.
3.  **Embeddings (OpenAI):** Creates vector embeddings from the text segments using the `text-embedding-3-small` model.
4.  **Pinecone Insert:** Inserts the embeddings into a Pinecone vector store in the `auto_archive_promotions` index.
5.  **Pinecone Query:** Queries the Pinecone index to retrieve contextual information.
6.  **RAG Agent (OpenAI):** Processes the email data using the retrieved context and an OpenAI chat model to decide whether to archive it.
7.  **Append Sheet:** Logs the decision in a Google Sheet named "Log".
8.  **Error Handling:** Sends an alert to the `#alerts` Slack channel if the RAG agent encounters an error.

---

## 8. 2/Email_Automation/follow-up_emails.json

**Workflow:** Follow-up Emails

This workflow automates the sending of follow-up emails. It processes email data through a RAG pipeline using Weaviate and Anthropic, and logs the activity.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/follow-up-emails`

### Workflow Steps

1.  **Webhook Trigger:** Triggered by an event, such as a previous email being sent or a specific time delay.
2.  **Text Splitter:** Breaks down relevant data into smaller chunks.
3.  **Embeddings (OpenAI):** Generates vector embeddings from the text chunks using the `text-embedding-3-small` model.
4.  **Weaviate Insert:** Stores the embeddings in a Weaviate vector store under the `follow-up_emails` index.
5.  **Weaviate Query:** Retrieves relevant data from the Weaviate index.
6.  **RAG Agent (Anthropic):** Generates a follow-up email or determines the next action using the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Appends the result to a Google Sheet named "Log".
8.  **Error Handling:** If the agent fails, a notification is sent to the `#alerts` Slack channel.

---

## 9. 2/Email_Automation/forward_attachments.json

**Workflow:** Forward Attachments

This workflow automates the forwarding of email attachments. It uses a RAG pipeline with Pinecone and OpenAI to process email data and determine where to forward attachments.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/forward-attachments`

### Workflow Steps

1.  **Webhook Trigger:** Receives an email with attachments.
2.  **Text Splitter:** Splits the email body or other relevant text into smaller chunks.
3.  **Embeddings (OpenAI):** Converts the text chunks into vector embeddings.
4.  **Pinecone Insert:** Stores the embeddings in a Pinecone vector store under the `forward_attachments` index.
5.  **Pinecone Query:** Retrieves forwarding rules or context from the Pinecone index.
6.  **RAG Agent (OpenAI):** Determines the forwarding action based on the retrieved context and an OpenAI chat model.
7.  **Append Sheet:** Logs the forwarding action in a Google Sheet named "Log".
8.  **Error Handling:** Sends an error message to the `#alerts` Slack channel upon failure.

---

## 10. 2/Email_Automation/daily_email_digest.json

**Workflow:** Daily Email Digest

This workflow creates and sends a daily email digest. It uses a RAG pipeline with Supabase and Anthropic to gather and summarize information, and logs the activity.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/daily-email-digest`

### Workflow Steps

1.  **Webhook Trigger:** Initiated on a daily schedule.
2.  **Text Splitter:** Processes the text data to be included in the digest.
3.  **Embeddings (OpenAI):** Creates vector embeddings from the text data.
4.  **Supabase Insert:** Stores the embeddings in a Supabase vector store in the `daily_email_digest` index.
5.  **Supabase Query:** Retrieves the information to be summarized from the Supabase index.
6.  **RAG Agent (Anthropic):** Generates the email digest summary using the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Records the activity in a Google Sheet named "Log".
8.  **Error Handling:** Notifies the `#alerts` Slack channel if the RAG agent fails.
---

## 11. 2/Email_Automation/sendgrid_bounce_alert.json

**Workflow:** SendGrid Bounce Alert

This workflow automates the handling of SendGrid bounce alerts. It uses a RAG pipeline with Weaviate and Anthropic to process bounce data and logs the results.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/sendgrid-bounce-alert`

### Workflow Steps

1.  **Webhook Trigger:** Receives bounce notifications from SendGrid.
2.  **Text Splitter:** Breaks down the bounce data into smaller text chunks.
3.  **Embeddings (OpenAI):** Converts the text chunks into vector embeddings using the `text-embedding-3-small` model.
4.  **Weaviate Insert:** Stores the embeddings in a Weaviate vector store under the `sendgrid_bounce_alert` index.
5.  **Weaviate Query:** Retrieves relevant data from the Weaviate index for context.
6.  **RAG Agent (Anthropic):** Processes the bounce data with the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Appends the agent's output to a Google Sheet named "Log".
8.  **Error Handling:** Sends an alert to the `#alerts` Slack channel if the RAG agent fails.

---

## 12. 2/Email_Automation/lead_to_hubspot.json

**Workflow:** Lead to HubSpot

This workflow automates the process of adding new leads to HubSpot. It uses a RAG pipeline with Supabase and Anthropic to process lead information and logs the outcome.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/lead-to-hubspot`

### Workflow Steps

1.  **Webhook Trigger:** Initiated by a new lead, for example, from a form submission.
2.  **Text Splitter:** Splits the lead data into smaller text segments.
3.  **Embeddings (Cohere):** Creates vector embeddings from the text segments using the `embed-english-v3.0` model.
4.  **Supabase Insert:** Inserts the embeddings into a Supabase vector store in the `lead_to_hubspot` index.
5.  **Supabase Query:** Queries the Supabase index to retrieve contextual information.
6.  **RAG Agent (Anthropic):** Processes the lead data using the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Logs the result in a Google Sheet named "Log".
8.  **Error Handling:** Sends an alert to the `#alerts` Slack channel if the RAG agent encounters an error.

---

## 13. 2/Email_Automation/parse_invoice_emails.json

**Workflow:** Parse Invoice Emails

This workflow automates the parsing of invoice data from emails. It processes email content through a RAG pipeline using Weaviate and Anthropic, and logs the extracted data.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/parse-invoice-emails`

### Workflow Steps

1.  **Webhook Trigger:** Triggered by an incoming email containing an invoice.
2.  **Text Splitter:** Breaks down the email content into smaller chunks.
3.  **Embeddings (OpenAI):** Generates vector embeddings from the text chunks using the `text-embedding-3-small` model.
4.  **Weaviate Insert:** Stores the embeddings in a Weaviate vector store under the `parse_invoice_emails` index.
5.  **Weaviate Query:** Retrieves relevant data from the Weaviate index.
6.  **RAG Agent (Anthropic):** Extracts invoice data using the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Appends the extracted data to a Google Sheet named "Log".
8.  **Error Handling:** If the agent fails, a notification is sent to the `#alerts` Slack channel.

---

## 14. 2/Travel/airport_lounge_finder.json

**Workflow:** Airport Lounge Finder

This workflow helps users find airport lounges. It uses a RAG pipeline with Redis and Hugging Face to provide lounge information.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/airport_lounge_finder`

### Workflow Steps

1.  **Webhook:** Receives a request for lounge information.
2.  **Text Splitter:** Splits the request into smaller text chunks.
3.  **Embeddings (Cohere):** Converts the text chunks into vector embeddings.
4.  **Redis Insert:** Stores the embeddings in a Redis vector store under the `airport_lounge_finder` index.
5.  **Redis Query:** Retrieves relevant lounge information from the Redis index.
6.  **RAG Agent (Hugging Face):** Generates a response using the retrieved context and a Hugging Face chat model.
7.  **Append Sheet:** Logs the request and response in a Google Sheet named "Log".

---

## 15. 2/Travel/local_attraction_recommender.json

**Workflow:** Local Attraction Recommender

This workflow recommends local attractions to users. It leverages a RAG pipeline with Pinecone and Anthropic to generate recommendations.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/local_attraction_recommender`

### Workflow Steps

1.  **Webhook:** Receives a user request for recommendations.
2.  **Text Splitter:** Splits the user's request into smaller text chunks.
3.  **Embeddings (Cohere):** Creates vector embeddings from the text chunks.
4.  **Pinecone Insert:** Stores the embeddings in a Pinecone vector store under the `local_attraction_recommender` index.
5.  **Pinecone Query:** Retrieves attraction information from the Pinecone index.
6.  **RAG Agent (Anthropic):** Generates recommendations using the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Logs the interaction in a Google Sheet named "Log".
---

## 16. 2/Travel/travel_itinerary_builder.json

**Workflow:** Travel Itinerary Builder

This workflow helps users build a travel itinerary. It uses a RAG pipeline with Supabase and OpenAI to generate a plan.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/travel_itinerary_builder`

### Workflow Steps

1.  **Webhook:** Receives a user's request to build an itinerary.
2.  **Text Splitter:** Breaks down the request into smaller text chunks.
3.  **Embeddings (Cohere):** Converts the text chunks into vector embeddings.
4.  **Supabase Insert:** Stores the embeddings in a Supabase vector store under the `travel_itinerary_builder` index.
5.  **Supabase Query:** Retrieves relevant information from the Supabase index.
6.  **RAG Agent (OpenAI):** Generates an itinerary using the retrieved context and an OpenAI chat model.
7.  **Append Sheet:** Logs the request and the generated itinerary in a Google Sheet named "Log".

---

## 17. 2/Travel/road_trip_stop_planner.json

**Workflow:** Road Trip Stop Planner

This workflow plans stops for a road trip. It uses a RAG pipeline with Supabase and Anthropic to suggest stops along a route.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/road_trip_stop_planner`

### Workflow Steps

1.  **Webhook:** Receives a user's road trip details.
2.  **Text Splitter:** Splits the input into smaller text segments.
3.  **Embeddings (Cohere):** Creates vector embeddings from the text segments.
4.  **Supabase Insert:** Inserts the embeddings into a Supabase vector store in the `road_trip_stop_planner` index.
5.  **Supabase Query:** Queries the Supabase index to retrieve potential stops.
6.  **RAG Agent (Anthropic):** Generates a list of recommended stops using the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Logs the road trip plan in a Google Sheet named "Log".

---

## 18. 2/Travel/weather_packing_list_generator.json

**Workflow:** Weather Packing List Generator

This workflow generates a packing list based on the weather of a destination. It uses a RAG pipeline with Supabase and Anthropic to create the list.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/weather_packing_list_generator`

### Workflow Steps

1.  **Webhook:** Receives a user's travel destination and dates.
2.  **Text Splitter:** Breaks down the request into smaller chunks.
3.  **Embeddings (OpenAI):** Generates vector embeddings from the text chunks.
4.  **Supabase Insert:** Stores the embeddings in a Supabase vector store under the `weather_packing_list_generator` index.
5.  **Supabase Query:** Retrieves weather information and packing suggestions from the Supabase index.
6.  **RAG Agent (Anthropic):** Creates a packing list using the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Appends the packing list to a Google Sheet named "Log".

---

## 19. 2/Travel/flight_price_drop_alert.json

**Workflow:** Flight Price Drop Alert

This workflow alerts users when a flight price drops. It uses a RAG pipeline with Weaviate and Hugging Face to monitor and report price changes.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/flight_price_drop_alert`

### Workflow Steps

1.  **Webhook:** Receives flight information to monitor.
2.  **Text Splitter:** Splits the flight details into smaller text chunks.
3.  **Embeddings (OpenAI):** Converts the text chunks into vector embeddings.
4.  **Weaviate Insert:** Stores the embeddings in a Weaviate vector store under the `flight_price_drop_alert` index.
5.  **Weaviate Query:** Retrieves the latest price information from the Weaviate index.
6.  **RAG Agent (Hugging Face):** Determines if the price has dropped and generates an alert using a Hugging Face chat model.
7.  **Append Sheet:** Logs the alert in a Google Sheet named "Log".

---

## 20. 2/Travel/visa_requirement_checker.json

**Workflow:** Visa Requirement Checker

This workflow checks visa requirements for a given destination. It uses a RAG pipeline with Weaviate and Anthropic to provide the information.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/visa_requirement_checker`

### Workflow Steps

1.  **Webhook:** Receives a user's nationality and destination.
2.  **Text Splitter:** Splits the input into smaller text chunks.
3.  **Embeddings (Cohere):** Creates vector embeddings from the text chunks.
4.  **Weaviate Insert:** Stores the embeddings in a Weaviate vector store under the `visa_requirement_checker` index.
5.  **Weaviate Query:** Retrieves visa requirement information from the Weaviate index.
6.  **RAG Agent (Anthropic):** Provides the visa requirements using the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Logs the query and response in a Google Sheet named "Log".
---

## 21. 2/Travel/travel_advisory_monitor.json

**Workflow:** Travel Advisory Monitor

This workflow monitors travel advisories. It uses a RAG pipeline with Pinecone and Anthropic to check for updates and logs the information.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/travel_advisory_monitor`

### Workflow Steps

1.  **Webhook:** Receives a request to check for travel advisories.
2.  **Text Splitter:** Breaks down the request into smaller text chunks.
3.  **Embeddings (OpenAI):** Converts the text chunks into vector embeddings.
4.  **Pinecone Insert:** Stores the embeddings in a Pinecone vector store under the `travel_advisory_monitor` index.
5.  **Pinecone Query:** Retrieves the latest travel advisories from the Pinecone index.
6.  **RAG Agent (Anthropic):** Generates a summary of the advisories using the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Logs the advisory information in a Google Sheet named "Log".

---

## 22. 2/Travel/hotel_review_sentiment.json

**Workflow:** Hotel Review Sentiment

This workflow analyzes the sentiment of hotel reviews. It uses a RAG pipeline with Pinecone and Hugging Face to determine the sentiment and logs the result.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/hotel_review_sentiment`

### Workflow Steps

1.  **Webhook:** Receives a hotel review.
2.  **Text Splitter:** Splits the review into smaller text segments.
3.  **Embeddings (Hugging Face):** Creates vector embeddings from the text segments.
4.  **Pinecone Insert:** Inserts the embeddings into a Pinecone vector store in the `hotel_review_sentiment` index.
5.  **Pinecone Query:** Queries the Pinecone index to retrieve relevant information.
6.  **RAG Agent (Hugging Face):** Determines the sentiment of the review using the retrieved context and a Hugging Face chat model.
7.  **Append Sheet:** Logs the review and its sentiment in a Google Sheet named "Log".

---

## 23. 2/Travel/currency_exchange_estimator.json

**Workflow:** Currency Exchange Estimator

This workflow estimates currency exchange rates. It uses a RAG pipeline with Weaviate and Hugging Face to provide an estimate.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/currency_exchange_estimator`

### Workflow Steps

1.  **Webhook:** Receives a request with the currencies to be exchanged.
2.  **Text Splitter:** Breaks down the request into smaller chunks.
3.  **Embeddings (Hugging Face):** Generates vector embeddings from the text chunks.
4.  **Weaviate Insert:** Stores the embeddings in a Weaviate vector store under the `currency_exchange_estimator` index.
5.  **Weaviate Query:** Retrieves exchange rate information from the Weaviate index.
6.  **RAG Agent (Hugging Face):** Calculates and returns the estimated exchange amount using a Hugging Face chat model.
7.  **Append Sheet:** Appends the transaction details to a Google Sheet named "Log".

---

## 24. 2/Finance_Accounting/transaction_logs_backup.json

**Workflow:** Transaction Logs Backup

This workflow backs up transaction logs. It uses a RAG pipeline with Supabase and OpenAI to process and store the logs.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/transaction-logs-backup`

### Workflow Steps

1.  **Webhook Trigger:** Receives transaction data to be backed up.
2.  **Text Splitter:** Splits the transaction data into smaller text chunks.
3.  **Embeddings (Cohere):** Converts the text chunks into vector embeddings.
4.  **Supabase Insert:** Stores the embeddings in a Supabase vector store under the `transaction_logs_backup` index.
5.  **Supabase Query:** Retrieves any necessary context from the Supabase index.
6.  **RAG Agent (OpenAI):** Processes the transaction log data using an OpenAI chat model.
7.  **Append Sheet:** Logs the backup status in a Google Sheet named "Log".
8.  **Error Handling:** Sends an alert to the `#alerts` Slack channel if the RAG agent fails.

---

## 25. 2/Finance_Accounting/unpaid_invoice_reminder.json

**Workflow:** Unpaid Invoice Reminder

This workflow sends reminders for unpaid invoices. It uses a RAG pipeline with Weaviate and OpenAI to generate and send the reminders.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/unpaid-invoice-reminder`

### Workflow Steps

1.  **Webhook Trigger:** Initiated by a schedule or a manual trigger to check for unpaid invoices.
2.  **Text Splitter:** Processes data related to unpaid invoices.
3.  **Embeddings (Cohere):** Creates vector embeddings from the data.
4.  **Weaviate Insert:** Stores the embeddings in a Weaviate vector store under the `unpaid_invoice_reminder` index.
5.  **Weaviate Query:** Retrieves information about which invoices are unpaid.
6.  **RAG Agent (OpenAI):** Generates a reminder message using the retrieved context and an OpenAI chat model.
7.  **Append Sheet:** Logs the reminder action in a Google Sheet named "Log".
8.  **Error Handling:** Notifies the `#alerts` Slack channel if the RAG agent fails.
---

## 26. 2/Finance_Accounting/stripe_to_quickbooks.json

**Workflow:** Stripe to QuickBooks

This workflow automates the process of syncing Stripe transactions to QuickBooks. It uses a RAG pipeline with Supabase and OpenAI to handle the data transfer.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/stripe-to-quickbooks`

### Workflow Steps

1.  **Webhook Trigger:** Receives transaction data from Stripe.
2.  **Text Splitter:** Breaks down the transaction data into smaller text chunks.
3.  **Embeddings (OpenAI):** Converts the text chunks into vector embeddings using the `text-embedding-3-small` model.
4.  **Supabase Insert:** Stores the embeddings in a Supabase vector store under the `stripe_to_quickbooks` index.
5.  **Supabase Query:** Retrieves relevant data from the Supabase index for context.
6.  **RAG Agent (OpenAI):** Processes the transaction data and prepares it for QuickBooks using an OpenAI chat model.
7.  **Append Sheet:** Appends the status of the sync to a Google Sheet named "Log".
8.  **Error Handling:** Sends an alert to the `#alerts` Slack channel if the RAG agent fails.

---

## 27. 2/Finance_Accounting/currency_rate_monitor.json

**Workflow:** Currency Rate Monitor

This workflow monitors currency exchange rates. It uses a RAG pipeline with Weaviate and OpenAI to fetch and log the latest rates.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/currency-rate-monitor`

### Workflow Steps

1.  **Webhook Trigger:** Initiated by a schedule or a manual trigger to check currency rates.
2.  **Text Splitter:** Processes the request.
3.  **Embeddings (OpenAI):** Creates vector embeddings from the text.
4.  **Weaviate Insert:** Inserts the embeddings into a Weaviate vector store in the `currency_rate_monitor` index.
5.  **Weaviate Query:** Queries the Weaviate index to retrieve the latest currency rates.
6.  **RAG Agent (OpenAI):** Processes the rate information using an OpenAI chat model.
7.  **Append Sheet:** Logs the rates in a Google Sheet named "Log".
8.  **Error Handling:** Sends an alert to the `#alerts` Slack channel if the RAG agent encounters an error.

---

## 28. 2/Finance_Accounting/monthly_expense_report.json

**Workflow:** Monthly Expense Report

This workflow generates a monthly expense report. It processes expense data through a RAG pipeline using Weaviate and Anthropic.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/monthly-expense-report`

### Workflow Steps

1.  **Webhook Trigger:** Triggered on a monthly schedule.
2.  **Text Splitter:** Breaks down the expense data into smaller chunks.
3.  **Embeddings (OpenAI):** Generates vector embeddings from the text chunks using the `text-embedding-3-small` model.
4.  **Weaviate Insert:** Stores the embeddings in a Weaviate vector store under the `monthly_expense_report` index.
5.  **Weaviate Query:** Retrieves relevant data from the Weaviate index.
6.  **RAG Agent (Anthropic):** Generates the expense report using the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Appends the report to a Google Sheet named "Log".
8.  **Error Handling:** If the agent fails, a notification is sent to the `#alerts` Slack channel.

---

## 29. 2/Finance_Accounting/ocr_receipts_to_notion.json

**Workflow:** OCR Receipts to Notion

This workflow uses OCR to extract data from receipts and saves it to Notion. It uses a RAG pipeline with Supabase and Anthropic to process the extracted text.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/ocr-receipts-to-notion`

### Workflow Steps

1.  **Webhook Trigger:** Receives an image of a receipt.
2.  **Text Splitter:** (Assumes OCR is handled before this workflow) Splits the extracted text from the receipt into smaller chunks.
3.  **Embeddings (OpenAI):** Converts the text chunks into vector embeddings.
4.  **Supabase Insert:** Stores the embeddings in a Supabase vector store under the `ocr_receipts_to_notion` index.
5.  **Supabase Query:** Retrieves context for parsing the receipt data.
6.  **RAG Agent (Anthropic):** Extracts structured data from the receipt text using an Anthropic chat model.
7.  **Append Sheet:** Logs the extracted data in a Google Sheet named "Log" (and would typically also save to Notion).
8.  **Error Handling:** Sends an error message to the `#alerts` Slack channel upon failure.

---

## 30. 2/Finance_Accounting/weekly_shopify_sales_summary.json

**Workflow:** Weekly Shopify Sales Summary

This workflow generates a weekly summary of Shopify sales. It uses a RAG pipeline with Pinecone and Anthropic to create the summary.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/weekly-shopify-sales-summary`

### Workflow Steps

1.  **Webhook Trigger:** Initiated on a weekly schedule.
2.  **Text Splitter:** Processes the weekly sales data from Shopify.
3.  **Embeddings (Cohere):** Creates vector embeddings from the sales data.
4.  **Pinecone Insert:** Stores the embeddings in a Pinecone vector store in the `weekly_shopify_sales_summary` index.
5.  **Pinecone Query:** Retrieves the sales data to be summarized.
6.  **RAG Agent (Anthropic):** Generates the sales summary using the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Records the summary in a Google Sheet named "Log".
8.  **Error Handling:** Notifies the `#alerts` Slack channel if the RAG agent fails.
---

## 31. 2/Finance_Accounting/paypal_to_airtable.json

**Workflow:** PayPal to Airtable

This workflow automates the process of syncing PayPal transactions to Airtable. It uses a RAG pipeline with Weaviate and OpenAI to handle the data transfer.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/paypal-to-airtable`

### Workflow Steps

1.  **Webhook Trigger:** Receives transaction data from PayPal.
2.  **Text Splitter:** Breaks down the transaction data into smaller text chunks.
3.  **Embeddings (OpenAI):** Converts the text chunks into vector embeddings using the `text-embedding-3-small` model.
4.  **Weaviate Insert:** Stores the embeddings in a Weaviate vector store under the `paypal_to_airtable` index.
5.  **Weaviate Query:** Retrieves relevant data from the Weaviate index for context.
6.  **RAG Agent (OpenAI):** Processes the transaction data and prepares it for Airtable using an OpenAI chat model.
7.  **Append Sheet:** Appends the status of the sync to a Google Sheet named "Log".
8.  **Error Handling:** Sends an alert to the `#alerts` Slack channel if the RAG agent fails.

---

## 32. 2/HR/notion_job_board_poster.json

**Workflow:** Notion Job Board Poster

This workflow automates posting jobs to a Notion job board. It uses a RAG pipeline with Supabase and OpenAI to process and post job details.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/notion-job-board-poster`

### Workflow Steps

1.  **Webhook Trigger:** Initiated by a new job opening.
2.  **Text Splitter:** Splits the job description into smaller text segments.
3.  **Embeddings (OpenAI):** Creates vector embeddings from the text segments using the `text-embedding-3-small` model.
4.  **Supabase Insert:** Inserts the embeddings into a Supabase vector store in the `notion_job_board_poster` index.
5.  **Supabase Query:** Queries the Supabase index to retrieve any relevant context.
6.  **RAG Agent (OpenAI):** Processes the job details using an OpenAI chat model.
7.  **Append Sheet:** Logs the posting action in a Google Sheet named "Log".
8.  **Error Handling:** Sends an alert to the `#alerts` Slack channel if the RAG agent encounters an error.

---

## 33. 2/HR/new_job_application_parser.json

**Workflow:** New Job Application Parser

This workflow automates the parsing of new job applications. It processes application data through a RAG pipeline using Pinecone and OpenAI.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/new-job-application-parser`

### Workflow Steps

1.  **Webhook Trigger:** Triggered by a new job application submission.
2.  **Text Splitter:** Breaks down the application text into smaller chunks.
3.  **Embeddings (OpenAI):** Generates vector embeddings from the text chunks using the `text-embedding-3-small` model.
4.  **Pinecone Insert:** Stores the embeddings in a Pinecone vector store under the `new_job_application_parser` index.
5.  **Pinecone Query:** Retrieves relevant data from the Pinecone index.
6.  **RAG Agent (OpenAI):** Extracts key information from the application using an OpenAI chat model.
7.  **Append Sheet:** Appends the extracted data to a Google Sheet named "Log".
8.  **Error Handling:** If the agent fails, a notification is sent to the `#alerts` Slack channel.

---

## 34. 2/Manufacturing/shift_handover_summary.json

**Workflow:** Shift Handover Summary

This workflow creates a summary of a shift handover. It uses a RAG pipeline with Supabase and Hugging Face to generate the summary.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/shift_handover_summary`

### Workflow Steps

1.  **Webhook:** Receives data from a shift handover form or log.
2.  **Text Splitter:** Splits the handover notes into smaller text chunks.
3.  **Embeddings (Hugging Face):** Converts the text chunks into vector embeddings.
4.  **Supabase Insert:** Stores the embeddings in a Supabase vector store under the `shift_handover_summary` index.
5.  **Supabase Query:** Retrieves information from the Supabase index.
6.  **RAG Agent (Hugging Face):** Generates a summary of the handover using a Hugging Face chat model.
7.  **Append Sheet:** Logs the summary in a Google Sheet named "Log".

---

## 35. 2/Manufacturing/quality_defect_classifier.json

**Workflow:** Quality Defect Classifier

This workflow classifies quality defects in a manufacturing process. It leverages a RAG pipeline with Redis and Anthropic to perform the classification.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/quality_defect_classifier`

### Workflow Steps

1.  **Webhook:** Receives a report of a quality defect.
2.  **Text Splitter:** Splits the defect description into smaller text chunks.
3.  **Embeddings (OpenAI):** Creates vector embeddings from the text chunks.
4.  **Redis Insert:** Stores the embeddings in a Redis vector store under the `quality_defect_classifier` index.
5.  **Redis Query:** Retrieves information about known defects from the Redis index.
6.  **RAG Agent (Anthropic):** Classifies the defect using the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Logs the defect and its classification in a Google Sheet named "Log".
---

## 36. 2/Manufacturing/safety_incident_alert.json

**Workflow:** Safety Incident Alert

This workflow sends alerts for safety incidents. It uses a RAG pipeline with Redis and Hugging Face to process incident reports and logs the alerts.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/safety_incident_alert`

### Workflow Steps

1.  **Webhook:** Receives a safety incident report.
2.  **Text Splitter:** Breaks down the incident report into smaller text chunks.
3.  **Embeddings (Hugging Face):** Converts the text chunks into vector embeddings.
4.  **Redis Insert:** Stores the embeddings in a Redis vector store under the `safety_incident_alert` index.
5.  **Redis Query:** Retrieves relevant information from the Redis index.
6.  **RAG Agent (Hugging Face):** Generates an alert using the retrieved context and a Hugging Face chat model.
7.  **Append Sheet:** Logs the incident and alert in a Google Sheet named "Log".

---

## 37. 2/Manufacturing/production_kpi_dashboard.json

**Workflow:** Production KPI Dashboard

This workflow updates a production KPI dashboard. It uses a RAG pipeline with Weaviate and OpenAI to process production data.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/production_kpi_dashboard`

### Workflow Steps

1.  **Webhook:** Receives production data.
2.  **Text Splitter:** Splits the data into smaller text segments.
3.  **Embeddings (Cohere):** Creates vector embeddings from the text segments.
4.  **Weaviate Insert:** Inserts the embeddings into a Weaviate vector store in the `production_kpi_dashboard` index.
5.  **Weaviate Query:** Queries the Weaviate index to retrieve KPI data.
6.  **RAG Agent (OpenAI):** Processes the data for the dashboard using an OpenAI chat model.
7.  **Append Sheet:** Logs the update in a Google Sheet named "Log".

---

## 38. 2/Manufacturing/inventory_restock_forecast.json

**Workflow:** Inventory Restock Forecast

This workflow forecasts inventory restock needs. It uses a RAG pipeline with Supabase and Anthropic to generate the forecast.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/inventory_restock_forecast`

### Workflow Steps

1.  **Webhook:** Receives current inventory levels and sales data.
2.  **Text Splitter:** Breaks down the data into smaller chunks.
3.  **Embeddings (Cohere):** Generates vector embeddings from the text chunks.
4.  **Supabase Insert:** Stores the embeddings in a Supabase vector store under the `inventory_restock_forecast` index.
5.  **Supabase Query:** Retrieves historical data and trends from the Supabase index.
6.  **RAG Agent (Anthropic):** Generates a restock forecast using the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Appends the forecast to a Google Sheet named "Log".

---

## 39. 2/Manufacturing/maintenance_ticket_router.json

**Workflow:** Maintenance Ticket Router

This workflow routes maintenance tickets to the appropriate team. It uses a RAG pipeline with Supabase and Hugging Face to determine the correct routing.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/maintenance_ticket_router`

### Workflow Steps

1.  **Webhook:** Receives a new maintenance ticket.
2.  **Text Splitter:** Splits the ticket description into smaller text chunks.
3.  **Embeddings (Cohere):** Converts the text chunks into vector embeddings.
4.  **Supabase Insert:** Stores the embeddings in a Supabase vector store under the `maintenance_ticket_router` index.
5.  **Supabase Query:** Retrieves information about team responsibilities from the Supabase index.
6.  **RAG Agent (Hugging Face):** Determines the correct team for the ticket using a Hugging Face chat model.
7.  **Append Sheet:** Logs the routing decision in a Google Sheet named "Log".

---

## 40. 2/Manufacturing/machine_downtime_predictor.json

**Workflow:** Machine Downtime Predictor

This workflow predicts machine downtime. It leverages a RAG pipeline with Weaviate and Anthropic to make predictions based on machine data.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/machine_downtime_predictor`

### Workflow Steps

1.  **Webhook:** Receives sensor data or other machine metrics.
2.  **Text Splitter:** Splits the data into smaller text chunks.
3.  **Embeddings (OpenAI):** Creates vector embeddings from the text chunks.
4.  **Weaviate Insert:** Stores the embeddings in a Weaviate vector store under the `machine_downtime_predictor` index.
5.  **Weaviate Query:** Retrieves historical data from the Weaviate index.
6.  **RAG Agent (Anthropic):** Predicts potential downtime using the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Logs the prediction in a Google Sheet named "Log".
---

## 41. 2/Manufacturing/packaging_waste_calculator.json

**Workflow:** Packaging Waste Calculator

This workflow calculates packaging waste. It uses a RAG pipeline with Redis and Anthropic to process data and calculate waste.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/packaging_waste_calculator`

### Workflow Steps

1.  **Webhook:** Receives data about packaging materials and usage.
2.  **Text Splitter:** Breaks down the data into smaller text chunks.
3.  **Embeddings (OpenAI):** Converts the text chunks into vector embeddings.
4.  **Redis Insert:** Stores the embeddings in a Redis vector store under the `packaging_waste_calculator` index.
5.  **Redis Query:** Retrieves relevant information from the Redis index.
6.  **RAG Agent (Anthropic):** Calculates the packaging waste using the retrieved context and an Anthropic chat model.
7.  **Append Sheet:** Logs the results in a Google Sheet named "Log".

---

## 42. 2/Manufacturing/supply_chain_delay_monitor.json

**Workflow:** Supply Chain Delay Monitor

This workflow monitors for delays in the supply chain. It uses a RAG pipeline with Supabase and OpenAI to process and report on delays.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/supply_chain_delay_monitor`

### Workflow Steps

1.  **Webhook:** Receives data about shipments and logistics.
2.  **Text Splitter:** Splits the data into smaller text segments.
3.  **Embeddings (Cohere):** Creates vector embeddings from the text segments.
4.  **Supabase Insert:** Inserts the embeddings into a Supabase vector store in the `supply_chain_delay_monitor` index.
5.  **Supabase Query:** Queries the Supabase index to identify potential delays.
6.  **RAG Agent (OpenAI):** Generates a report on any identified delays using an OpenAI chat model.
7.  **Append Sheet:** Logs the report in a Google Sheet named "Log".

---

## 43. 2/Manufacturing/mes_log_analyzer.json

**Workflow:** MES Log Analyzer

This workflow analyzes logs from a Manufacturing Execution System (MES). It uses a RAG pipeline with Weaviate and OpenAI to extract insights from the logs.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/mes_log_analyzer`

### Workflow Steps

1.  **Webhook:** Receives MES log data.
2.  **Text Splitter:** Breaks down the log data into smaller chunks.
3.  **Embeddings (Hugging Face):** Generates vector embeddings from the text chunks.
4.  **Weaviate Insert:** Stores the embeddings in a Weaviate vector store under the `mes_log_analyzer` index.
5.  **Weaviate Query:** Retrieves relevant information from the Weaviate index.
6.  **RAG Agent (OpenAI):** Analyzes the logs and generates insights using an OpenAI chat model.
7.  **Append Sheet:** Appends the analysis to a Google Sheet named "Log".

---

## 44. 2/IoT/mqtt_topic_monitor.json

**Workflow:** MQTT Topic Monitor

This workflow monitors messages on an MQTT topic. It uses a RAG pipeline with Redis and Hugging Face to process the messages.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/mqtt_topic_monitor`

### Workflow Steps

1.  **Webhook:** Receives a message from an MQTT topic.
2.  **Text Splitter:** Splits the message content into smaller text chunks.
3.  **Embeddings (OpenAI):** Converts the text chunks into vector embeddings.
4.  **Redis Insert:** Stores the embeddings in a Redis vector store under the `mqtt_topic_monitor` index.
5.  **Redis Query:** Retrieves relevant information from the Redis index.
6.  **RAG Agent (Hugging Face):** Processes the message using a Hugging Face chat model.
7.  **Append Sheet:** Logs the message and any actions taken in a Google Sheet named "Log".

---

## 45. 2/IoT/predictive_maintenance_alert.json

**Workflow:** Predictive Maintenance Alert

This workflow sends alerts for predictive maintenance. It leverages a RAG pipeline with Weaviate and OpenAI to analyze sensor data and predict maintenance needs.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/predictive_maintenance_alert`

### Workflow Steps

1.  **Webhook:** Receives sensor data from IoT devices.
2.  **Text Splitter:** Splits the data into smaller text chunks.
3.  **Embeddings (OpenAI):** Creates vector embeddings from the text chunks.
4.  **Weaviate Insert:** Stores the embeddings in a Weaviate vector store under the `predictive_maintenance_alert` index.
5.  **Weaviate Query:** Retrieves historical data from the Weaviate index.
6.  **RAG Agent (OpenAI):** Predicts maintenance needs using the retrieved context and an OpenAI chat model.
7.  **Append Sheet:** Logs the prediction and any alerts in a Google Sheet named "Log".
---

## 46. 2/IoT/industrial_iot_kpi_email.json

**Workflow:** Industrial IoT KPI Email

This workflow sends an email with Industrial IoT (IIoT) Key Performance Indicators (KPIs). It uses a RAG pipeline with Redis and OpenAI to generate the email content.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/industrial_iot_kpi_email`

### Workflow Steps

1.  **Webhook:** Receives IIoT data.
2.  **Text Splitter:** Breaks down the data into smaller text chunks.
3.  **Embeddings (Cohere):** Converts the text chunks into vector embeddings.
4.  **Redis Insert:** Stores the embeddings in a Redis vector store under the `industrial_iot_kpi_email` index.
5.  **Redis Query:** Retrieves relevant KPI data from the Redis index.
6.  **RAG Agent (OpenAI):** Generates the KPI email using the retrieved context and an OpenAI chat model.
7.  **Append Sheet:** Logs the email sending event in a Google Sheet named "Log".

---

## 47. 2/IoT/ble_beacon_mapper.json

**Workflow:** BLE Beacon Mapper

This workflow maps Bluetooth Low Energy (BLE) beacons. It uses a RAG pipeline with Pinecone and OpenAI to process beacon data.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/ble_beacon_mapper`

### Workflow Steps

1.  **Webhook:** Receives data from BLE beacons.
2.  **Text Splitter:** Splits the beacon data into smaller text segments.
3.  **Embeddings (Hugging Face):** Creates vector embeddings from the text segments.
4.  **Pinecone Insert:** Inserts the embeddings into a Pinecone vector store in the `ble_beacon_mapper` index.
5.  **Pinecone Query:** Queries the Pinecone index to retrieve location or other contextual data.
6.  **RAG Agent (OpenAI):** Maps the beacon's location or status using an OpenAI chat model.
7.  **Append Sheet:** Logs the mapping data in a Google Sheet named "Log".

---

## 48. 2/IoT/edge_device_log_compressor.json

**Workflow:** Edge Device Log Compressor

This workflow compresses logs from edge devices. It uses a RAG pipeline with Redis and Anthropic to summarize the logs.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/edge_device_log_compressor`

### Workflow Steps

1.  **Webhook:** Receives log data from an edge device.
2.  **Text Splitter:** Breaks down the log data into smaller chunks.
3.  **Embeddings (Cohere):** Generates vector embeddings from the text chunks.
4.  **Redis Insert:** Stores the embeddings in a Redis vector store under the `edge_device_log_compressor` index.
5.  **Redis Query:** Retrieves relevant information from the Redis index.
6.  **RAG Agent (Anthropic):** Compresses or summarizes the logs using an Anthropic chat model.
7.  **Append Sheet:** Appends the compressed log to a Google Sheet named "Log".

---

## 49. 2/IoT/environmental_data_dashboard.json

**Workflow:** Environmental Data Dashboard

This workflow updates an environmental data dashboard. It uses a RAG pipeline with Weaviate and OpenAI to process and display data.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/environmental_data_dashboard`

### Workflow Steps

1.  **Webhook:** Receives environmental sensor data.
2.  **Text Splitter:** Splits the data into smaller text chunks.
3.  **Embeddings (OpenAI):** Converts the text chunks into vector embeddings.
4.  **Weaviate Insert:** Stores the embeddings in a Weaviate vector store under the `environmental_data_dashboard` index.
5.  **Weaviate Query:** Retrieves data for the dashboard from the Weaviate index.
6.  **RAG Agent (OpenAI):** Processes the data for visualization using an OpenAI chat model.
7.  **Append Sheet:** Logs the update in a Google Sheet named "Log".

---

## 50. 2/IoT/iot_device_firmware_update_planner.json

**Workflow:** IoT Device Firmware Update Planner

This workflow plans firmware updates for IoT devices. It leverages a RAG pipeline with Pinecone and OpenAI to create an update plan.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/iot_device_firmware_update_planner`

### Workflow Steps

1.  **Webhook:** Receives information about devices and new firmware.
2.  **Text Splitter:** Splits the information into smaller text chunks.
3.  **Embeddings (Hugging Face):** Creates vector embeddings from the text chunks.
4.  **Pinecone Insert:** Stores the embeddings in a Pinecone vector store under the `iot_device_firmware_update_planner` index.
5.  **Pinecone Query:** Retrieves device information and constraints from the Pinecone index.
6.  **RAG Agent (OpenAI):** Creates a firmware update plan using an OpenAI chat model.
7.  **Append Sheet:** Logs the plan in a Google Sheet named "Log".
---

## 51. 2/IoT/vehicle_telematics_analyzer.json

**Workflow:** Vehicle Telematics Analyzer

This workflow analyzes vehicle telematics data. It uses a RAG pipeline with Redis and Hugging Face to process the data and generate insights.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/vehicle_telematics_analyzer`

### Workflow Steps

1.  **Webhook:** Receives telematics data from a vehicle.
2.  **Text Splitter:** Breaks down the data into smaller text chunks.
3.  **Embeddings (OpenAI):** Converts the text chunks into vector embeddings.
4.  **Redis Insert:** Stores the embeddings in a Redis vector store under the `vehicle_telematics_analyzer` index.
5.  **Redis Query:** Retrieves relevant information from the Redis index.
6.  **RAG Agent (Hugging Face):** Analyzes the telematics data using a Hugging Face chat model.
7.  **Append Sheet:** Logs the analysis in a Google Sheet named "Log".

---

## 52. 2/IoT/sensor_fault_detector.json

**Workflow:** Sensor Fault Detector

This workflow detects faults in sensors. It uses a RAG pipeline with Supabase and Hugging Face to identify potential faults.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/sensor_fault_detector`

### Workflow Steps

1.  **Webhook:** Receives sensor data.
2.  **Text Splitter:** Splits the sensor data into smaller text segments.
3.  **Embeddings (OpenAI):** Creates vector embeddings from the text segments.
4.  **Supabase Insert:** Inserts the embeddings into a Supabase vector store in the `sensor_fault_detector` index.
5.  **Supabase Query:** Queries the Supabase index to retrieve baseline or historical data.
6.  **RAG Agent (Hugging Face):** Detects faults by comparing current data to historical data using a Hugging Face chat model.
7.  **Append Sheet:** Logs any detected faults in a Google Sheet named "Log".

---

## 53. 2/IoT/smart_home_energy_saver.json

**Workflow:** Smart Home Energy Saver

This workflow helps save energy in a smart home. It uses a RAG pipeline with Supabase and Hugging Face to make energy-saving recommendations.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/smart_home_energy_saver`

### Workflow Steps

1.  **Webhook:** Receives data about energy consumption and device status.
2.  **Text Splitter:** Breaks down the data into smaller chunks.
3.  **Embeddings (Cohere):** Generates vector embeddings from the text chunks.
4.  **Supabase Insert:** Stores the embeddings in a Supabase vector store under the `smart_home_energy_saver` index.
5.  **Supabase Query:** Retrieves energy usage patterns and other relevant data from the Supabase index.
6.  **RAG Agent (Hugging Face):** Generates energy-saving recommendations using a Hugging Face chat model.
7.  **Append Sheet:** Appends the recommendations to a Google Sheet named "Log".

---

## 54. 2/Automotive/autonomous_vehicle_log_summarizer.json

**Workflow:** Autonomous Vehicle Log Summarizer

This workflow summarizes logs from autonomous vehicles. It uses a RAG pipeline with Weaviate and OpenAI to generate the summaries.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/autonomous_vehicle_log_summarizer`

### Workflow Steps

1.  **Webhook:** Receives log data from an autonomous vehicle.
2.  **Text Splitter:** Splits the log data into smaller text chunks.
3.  **Embeddings (Hugging Face):** Converts the text chunks into vector embeddings.
4.  **Weaviate Insert:** Stores the embeddings in a Weaviate vector store under the `autonomous_vehicle_log_summarizer` index.
5.  **Weaviate Query:** Retrieves relevant information from the Weaviate index.
6.  **RAG Agent (OpenAI):** Summarizes the logs using an OpenAI chat model.
7.  **Append Sheet:** Logs the summary in a Google Sheet named "Log".

---

## 55. 2/Automotive/connected_car_alert.json

**Workflow:** Connected Car Alert

This workflow sends alerts from a connected car. It leverages a RAG pipeline with Redis and OpenAI to process and send alerts.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/connected_car_alert`

### Workflow Steps

1.  **Webhook:** Receives an alert or event from a connected car.
2.  **Text Splitter:** Splits the alert data into smaller text chunks.
3.  **Embeddings (OpenAI):** Creates vector embeddings from the text chunks.
4.  **Redis Insert:** Stores the embeddings in a Redis vector store under the `connected_car_alert` index.
5.  **Redis Query:** Retrieves contextual information from the Redis index.
6.  **RAG Agent (OpenAI):** Processes the alert and generates a notification using an OpenAI chat model.
7.  **Append Sheet:** Logs the alert in a Google Sheet named "Log".
---

## 56. 2/Automotive/dealer_lead_qualifier.json

**Workflow:** Dealer Lead Qualifier

This workflow qualifies leads for a car dealership. It uses a RAG pipeline with Pinecone and Hugging Face to process lead information.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/dealer_lead_qualifier`

### Workflow Steps

1.  **Webhook:** Receives lead information from a form or other source.
2.  **Text Splitter:** Breaks down the lead data into smaller text chunks.
3.  **Embeddings (Cohere):** Converts the text chunks into vector embeddings.
4.  **Pinecone Insert:** Stores the embeddings in a Pinecone vector store under the `dealer_lead_qualifier` index.
5.  **Pinecone Query:** Retrieves relevant information from the Pinecone index.
6.  **RAG Agent (Hugging Face):** Qualifies the lead using a Hugging Face chat model.
7.  **Append Sheet:** Logs the lead and qualification status in a Google Sheet named "Log".

---

## 57. 2/Automotive/adas_event_annotator.json

**Workflow:** ADAS Event Annotator

This workflow annotates events from an Advanced Driver-Assistance System (ADAS). It uses a RAG pipeline with Supabase and OpenAI to process and annotate the events.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/adas_event_annotator`

### Workflow Steps

1.  **Webhook:** Receives ADAS event data.
2.  **Text Splitter:** Splits the event data into smaller text segments.
3.  **Embeddings (Cohere):** Creates vector embeddings from the text segments.
4.  **Supabase Insert:** Inserts the embeddings into a Supabase vector store in the `adas_event_annotator` index.
5.  **Supabase Query:** Queries the Supabase index to retrieve contextual information.
6.  **RAG Agent (OpenAI):** Annotates the event using an OpenAI chat model.
7.  **Append Sheet:** Logs the annotated event in a Google Sheet named "Log".

---

## 58. 2/Automotive/ev_battery_degradation_report.json

**Workflow:** EV Battery Degradation Report

This workflow generates a report on the degradation of an electric vehicle's battery. It uses a RAG pipeline with Redis and OpenAI to create the report.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/ev_battery_degradation_report`

### Workflow Steps

1.  **Webhook:** Receives battery data from an EV.
2.  **Text Splitter:** Breaks down the data into smaller chunks.
3.  **Embeddings (Cohere):** Generates vector embeddings from the text chunks.
4.  **Redis Insert:** Stores the embeddings in a Redis vector store under the `ev_battery_degradation_report` index.
5.  **Redis Query:** Retrieves historical battery data from the Redis index.
6.  **RAG Agent (OpenAI):** Generates a degradation report using an OpenAI chat model.
7.  **Append Sheet:** Appends the report to a Google Sheet named "Log".

---

## 59. 2/Automotive/fleet_fuel_efficiency_report.json

**Workflow:** Fleet Fuel Efficiency Report

This workflow generates a fuel efficiency report for a fleet of vehicles. It uses a RAG pipeline with Weaviate and Anthropic to analyze the data.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/fleet_fuel_efficiency_report`

### Workflow Steps

1.  **Webhook:** Receives fuel consumption and mileage data for the fleet.
2.  **Text Splitter:** Splits the data into smaller text chunks.
3.  **Embeddings (Hugging Face):** Converts the text chunks into vector embeddings.
4.  **Weaviate Insert:** Stores the embeddings in a Weaviate vector store under the `fleet_fuel_efficiency_report` index.
5.  **Weaviate Query:** Retrieves relevant data from the Weaviate index.
6.  **RAG Agent (Anthropic):** Generates a fuel efficiency report using an Anthropic chat model.
7.  **Append Sheet:** Logs the report in a Google Sheet named "Log".

---

## 60. 2/Automotive/car_insurance_quote_generator.json

**Workflow:** Car Insurance Quote Generator

This workflow generates car insurance quotes. It leverages a RAG pipeline with Pinecone and Anthropic to calculate and provide quotes.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/car_insurance_quote_generator`

### Workflow Steps

1.  **Webhook:** Receives user information for a quote.
2.  **Text Splitter:** Splits the user data into smaller text chunks.
3.  **Embeddings (Hugging Face):** Creates vector embeddings from the text chunks.
4.  **Pinecone Insert:** Stores the embeddings in a Pinecone vector store under the `car_insurance_quote_generator` index.
5.  **Pinecone Query:** Retrieves rating information from the Pinecone index.
6.  **RAG Agent (Anthropic):** Generates an insurance quote using an Anthropic chat model.
7.  **Append Sheet:** Logs the quote details in a Google Sheet named "Log".
---

## 61. 2/Automotive/recall_notice_tracker.json

**Workflow:** Recall Notice Tracker

This workflow tracks vehicle recall notices. It uses a RAG pipeline with Pinecone and Anthropic to process and monitor recall information.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/recall_notice_tracker`

### Workflow Steps

1.  **Webhook:** Receives information about a potential recall.
2.  **Text Splitter:** Breaks down the information into smaller text chunks.
3.  **Embeddings (OpenAI):** Converts the text chunks into vector embeddings.
4.  **Pinecone Insert:** Stores the embeddings in a Pinecone vector store under the `recall_notice_tracker` index.
5.  **Pinecone Query:** Retrieves relevant recall information from the Pinecone index.
6.  **RAG Agent (Anthropic):** Processes the information and determines if a new recall has been issued using an Anthropic chat model.
7.  **Append Sheet:** Logs the findings in a Google Sheet named "Log".

---

## 62. 2/Automotive/vin_decoder.json

**Workflow:** VIN Decoder

This workflow decodes Vehicle Identification Numbers (VINs). It uses a RAG pipeline with Redis and Hugging Face to provide vehicle information.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/vin_decoder`

### Workflow Steps

1.  **Webhook:** Receives a VIN to be decoded.
2.  **Text Splitter:** Splits the VIN or related data into smaller text segments.
3.  **Embeddings (Hugging Face):** Creates vector embeddings from the text segments.
4.  **Redis Insert:** Inserts the embeddings into a Redis vector store in the `vin_decoder` index.
5.  **Redis Query:** Queries the Redis index to retrieve vehicle specifications.
6.  **RAG Agent (Hugging Face):** Decodes the VIN and provides vehicle details using a Hugging Face chat model.
7.  **Append Sheet:** Logs the decoded information in a Google Sheet named "Log".

---

## 63. 2/Automotive/ride-share_surge_predictor.json

**Workflow:** Ride-Share Surge Predictor

This workflow predicts surge pricing for ride-sharing services. It uses a RAG pipeline with Supabase and Anthropic to make predictions.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/ride-share_surge_predictor`

### Workflow Steps

1.  **Webhook:** Receives location and time data.
2.  **Text Splitter:** Breaks down the data into smaller chunks.
3.  **Embeddings (Cohere):** Generates vector embeddings from the text chunks.
4.  **Supabase Insert:** Stores the embeddings in a Supabase vector store under the `ride-share_surge_predictor` index.
5.  **Supabase Query:** Retrieves historical surge data from the Supabase index.
6.  **RAG Agent (Anthropic):** Predicts surge pricing using an Anthropic chat model.
7.  **Append Sheet:** Appends the prediction to a Google Sheet named "Log".

---

## 64. 2/Agriculture/weather_impact_report.json

**Workflow:** Weather Impact Report

This workflow generates a report on the impact of weather on agriculture. It uses a RAG pipeline with Supabase and Anthropic to analyze weather data.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/weather_impact_report`

### Workflow Steps

1.  **Webhook:** Receives weather data and crop information.
2.  **Text Splitter:** Splits the data into smaller text chunks.
3.  **Embeddings (Hugging Face):** Converts the text chunks into vector embeddings.
4.  **Supabase Insert:** Stores the embeddings in a Supabase vector store under the `weather_impact_report` index.
5.  **Supabase Query:** Retrieves relevant agricultural data from the Supabase index.
6.  **RAG Agent (Anthropic):** Generates a weather impact report using an Anthropic chat model.
7.  **Append Sheet:** Logs the report in a Google Sheet named "Log".

---

## 65. 2/Agriculture/crop_yield_predictor.json

**Workflow:** Crop Yield Predictor

This workflow predicts crop yields. It leverages a RAG pipeline with Supabase and OpenAI to make predictions based on various factors.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/crop_yield_predictor`

### Workflow Steps

1.  **Webhook:** Receives data on weather, soil, and other agricultural inputs.
2.  **Text Splitter:** Splits the data into smaller text chunks.
3.  **Embeddings (Hugging Face):** Creates vector embeddings from the text chunks.
4.  **Supabase Insert:** Stores the embeddings in a Supabase vector store under the `crop_yield_predictor` index.
5.  **Supabase Query:** Retrieves historical yield data from the Supabase index.
6.  **RAG Agent (OpenAI):** Predicts the crop yield using an OpenAI chat model.
7.  **Append Sheet:** Logs the prediction in a Google Sheet named "Log".
---

## 66. 1/AI_Research_RAG_and_Data_Analysis/🔍 Perplexity Research to HTML_ AI-Powered Content Creation.txt

**Workflow:** 🔍 Perplexity Research to HTML: AI-Powered Content Creation

This workflow automates the creation of HTML articles from research conducted using Perplexity. It uses a series of AI models to generate, refine, and format the content.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/pblog`

### Workflow Steps

1.  **Webhook:** Receives a topic for research.
2.  **Perplexity Research:** An AI agent uses a custom `perplexity_research_tool` to gather information on the topic.
3.  **Article Generation:** A `gpt-4o-mini` model generates a structured article in JSON format based on the research.
4.  **HTML Conversion:** Another `gpt-4o-mini` model converts the JSON article into a single-line HTML document with Tailwind CSS styling.
5.  **Telegram Notification:** A summary of the article is sent to a Telegram chat.
6.  **Respond to Webhook:** The final HTML content is sent back as the webhook response.

---

## 67. 1/AI_Research_RAG_and_Data_Analysis/Analyze tradingview.com charts with Chrome extension, N8N and OpenAI.txt

**Workflow:** Analyze tradingview.com charts with Chrome extension, N8N and OpenAI

This workflow provides an AI-powered technical analysis of financial charts from tradingview.com, delivered through a Chrome extension.

### Trigger

- **Type:** Webhook
- **Method:** POST
- **URL Path:** `/e9a97dd5-f1e7-4d5b-a6f1-be5f0c9eb96c`

### Workflow Steps

1.  **Webhook:** Receives a base64 encoded image of a chart from the Chrome extension.
2.  **OpenAI Image Analysis:** A `gpt-4o-mini` model analyzes the image, providing technical analysis and market predictions in simple terms.
3.  **Respond to Webhook:** The analysis is sent back as the response to the webhook, which is then displayed by the Chrome extension.

---

## 68. 1/AI_Research_RAG_and_Data_Analysis/Automated Hugging Face Paper Summary Fetching & Categorization Workflow.txt

**Workflow:** Automated Hugging Face Paper Summary Fetching & Categorization Workflow

This workflow is an anomaly detection tool for a dataset of crop images. It uses a Voyage AI embedding model and a Qdrant vector database to identify images that do not belong to the known crop categories.

### Trigger

- **Type:** Execute Workflow Trigger
- **Input:** An image URL.

### Workflow Steps

1.  **Embed Image:** The input image is converted into a vector embedding using the `voyage-multimodal-3` model.
2.  **Get Similarity of Medoids:** The embedding is compared against the pre-calculated cluster centers (medoids) of known crop types stored in a Qdrant database.
3.  **Compare Scores:** A Python script compares the similarity scores against pre-defined thresholds for each crop type.
4.  **Output:** The workflow returns a message indicating whether the image is similar to a known crop or if it is a potential anomaly.

---

## 69. 1/AI_Research_RAG_and_Data_Analysis/Autonomous AI crawler.txt

**Workflow:** Autonomous AI Crawler

This workflow acts as an autonomous AI crawler that can scrape text and URLs from websites. It is designed to be used as a tool within other workflows.

### Tools

-   **text_retrieval_tool:** Takes a URL as input and returns all the text content from the webpage after converting it to Markdown.
-   **url_retrieval_tool:** Takes a URL as input and returns all the hyperlinks found on the webpage.

### Workflow Steps

1.  **Get Companies:** Retrieves a list of companies and their websites from a Supabase table.
2.  **Loop through Companies:** For each company, the workflow performs the following steps:
3.  **URL Retrieval:** Uses the `url_retrieval_tool` to get all URLs from the company's website.
4.  **Social Media Extraction:** An OpenAI model (`gpt-4o`) processes the extracted URLs to identify social media links.
5.  **Data Merging:** The company's information is merged with the extracted social media links.
6.  **Insert New Row:** The combined data is inserted into a new Supabase table.

---

## 70. 1/AI_Research_RAG_and_Data_Analysis/Build a Financial Documents Assistant using Qdrant and Mistral.ai.txt

**Workflow:** Build a Financial Documents Assistant using Qdrant and Mistral.ai

This workflow creates a question-and-answer AI assistant for financial documents. It monitors a local folder for new documents, synchronizes them with a Qdrant vector database, and uses a Mistral AI model to answer questions about the documents.

### Trigger

- **Type:** Local File Trigger
- **Path:** `/home/node/host_mount/local_file_search`
- **Events:** `add`, `change`, `unlink`

### Workflow Steps

1.  **File Synchronization:**
    *   When a file is added or changed, it is read, and its content is converted into vector embeddings using a Mistral model. The embeddings are then stored in a Qdrant collection.
    *   If a file is deleted, its corresponding vector is removed from the Qdrant collection.
2.  **Q&A Agent:**
    *   A chat trigger receives questions from the user.
    *   A Mistral AI chat model, combined with a vector store retriever, answers the questions based on the content of the documents in the Qdrant database.
---

## 71. 1/AI_Research_RAG_and_Data_Analysis/Build a Tax Code Assistant with Qdrant, Mistral.ai and OpenAI.txt

**Workflow:** Build a Tax Code Assistant with Qdrant, Mistral.ai and OpenAI

This workflow creates a tax code assistant that can answer questions about Texas tax codes. It downloads the tax code, processes it, and uses a combination of AI models to provide answers.

### Trigger

- **Type:** Manual

### Workflow Steps

1.  **Download and Extract:** Downloads a zip file containing Texas tax codes as PDFs and extracts them.
2.  **Process PDFs:** Each PDF is processed to extract chapters and sections.
3.  **Embed and Store:** The content is chunked, and embeddings are generated using a Mistral model. The embeddings are then stored in a Qdrant vector database.
4.  **Q&A Agent:**
    *   A chat trigger receives user questions.
    *   The user's question is embedded using a Mistral model.
    *   The Qdrant database is searched for relevant tax code sections.
    *   A Mistral chat model generates an answer based on the retrieved context.

---

## 72. 1/AI_Research_RAG_and_Data_Analysis/Build Your Own Image Search Using AI Object Detection, CDN and ElasticSearch.txt

**Workflow:** Build Your Own Image Search Using AI Object Detection, CDN and ElasticSearch

This workflow builds an image search service based on object detection. It identifies objects in an image, crops them, and indexes them in Elasticsearch.

### Trigger

- **Type:** Manual

### Workflow Steps

1.  **Fetch Image:** An image is fetched from a URL.
2.  **Object Detection:** A `detr-resnet-50` model from Cloudflare Workers AI is used to detect objects in the image.
3.  **Crop Objects:** The identified objects are cropped from the source image.
4.  **Upload to CDN:** The cropped images are uploaded to Cloudinary.
5.  **Index in Elasticsearch:** The public URL of each cropped image, along with its label and other metadata, is indexed in an Elasticsearch database.

---

## 73. 1/AI_Research_RAG_and_Data_Analysis/Building RAG Chatbot for Movie Recommendations with Qdrant and Open AI.txt

**Workflow:** Building RAG Chatbot for Movie Recommendations with Qdrant and Open AI

This workflow creates a movie recommendation chatbot. It uses a dataset of movies, embeds their descriptions, and then uses a RAG pipeline to provide recommendations.

### Trigger

- **Type:** Manual (for indexing) and Chat (for recommendations)

### Workflow Steps

1.  **Indexing:**
    *   A CSV file with movie data is fetched from GitHub.
    *   The movie descriptions are embedded using OpenAI's `text-embedding-3-small` model.
    *   The embeddings are stored in a Qdrant vector database.
2.  **Recommendation:**
    *   A chat trigger receives a user's request for a movie recommendation.
    *   An AI agent uses a custom `movie_recommender` tool to query the Qdrant database for movies based on positive and negative examples provided by the user.
    *   The agent then provides the top 3 movie recommendations.

---

## 74. 1/AI_Research_RAG_and_Data_Analysis/Chat with GitHub API Documentation_ RAG-Powered Chatbot with Pinecone & OpenAI.txt

**Workflow:** Chat with GitHub API Documentation: RAG-Powered Chatbot with Pinecone & OpenAI

This workflow creates a chatbot that can answer questions about the GitHub API. It uses the GitHub API's OpenAPI specification as its knowledge base.

### Trigger

- **Type:** Manual (for indexing) and Chat (for questions)

### Workflow Steps

1.  **Indexing:**
    *   The GitHub API's OpenAPI specification is downloaded.
    *   The specification is split into chunks, and embeddings are generated using OpenAI.
    *   The embeddings are stored in a Pinecone vector database.
2.  **Chatbot:**
    *   A chat trigger receives user questions about the GitHub API.
    *   An AI agent uses a vector store tool to query the Pinecone database for relevant information.
    *   An OpenAI `gpt-4o-mini` model generates an answer based on the retrieved context.

---

## 75. 1/AI_Research_RAG_and_Data_Analysis/Create a Google Analytics Data Report with AI and sent it to E-Mail and Telegram.txt

**Workflow:** Create a Google Analytics Data Report with AI and sent it to E-Mail and Telegram

This workflow generates a weekly Google Analytics report, enriches it with AI-powered analysis, and sends it via email and Telegram.

### Trigger

- **Type:** Schedule (weekly)

### Workflow Steps

1.  **Fetch Data:** Retrieves Google Analytics data for the last 7 days and the same period from the previous year.
2.  **Data Processing:** The data is summarized and prepared for analysis.
3.  **AI Analysis:** An OpenAI `gpt-4o-mini` model compares the data from the two periods and generates a report in HTML format.
4.  **Send Email:** The HTML report is sent as an email.
5.  **Send Telegram Message:** The HTML report is converted to plain text and sent as a Telegram message.
---

## 76. 1/AI_Research_RAG_and_Data_Analysis/Customer Insights with Qdrant, Python and Information Extractor.txt

**Workflow:** Customer Insights with Qdrant, Python and Information Extractor

This workflow extracts customer insights from TrustPilot reviews. It scrapes reviews, stores them in a Qdrant vector database, and then uses Python and an information extractor to analyze the data.

### Trigger

- **Type:** Manual

### Workflow Steps

1.  **Scrape Reviews:** Scrapes reviews from a TrustPilot page.
2.  **Process and Store:** The reviews are processed, and the text is embedded using an OpenAI model. The embeddings are then stored in a Qdrant collection.
3.  **Cluster and Analyze:** The workflow clusters the reviews based on their embeddings and then uses a Python script and an information extractor to identify key themes and insights from the clusters.
4.  **Export to Sheets:** The extracted insights are exported to a Google Sheet.

---

## 77. 1/AI_Research_RAG_and_Data_Analysis/Deduplicate Scraping AI Grants for Eligibility using AI.txt

**Workflow:** Deduplicate Scraping AI Grants for Eligibility using AI

This workflow scrapes AI grant opportunities from grants.gov, deduplicates them, and uses AI to determine eligibility and summarize the grant details.

### Trigger

- **Type:** Manual

### Workflow Steps

1.  **Scrape Grants:** Fetches AI-related grant opportunities from grants.gov.
2.  **Deduplicate:** Removes any grants that have been processed in previous executions.
3.  **Get Grant Details:** For each new grant, it fetches the full details.
4.  **AI Analysis:**
    *   An OpenAI model summarizes the grant's synopsis.
    *   Another OpenAI model determines eligibility based on a predefined company profile.
5.  **Save to Airtable:** The grant details, summary, and eligibility information are saved to an Airtable base.
6.  **Email Notification:** An email is generated with a summary of the new eligible grants.

---

## 78. 1/AI_Research_RAG_and_Data_Analysis/Enrich Property Inventory Survey with Image Recognition and AI Agent.txt

**Workflow:** Enrich Property Inventory Survey with Image Recognition and AI Agent

This workflow enriches a property inventory survey in Airtable by using image recognition and an AI agent to identify and describe items from photos.

### Trigger

- **Type:** Manual

### Workflow Steps

1.  **Get Rows:** Fetches rows from an Airtable base where an image is present but the AI status is false.
2.  **Image Analysis:** An OpenAI vision model analyzes the image to provide a detailed description of the item.
3.  **AI Agent:** An AI agent with two tools (`reverse_image_search` and `webpage_url_scraper_tool`) is used to find more information about the item online.
4.  **Update Airtable:** The Airtable row is updated with the enriched information, including the item's title, description, model, material, color, and condition.

---

## 79. 1/AI_Research_RAG_and_Data_Analysis/Extract insights & analyse YouTube comments via AI Agent chat.txt

**Workflow:** Extract insights & analyse YouTube comments via AI Agent chat

This workflow provides a comprehensive toolset for analyzing YouTube channels and videos. It uses a set of custom tools within an AI agent to perform various tasks.

### Trigger

- **Type:** Chat

### Tools

-   **get_channel_details:** Get channel ID, title, and description from a handle.
-   **get_video_description:** Get the full description, title, and publish date of a video.
-   **get_list_of_videos:** Retrieve a list of videos from a channel.
-   **get_list_of_comments:** Retrieve a list of comments from a video.
-   **search:** Search for videos or channels.
-   **analyze_thumbnail:** Analyze a thumbnail image.
-   **video_transcription:** Transcribe a video.

### Workflow Steps

1.  **Chat Input:** The user interacts with the AI agent through a chat interface.
2.  **Tool Execution:** The AI agent determines which tool to use based on the user's request and executes it.
3.  **Response:** The agent returns the result of the tool's execution to the user.

---

## 80. 1/AI_Research_RAG_and_Data_Analysis/Generate SEO Seed Keywords Using AI.txt

**Workflow:** Generate SEO Seed Keywords Using AI

This workflow generates a list of SEO seed keywords based on an Ideal Customer Profile (ICP).

### Trigger

- **Type:** Manual

### Workflow Steps

1.  **Set ICP:** The user provides details about their ideal customer, including pain points, goals, and current solutions.
2.  **AI Agent:** An Anthropic chat model, acting as an expert SEO strategist, analyzes the ICP and generates a list of 15-20 seed keywords.
3.  **Output:** The list of keywords is split into individual items, which can then be saved to a database or spreadsheet.
---

## 81. 1/AI_Research_RAG_and_Data_Analysis/Hacker News Job Listing Scraper and Parser.txt

**Workflow:** Hacker News Job Listing Scraper and Parser

This workflow scrapes job listings from the "Who is hiring?" threads on Hacker News, parses the job details using AI, and saves the structured data to Airtable.

### Trigger

- **Type:** Manual

### Workflow Steps

1.  **Search for Posts:** Searches for "Ask HN: Who is hiring?" posts on Hacker News using the Algolia API.
2.  **Filter Recent Posts:** Filters for posts created in the last 30 days.
3.  **Get Post Details:** Fetches the details of the latest "Who is hiring?" post, including the IDs of the comments (job listings).
4.  **Process Job Listings:** For each job listing (comment):
    *   Fetches the full comment text.
    *   Cleans the HTML from the text.
    *   Uses an OpenAI model to parse the text and extract structured data (company, title, location, etc.).
5.  **Save to Airtable:** The structured job data is saved to an Airtable base.

---

## 82. 1/AI_Research_RAG_and_Data_Analysis/Hacker News to Video Content.txt

**Workflow:** Hacker News to Video Content

This workflow transforms Hacker News articles into video content. It uses AI to summarize the article, generate images, and create a video.

### Trigger

- **Type:** Manual

### Workflow Steps

1.  **Get Hacker News Stories:** Fetches the top stories from Hacker News.
2.  **Analyze Article:** For each story, an AI agent reads the article and generates a summary, a related topic, and image prompts.
3.  **Generate Images:** Uses Leonardo AI to generate images based on the prompts.
4.  **Generate Video:** Uses RunwayML to create a video from the generated images.
5.  **Upload Video:** The final video is uploaded to a Minio S3 bucket.

---

## 83. 1/AI_Research_RAG_and_Data_Analysis/Host Your Own AI Deep Research Agent with n8n, Apify and OpenAI o3.txt

**Workflow:** Host Your Own AI Deep Research Agent with n8n, Apify and OpenAI o3

This workflow creates a deep research agent that can be hosted on n8n. It takes a research prompt and performs a multi-step, recursive search to gather information.

### Trigger

- **Type:** Form

### Workflow Steps

1.  **Initial Prompt:** The user submits a research prompt and specifies the desired research depth and breadth.
2.  **Query Generation:** An OpenAI model generates a set of initial search queries based on the prompt.
3.  **Recursive Research:** The workflow enters a loop that continues for the specified depth:
    *   For each query, it performs a web search using the Apify Fast Google Search actor.
    *   The content of the top search results is scraped.
    *   An OpenAI model analyzes the scraped content to extract key learnings and generate follow-up questions.
    *   The follow-up questions are used to generate new search queries for the next iteration.
4.  **Final Report:** Once the desired depth is reached, the accumulated learnings and URLs are saved to a Notion database.

---

## 84. 1/AI_Research_RAG_and_Data_Analysis/Intelligent Web Query and Semantic Re-Ranking Flow using Brave and Google Gemini.txt

**Workflow:** Intelligent Web Query and Semantic Re-Ranking Flow using Brave and Google Gemini

This workflow performs an intelligent web search by first generating an optimal search query and then re-ranking the results based on semantic relevance.

### Trigger

- **Type:** Webhook

### Workflow Steps

1.  **Query Generation:** A Google Gemini model takes a user's research question and generates an optimized search query.
2.  **Web Search:** The Brave Search API is used to perform a web search with the generated query.
3.  **Result Re-ranking:** A second Google Gemini model re-ranks the search results based on their relevance to the original research question.
4.  **Information Extraction:** The model also extracts the most relevant information from the top-ranked results.
5.  **Response:** The top 10 re-ranked URLs and the extracted information are returned as the webhook response.

---

## 85. 1/AI_Research_RAG_and_Data_Analysis/Learn Anything from HN - Get Top Resource Recommendations from Hacker News.txt

**Workflow:** Learn Anything from HN - Get Top Resource Recommendations from Hacker News

This workflow finds the best resources to learn a specific topic by searching for and analyzing discussions on Hacker News.

### Trigger

- **Type:** Form

### Workflow Steps

1.  **Get Topic:** The user submits a topic they want to learn about and their email address.
2.  **Search Hacker News:** The workflow searches for "Ask HN" posts related to the topic.
3.  **Fetch Comments:** It then fetches all the comments from the relevant posts.
4.  **AI Analysis:** A Google Gemini model analyzes the comments, identifies the top recommended resources (courses, books, articles, etc.), and categorizes them by type and difficulty level.
5.  **Send Email:** The curated list of resources is formatted into an HTML email and sent to the user.
## 90. 1/AI_Research_RAG_and_Data_Analysis/Make OpenAI Citation for File Retrieval RAG.txt

This workflow enhances the output of an OpenAI Assistant that uses file retrieval for RAG (Retrieval-Augmented Generation). It processes the assistant's response to format citations, making them more user-friendly by replacing standard citation markers with the actual source filenames.

**Trigger:** The workflow is initiated via a Chat Trigger, allowing for interactive use.

**Functionality:**

1.  **Initiate Chat:** The workflow starts with a user's prompt to the chat trigger.
2.  **Query OpenAI Assistant:** The prompt is sent to a pre-configured OpenAI Assistant that is equipped with a vector store for file retrieval. The assistant generates a response that includes citations pointing to the source files.
3.  **Fetch Thread Content:** An HTTP request is made to the OpenAI API to retrieve the complete message thread, which contains detailed information about the assistant's response and citations.
4.  **Isolate Citations:** The workflow uses a series of `Split Out` nodes to parse the API response, isolating each message, its content, and the specific citation annotations.
5.  **Retrieve Filenames:** For each citation, another HTTP request is made to the OpenAI Files API to fetch the metadata of the source file, specifically its filename.
6.  **Format and Aggregate:** The data is cleaned to retain only the essential information (citation ID, filename, and the text to be replaced). All processed citations are then aggregated into a single item.
7.  **Substitute Citations:** A `Code` node iterates through the aggregated citations and replaces the original citation text in the assistant's output with a formatted string that includes the source filename (e.g., "_(source_document.pdf)_").
8.  **Optional HTML Conversion:** A disabled node is available to convert the final Markdown-formatted text into HTML if needed.

---

## 91. 1/AI_Research_RAG_and_Data_Analysis/Open Deep Research - AI-Powered Autonomous Research Workflow.txt

This workflow acts as an AI-powered autonomous research assistant. Given a user's query, it generates relevant search terms, scours the web for information, extracts the most pertinent context, and compiles a detailed, structured report.

**Trigger:** The workflow starts when a user sends a message to the Chat Trigger.

**Functionality:**

1.  **Generate Search Queries:** The initial user query is fed to an LLM (via OpenRouter) which generates up to four distinct and precise search queries to cover the topic comprehensively.
2.  **Perform Web Searches:** The generated queries are sent to the SerpAPI service to perform Google searches, retrieving a list of organic search results for each.
3.  **Format Search Results:** The raw SerpAPI output is processed to extract the title, URL, and source for each search result.
4.  **Scrape Web Pages:** The URLs from the search results are passed to Jina AI's reader endpoint (`r.jina.ai`), which scrapes the full content of each webpage.
5.  **Extract Relevant Context:** The scraped webpage content is passed to another LLM agent. This agent is tasked with extracting only the information that is directly relevant to the original user query.
6.  **Generate Final Report:** All the extracted, relevant contexts from the various sources are merged and passed to a final LLM agent. This agent acts as a research writer, generating a comprehensive, well-structured report in Markdown format, complete with headings and key findings.
7.  **Tool Integration:** The workflow is also equipped with a Wikipedia tool, allowing the research agent to fetch information directly from Wikipedia if needed.

---

## 92. 1/AI_Research_RAG_and_Data_Analysis/Query Perplexity AI from your n8n workflows.txt

This workflow provides a simple and direct example of how to query the Perplexity AI API from within an n8n workflow. It demonstrates how to structure the API request and handle the response.

**Trigger:** The workflow is triggered manually by clicking the "Test workflow" button.

**Functionality:**

1.  **Set Parameters:** A `Set` node is used to define the parameters for the API call. This includes:
    *   `system_prompt`: Instructions for the AI model (e.g., "You are an n8n fanboy.").
    *   `user_prompt`: The actual question or query for the AI (e.g., "What are the differences between n8n and Make?").
    *   `domains`: A comma-separated list of domains to restrict the search to (e.g., "n8n.io, make.com").
2.  **Perplexity API Request:** An `HTTPRequest` node sends a POST request to the Perplexity AI `chat/completions` endpoint. The body of the request is a JSON object containing the model to use (`sonar`), the prompts, and other parameters like temperature and domain filters.
3.  **Clean Output:** The JSON response from the Perplexity API is processed by a final `Set` node, which extracts the main content of the message and a list of the sources (citations) used to generate the answer.

---

## 93. 1/AI_Research_RAG_and_Data_Analysis/Recipe Recommendations with Qdrant and Mistral.txt

This workflow creates a sophisticated recipe recommendation system. It operates in two phases: first, it scrapes recipe data from the HelloFresh website, creates vector embeddings, and stores them in a Qdrant database. Second, it provides a chat interface for users to get personalized recipe recommendations based on their preferences.

**Trigger:** The data ingestion part is triggered manually, while the recommendation part is triggered by a Chat Trigger.

**Functionality:**

**Part 1: Data Ingestion & Vector Storage**

1.  **Scrape Menu:** The workflow fetches the current week's menu from the HelloFresh UK website.
2.  **Extract Recipe Data:** It parses the HTML to extract a list of available courses and then, for each course, scrapes the full recipe page to get details like description, ingredients, utensils, and instructions.
3.  **Prepare Documents:** The scraped data for each recipe is merged and formatted into a clean, structured text document.
4.  **Generate Embeddings:** The prepared recipe document is fed to a Mistral embedding model to create a vector representation of the recipe.
5.  **Store in Qdrant:** The documents and their corresponding embeddings are then loaded and stored in a Qdrant vector collection named `hello_fresh`. (This step is handled by the Qdrant integration).

**Part 2: Recipe Recommendation Chatbot**

1.  **Chat Interface:** A user interacts with the system via a chat interface, describing the kind of meal they want.
2.  **Tool-Based Agent:** The chat is powered by a Mistral chat model configured as an agent with a custom tool named `get_recipe_recommendation`.
3.  **Query Analysis:** The agent understands the user's request and calls the custom tool, passing the user's preferences as "positive" (what they want) and "negative" (what they want to avoid) descriptions.
4.  **Query Embedding:** The positive and negative descriptions are converted into vector embeddings using the Mistral embedding model.
5.  **Qdrant Recommendation:** The workflow makes a `recommend` API call to the Qdrant collection. It uses the positive and negative vectors to find the most relevant recipes in the database.
6.  **Return Results:** Qdrant returns a list of recommended recipes, which are then formatted and presented to the user in the chat.

---

## 94. 1/AI_Research_RAG_and_Data_Analysis/Reconcile Rent Payments with Local Excel Spreadsheet and OpenAI.txt

This workflow automates the tedious process of reconciling rent payments by using an AI agent to analyze bank statements against tenant data stored in a local Excel file. It is designed for self-hosted n8n instances to ensure data privacy by keeping all files on the local system.

**Trigger:** The workflow is triggered by a `Local File Trigger` which watches a specified folder for new `.csv` files (bank statements).

**Functionality:**

1.  **Watch for Statements:** The workflow activates whenever a new CSV file is added to the designated reconciliation folder.
2.  **Read and Extract Data:** The new CSV file is read, and its data is extracted for processing.
3.  **AI Agent Analysis:** The extracted bank statement data is passed as context to an AI Agent powered by an OpenAI model (e.g., GPT-4o).
4.  **Agent Instructions:** The agent is given a detailed system prompt instructing it to:
    *   Identify missed or late rent payments.
    *   Flag incorrect payment amounts (over or underpayments).
    *   Note tenants whose leases are ending soon.
    *   Check for any outstanding fees.
5.  **Custom Tools for Data Retrieval:** The agent is equipped with two custom `Code` nodes that act as tools, allowing it to query a local Excel file (`reconcilation-workbook.xlsx`):
    *   `get_tenant_details`: Retrieves tenant information (rent amount, due dates, etc.) from the 'tenants' sheet.
    *   `get_property_details`: Retrieves property information from the 'properties' sheet.
6.  **Generate Actionable Report:** The agent uses the tools to cross-reference the bank statement with the tenant data and generates a structured JSON report of any issues that require action.
7.  **Update Spreadsheet:** The JSON output from the agent is parsed, and a final `Code` node appends each flagged issue as a new row to an 'alerts' sheet within the same local Excel workbook, creating a clear log of items to be addressed.
## 95. 1/AI_Research_RAG_and_Data_Analysis/Scrape and summarize posts of a news site without RSS feed using AI and save them to a NocoDB.txt

This workflow automates the process of monitoring a news website that does not provide an RSS feed. It scrapes the site for new articles, uses AI to process them, and saves the results to a NocoDB database.

**Trigger:** The workflow is designed to be run on a schedule (e.g., weekly) using a Cron job.

**Functionality:**

1.  **Fetch News Page:** It starts by making an HTTP request to the main news page to get its HTML content.
2.  **Extract Links and Dates:** It uses the `HTML` node to parse the page and extract the URLs and publication dates of all listed articles.
3.  **Filter Recent Posts:** A `Code` node filters the extracted articles, keeping only those published within a specified recent period (e.g., the last 7 days) to avoid processing old content.
4.  **Scrape Individual Articles:** For each recent article, it makes another HTTP request to its specific URL to fetch its full page content.
5.  **Extract Content and Title:** The `HTML` node is used again to extract the main title and body content from each article page.
6.  **AI Summarization:** The extracted article content is sent to the OpenAI API (GPT-4) with a prompt to generate a concise summary (under 70 words).
7.  **AI Keyword Extraction:** The content is sent to OpenAI again with a prompt to identify the three most important technical keywords from the text.
8.  **Merge and Structure Data:** The workflow uses a series of `Merge` nodes to combine all the extracted and generated data—date, link, title, content, summary, and keywords—into a single, structured item for each article.
9.  **Save to NocoDB:** The final structured data is then sent to a NocoDB table to be stored. (The final NocoDB node is implied by the workflow's description).

---

## 96. 1/AI_Research_RAG_and_Data_Analysis/Scrape and summarize webpages with AI.txt

This workflow demonstrates how to scrape a series of webpages, in this case, essays from Paul Graham's website, and use a LangChain summarization chain to create a concise summary for each.

**Trigger:** The workflow is triggered manually.

**Functionality:**

1.  **Fetch Article List:** An `HTTPRequest` node fetches the main articles page (`articles.html`) from paulgraham.com.
2.  **Extract Article Links:** An `HTML` node parses the fetched page and extracts the relative URLs for all the essays listed.
3.  **Process in Batches:** The list of essay URLs is split into individual items, and a `Limit` node is used to process only the first few (e.g., 3) for demonstration purposes.
4.  **Fetch Full Essay Text:** For each essay URL, another `HTTPRequest` node fetches the full HTML content of that essay's page.
5.  **Summarize with LangChain:** The core of the workflow is the `Summarization Chain` node. This LangChain node takes the full text of the essay, automatically handles text splitting and chunking, and uses an OpenAI model (like `gpt-4o-mini`) to generate a summary of the content.
6.  **Extract Title:** In parallel, an `HTML` node extracts the `<title>` from the essay page.
7.  **Combine and Clean:** The generated summary and the extracted title are merged, and a final `Set` node cleans up the data, producing a final output with the essay's title, its AI-generated summary, and the original URL.

---

## 97. 1/AI_Research_RAG_and_Data_Analysis/Scrape Trustpilot Reviews with DeepSeek, Analyze Sentiment with OpenAI.txt

This workflow automates scraping reviews from Trustpilot, extracting structured data using an AI model, analyzing the sentiment of the review, and saving the results to a Google Sheet, ensuring no duplicate entries are created.

**Trigger:** The workflow is triggered manually.

**Functionality:**

1.  **Scrape Trustpilot Pages:** The workflow starts by making paginated HTTP requests to a specified company's Trustpilot review page to fetch the HTML content of recent reviews.
2.  **Extract Review Links:** It parses the HTML to extract the unique URLs for each individual review.
3.  **Check for Duplicates:** For each review URL, it queries a Google Sheet to check if a review with that specific ID has already been saved. An `If` node then stops the process for any review that already exists.
4.  **Fetch Full Review:** If the review is new, an HTTP request fetches the full HTML of the individual review page.
5.  **AI Information Extraction:** The raw HTML of the review is passed to a DeepSeek model via the `Information Extractor` node. A detailed schema instructs the model to extract specific fields: author, rating, date, title, text, total number of reviews by the author, and their country.
6.  **AI Sentiment Analysis:** The extracted review text is then sent to an OpenAI model with a prompt to classify its sentiment (e.g., Positive, Negative, Neutral).
7.  **Append to Google Sheets:** Finally, all the extracted information (author, rating, date, etc.) along with the determined sentiment is appended as a new row to the Google Sheet, creating a structured database of customer feedback.

---

## 98. 1/AI_Research_RAG_and_Data_Analysis/Send Google analytics data to A.I. to analyze then save results in Baserow.txt

This workflow automates weekly SEO and website performance analysis by fetching data from Google Analytics, sending it to an AI for interpretation, and saving the insights into a Baserow database.

**Trigger:** The workflow can be run manually or on a weekly schedule.

**Functionality:**

1.  **Fetch GA Data (This Week vs. Last Week):** The workflow executes a series of parallel branches to pull data from the Google Analytics API. For each metric, it fetches data for the most recent 7 days and the 7 days prior to that for comparison. The metrics include:
    *   **Page Engagement:** Page views, active users, views per user.
    *   **Google Search Console Results:** Clicks, impressions, CTR, and average position for landing pages.
    *   **Traffic by Country:** Active users, new users, and engagement rate segmented by country.
2.  **Parse and Format Data:** After each API call, a `Code` node parses the raw JSON response from Google Analytics, cleans it, and transforms it into a simplified, structured format.
3.  **Send to AI for Analysis:** All the formatted data from the different reports (this week's and last week's) is compiled and sent to an OpenAI model. The AI is prompted to act as an SEO expert, analyze the data, identify trends, and provide insights on performance changes between the two weeks.
4.  **Save to Baserow:** The analysis and insights generated by the AI are then saved as a new entry in a specified Baserow table, creating a historical log of weekly performance reports.
## 99. 1/AI_Research_RAG_and_Data_Analysis/Spot Workplace Discrimination Patterns with AI.txt

This workflow is designed to analyze public employee reviews from Glassdoor to identify potential patterns of workplace discrimination or bias. It scrapes company data, extracts relevant text, and uses AI to analyze both qualitative reviews and quantitative demographic data.

**Trigger:** The workflow is triggered manually.

**Functionality:**

1.  **Scrape Glassdoor:** It uses ScrapingBee, a web scraping API, to first search for a specified company on Glassdoor and then navigate to its main page and reviews page.
2.  **Extract Review and Demographic Data:** It parses the HTML of the reviews page to extract two key sections:
    *   The qualitative review summary.
    *   The quantitative "Demographics" module, which contains data on diversity and inclusion.
3.  **AI Analysis of Qualitative Reviews:** The text from the review summary is sent to an OpenAI model via the `Information Extractor` node. The AI is prompted to extract the overall rating and the distribution of 1-star to 5-star reviews.
4.  **AI Analysis of Demographic Data:** The HTML content of the demographics module is sent to another `Information Extractor` node. This AI is tasked with a more complex extraction, pulling out the percentage representation for various demographic groups (e.g., by race, gender, disability status, etc.).
5.  **Final Thematic Analysis:** All the extracted data (qualitative and quantitative) is merged and sent to a final OpenAI Chat Model. This model is given a comprehensive prompt to act as an HR analyst, synthesize all the information, and generate a report summarizing any potential discrimination patterns, diversity and inclusion themes, and overall employee sentiment.
6.  **Output:** The final output is a detailed analysis from the AI, highlighting potential areas of concern regarding workplace discrimination.

---

## 100. 1/AI_Research_RAG_and_Data_Analysis/Summarize SERPBear data with AI (via Openrouter) and save it to Baserow.txt

This workflow automates the process of analyzing keyword ranking data from SERPBear, a self-hosted rank tracker. It fetches the latest data, uses an AI model for analysis, and stores the insights in a Baserow database.

**Trigger:** The workflow can be triggered manually or on a recurring schedule (e.g., weekly).

**Functionality:**

1.  **Get SERPBear Data:** An `HTTPRequest` node makes an API call to a specified SERPBear instance to retrieve the latest keyword ranking data for a given domain.
2.  **Parse and Prepare Data:** A `Code` node processes the raw JSON data from SERPBear. It calculates a 7-day average position for each keyword and determines if the ranking trend is "improving," "declining," or "stable" by comparing the current position to the average.
3.  **Construct AI Prompt:** The same `Code` node then constructs a detailed prompt for an AI model. The prompt includes a summary of each keyword's performance (current position, 7-day average, trend, and ranking URL).
4.  **Send to AI for Analysis:** The constructed prompt is sent to a large language model (e.g., Llama 3.1 70B) via the OpenRouter API. The AI is asked to act as an SEO expert, analyze the data, and provide key observations and actionable suggestions for improvement.
5.  **Save to Baserow:** The AI's response, containing the analysis and suggestions, is then saved as a new record in a Baserow table. The record includes the date of the analysis and the AI-generated notes.

---

## 101. 1/AI_Research_RAG_and_Data_Analysis/Summarize Umami data with AI (via Openrouter) and save it to Baserow.txt

This workflow provides automated analysis of website traffic data from Umami, a self-hosted web analytics tool. It fetches various metrics, uses an AI model for interpretation and comparison, and logs the insights in a Baserow database.

**Trigger:** The workflow can be run manually or on a schedule.

**Functionality:**

1.  **Fetch Umami Stats:** The workflow makes a series of API calls to a specified Umami instance to retrieve analytics data. It pulls two main types of reports:
    *   **Overall Stats:** Fetches aggregate data for the last 7 days, including pageviews, visitors, visits, bounces, and total time on site, along with the percentage change from the previous period.
    *   **Page-Specific Metrics:** Fetches a list of all visited URLs and their view counts for the current week and the previous week.
2.  **Parse and Format Data:** After each API call, a `Code` node parses the data and formats it into a clean, URL-encoded JSON string suitable for inclusion in an AI prompt.
3.  **AI Analysis:** The workflow sends two separate requests to an AI model (e.g., Llama 3.1 70B) via the OpenRouter API:
    *   The first request sends the overall stats for a high-level summary.
    *   The second request sends the page-specific data for both weeks and asks the AI to perform a comparative analysis, present it in a markdown table, and offer improvement suggestions.
4.  **Save to Baserow:** The two AI-generated responses (the summary and the detailed page analysis) are combined and saved as a single new entry in a Baserow table, creating a weekly analytics report.

---

## 102. 1/AI_Research_RAG_and_Data_Analysis/Survey Insights with Qdrant, Python and Information Extractor.txt

This is a powerful and advanced workflow for uncovering deep insights from qualitative survey data (i.e., open-ended text responses). It uses vector embeddings, clustering, and AI-powered summarization to identify thematic patterns in the answers.

**Trigger:** The workflow is triggered by another workflow, which passes in the Google Sheet ID and sheet name of the survey data to be analyzed.

**Functionality:**

**Part 1: Data Ingestion and Vectorization (Run once per survey)**

1.  **Read Survey Data:** It reads all responses from a specified Google Sheet.
2.  **Structure Data:** It converts the spreadsheet data from a wide format (one row per participant) to a long format of question-answer pairs.
3.  **Generate Embeddings:** Each answer is passed to an OpenAI embedding model (`text-embedding-3-small`) to create a vector representation of its semantic meaning.
4.  **Store in Qdrant:** The vector embeddings, along with metadata (the question, the participant ID, and the survey name), are stored in a Qdrant vector database collection.

**Part 2: Insight Generation and Reporting**

1.  **Get All Questions:** It reads the header row of the Google Sheet to get a list of all survey questions.
2.  **Process Each Question:** The workflow iterates through each question one by one.
3.  **Fetch All Answers:** For a given question, it queries the Qdrant database to retrieve all the answer vectors associated with it.
4.  **Perform Clustering:** The core of the analysis happens in a Python `Code` node. It uses the `scikit-learn` library to perform K-Means clustering on the answer vectors. This groups the answers into thematic clusters based on their semantic similarity.
5.  **Summarize Clusters:** For each cluster of answers, it sends the raw text of those answers to an OpenAI model. The AI is prompted to identify the core theme or insight of that cluster and assign it a sentiment (positive, negative, neutral).
6.  **Export to Google Sheets:** The generated insights (theme, sentiment, number of responses in the cluster, raw responses, etc.) are appended as new rows to a new "Insights" sheet created within the original Google Sheet, providing a clear and actionable summary of the survey results.

---

## 103. 1/AI_Research_RAG_and_Data_Analysis/Ultimate Scraper Workflow for n8n.txt

This is a comprehensive and robust web scraping solution that uses a remote-controlled Selenium browser to handle complex scraping tasks, including those that require bypassing bot detection measures. It is designed to be highly flexible and can be adapted to various target websites.

**Trigger:** The workflow is triggered by a webhook, which is expected to provide the target URL, the subject to search for, the website's domain, and a set of cookies for authentication.

**Functionality:**

1.  **Session Management:**
    *   **Create Session:** It starts by creating a new Selenium session with a Chrome browser instance running in a separate Docker container.
    *   **Clean Webdriver:** It executes a script to remove common signs of automation from the browser's navigator object to appear more like a human user.
    *   **Delete Session:** It includes multiple `Delete Session` nodes at the end of every possible path (success or error) to ensure the Selenium session is always closed properly, preventing resource leaks.
2.  **Cookie Injection:**
    *   It receives cookies via the webhook, validates that their domain matches the target URL, and then injects them into the Selenium browser session one by one. This is crucial for accessing pages that require a login.
3.  **Navigation and Initial Scraping:**
    *   It navigates to a search results page or a primary URL.
    *   It scrapes this initial page to find all links that match the target website's domain.
4.  **AI-Powered URL Selection:**
    *   The list of found URLs is passed to an OpenAI model via the `Information Extractor` node.
    *   The AI is prompted to act as an expert and select the single most relevant URL from the list based on the provided `Subject` and `Website Domaine`. This allows the scraper to intelligently navigate to the correct sub-page.
5.  **Final Page Scraping:**
    *   The workflow navigates to the AI-selected URL.
    *   It then executes the final scrape on this target page to extract the desired information. (The final extraction logic is meant to be customized).
6.  **Error Handling and Response:**
    *   The workflow has extensive error handling. It can detect if the request was blocked, if the page crashed, or if the cookies were invalid, and it will respond to the webhook with a specific error message and status code for each case.
    *   On success, it returns the scraped data.
## 104. Vector Database as a Big Data Analysis Tool for AI Agents (A Multi-Part Workflow Series)

This is a series of interconnected workflows that demonstrate how to use a vector database (Qdrant) not just for search, but for advanced data analysis tasks like image classification and anomaly detection. The series uses multimodal embeddings from Voyage AI to represent images and their content.

---

### Part 1: Batch Upload Dataset to Qdrant

**Full Path:** `1/AI_Research_RAG_and_Data_Analysis/Vector Database as a Big Data Analysis Tool for AI Agents [1_3 anomaly][1_2 KNN].txt`

This workflow is the first step, responsible for populating the Qdrant vector database with an image dataset. It processes images from a Google Cloud Storage bucket, embeds them, and uploads them in batches.

**Trigger:** The workflow is triggered manually.

**Functionality:**

1.  **Setup and Configuration:** It begins by setting key variables, including the Qdrant cluster URL, the target collection name (`agricultural-crops`), the embedding dimension size, and the batch size for processing.
2.  **Check/Create Collection:** It checks if the target collection already exists in Qdrant. If not, it creates a new one with the specified vector parameters (using Cosine distance).
3.  **Create Payload Index:** It creates an index on the `crop_name` payload field. This optimizes the database for filtering and counting operations based on the crop type.
4.  **Fetch Image Data:** It lists all image files from a specified Google Cloud Storage bucket.
5.  **Prepare Data:** For each image, it constructs a public URL and extracts the `cropName` from its folder path. To set up a future test case, it explicitly filters out any images of "tomato".
6.  **Batch Processing:** A Python `Code` node groups the images into batches and generates a unique UUID for each image, which is required for the Qdrant point ID.
7.  **Embed Images:** For each batch, it makes an API call to the Voyage AI multimodal embeddings endpoint, passing the public image URLs to get their vector representations.
8.  **Upload to Qdrant:** Finally, it performs a batch upload to Qdrant, sending the UUIDs, the generated vectors, and the payload (metadata including `crop_name` and the image URL) for each image.

---

### Part 2: Set Up Medoids for Anomaly Detection

**Full Path:** `1/AI_Research_RAG_and_Data_Analysis/Vector Database as a Big Data Analysis Tool for AI Agents [2_3 - anomaly].txt`

This workflow processes the data uploaded in Part 1 to prepare it for anomaly detection. It identifies the center of each class (crop type) and calculates a similarity threshold that defines the boundary of that class.

**Trigger:** The workflow is triggered manually.

**Functionality:**

1.  **Calculate Cluster Medoids (Image-based):**
    *   For each crop type, it queries Qdrant to get a distance matrix of all images within that class.
    *   A Python `Code` node uses the `scipy` library to analyze this matrix and identify the "medoid" – the single image that is most central and similar to all other images in its class.
    *   It then updates the payload of this specific point in Qdrant, flagging it with `is_medoid: true`.
2.  **Calculate Anomaly Threshold:**
    *   Using the newly found medoid as a reference, it performs another query to find the point within the same class that is *least* similar (i.e., furthest away) from the medoid.
    *   The similarity score of this furthest point is then used as the anomaly `thresholdScore`.
    *   This threshold score is saved back into the medoid's payload, effectively defining the boundary for that class.
3.  **Calculate Text Anchor Medoids (Text-based):**
    *   The workflow also defines a set of textual descriptions for each crop type.
    *   It embeds these text descriptions using Voyage AI.
    *   For each crop, it queries Qdrant to find the image whose vector is most similar to the text description's vector. This image is flagged as the `is_text_anchor_medoid`.
    *   It then calculates and saves an anomaly threshold for this text-based medoid as well.

---

### Part 3: Anomaly Detection Tool

**Full Path:** `1/AI_Research_RAG_and_Data_Analysis/Vector Database as a Big Data Analysis Tool for AI Agents [3_3 - anomaly].txt`

This workflow is the final application that uses the prepared data to perform anomaly detection. It takes a new image and determines if it belongs to any of the known crop classes or if it's an anomaly.

**Trigger:** The workflow is triggered by an `Execute Workflow Trigger`, expecting an `imageURL` in the input.

**Functionality:**

1.  **Embed Input Image:** It takes the input `imageURL` and sends it to the Voyage AI embeddings API to get its vector representation.
2.  **Query Medoids:** It uses the new image's vector to query the Qdrant collection. The query is filtered to only return the pre-calculated medoid points for every crop class.
3.  **Compare Scores to Thresholds:** A Python `Code` node iterates through the results. For each medoid returned, it compares the similarity score of the input image to the `is_medoid_cluster_threshold` stored in that medoid's payload.
4.  **Determine Outcome:**
    *   If the input image's score is **higher** than the threshold for any of the classes, it means the image falls within the boundaries of that class. The workflow returns a message like "Looks similar to {crop_name}".
    *   If the input image's score is **lower** than the thresholds for *all* classes, it is considered an anomaly. The workflow returns the message: "ALERT, we might have a new undefined crop!".

---

### Part 4: KNN Classifier Tool

**Full Path:** `1/AI_Research_RAG_and_Data_Analysis/Vector Database as a Big Data Analysis Tool for AI Agents [2_2 KNN].txt` (and identical duplicate file)

This workflow demonstrates a classic K-Nearest Neighbors (KNN) classification algorithm using a vector database. It classifies a new image based on the classes of its most similar neighbors in a pre-existing dataset of land-use images.

**Trigger:** The workflow is triggered by an `Execute Workflow Trigger`, expecting an `imageURL`.

**Functionality:**

1.  **Embed Input Image:** The input `imageURL` is sent to the Voyage AI embeddings API to generate its vector.
2.  **Initial Query:** It queries the `land-use` Qdrant collection to find the `k` (e.g., 10) nearest neighbors to the input image's vector.
3.  **Majority Vote:** A Python `Code` node takes the results and performs a majority vote on the `landscape_name` payload field of the neighboring points to determine the most likely class.
4.  **Tie-Breaking Loop:** The workflow includes a loop to handle ties.
    *   An `If` node checks if the two most common classes in the vote have an equal number of neighbors.
    *   If there is a tie, the workflow increases the number of neighbors to consider (`limitKNN`) by 5 and re-runs the Qdrant query and majority vote.
    *   This loop continues until the tie is broken or a maximum number of neighbors (e.g., 100) has been checked.
5.  **Return Class:** Once a clear winner is determined by the majority vote, a `Set` node extracts the final class name and returns it as the output.
## 105. 1/AI_Research_RAG_and_Data_Analysis/Visual Regression Testing with Apify and AI Vision Model.txt

This workflow automates visual regression testing for a list of specified webpages. It compares a current screenshot of a page against a stored baseline image, using an AI vision model to detect any changes in layout, text, or imagery.

The workflow operates in two main parts: generating baseline images and running the tests.

**Trigger:** The testing part can be run on a schedule (e.g., weekly), while the baseline generation is typically done manually as needed.

**Functionality:**

**Part 1: Generate and Update Base Images**

1.  **Get URL List:** The workflow reads a list of URLs from a Google Sheet.
2.  **Filter for Missing Bases:** It filters this list to find any URLs that do not yet have a baseline image associated with them.
3.  **Generate Screenshots:** For each URL needing a base image, it uses the Apify "Screenshot URL" actor to capture a fresh screenshot.
4.  **Store Base Image:** The captured screenshot is downloaded and then uploaded to a designated "base_images" folder in Google Drive.
5.  **Update Sheet:** The file ID of the newly uploaded image in Google Drive is saved back into the Google Sheet, linking it to the corresponding URL as its official baseline.

**Part 2: Run Visual Regression Test**

1.  **Get URL List:** The workflow again reads the full list of URLs from the Google Sheet.
2.  **Download Base Image:** For each URL, it downloads the corresponding baseline image from Google Drive.
3.  **Generate New Screenshot:** It uses the Apify actor again to capture a brand-new, current screenshot of the same URL.
4.  **AI Vision Comparison:** Both the baseline image and the new screenshot are sent as binary data to a Google Gemini vision model. The AI is prompted to act as a QA tester and meticulously compare the two images, identifying any regressions.
5.  **Structured Output:** A `Structured Output Parser` is used to ensure the AI's findings are returned in a clean, predictable JSON format, detailing the type of change (e.g., "text", "color", "position"), a description, the previous state, and the current state.
6.  **Report Generation:**
    *   The workflow filters out any pages where no changes were detected.
    *   It aggregates all the identified changes from all pages.
    *   It then creates a new issue in a Linear project, formatting the aggregated changes into a comprehensive markdown report that details each visual regression found.

---

## 106. 1/AI_Research_RAG_and_Data_Analysis/🔍 Perplexity Research to HTML_ AI-Powered Content Creation.txt

This is an advanced, end-to-end content creation pipeline. It takes a simple topic, uses an AI agent to perform in-depth research using Perplexity, generates a complete article based on that research, and finally converts the article into a polished, responsive HTML webpage styled with Tailwind CSS.

**Trigger:** The workflow is triggered by a webhook, which accepts a `topic` and a `telegram_chat_id` for notifications.

**Functionality:**

1.  **Topic Refinement:** The initial topic provided by the user is first sent to an AI model (GPT-4o Mini) to be improved and expanded into a more effective and detailed research query.
2.  **Perplexity Research Agent:** The refined topic is passed to an AI Agent. This agent is equipped with a custom `perplexity_research_tool`, which it uses to conduct comprehensive research on the subject.
3.  **Structured Article Generation:** The raw research output from the Perplexity agent is then passed to another AI model. This model is prompted to act as a writer and transform the research into a well-structured article. A `Structured Output Parser` forces the AI to return the article in a specific JSON format, including a category, title, metadata, main text, distinct sections with their own titles and quotes, and a list of hashtags.
4.  **Notification:** A brief snippet of the research result is sent to the user via Telegram to notify them that the process is running.
5.  **HTML Conversion with Tailwind CSS:** The structured article content is passed to a final, powerful AI model. This model is given a very specific and detailed prompt instructing it to:
    *   Convert the entire article into a single-line HTML document.
    *   Use Tailwind CSS classes to create a modern, responsive, and visually appealing layout (e.g., using cards).
    *   Correctly convert any markdown (like lists) into proper HTML tags.
    *   Preserve line breaks within the content while removing all other newline characters from the final HTML string.
6.  **Final Response:** The generated single-line HTML document is sent back as the final response to the initial webhook request, ready to be served or saved as a file.
## 107. 1/Airtable/AI Agent for project management and meetings with Airtable and Fireflies.txt

This workflow automates post-meeting project management by connecting Fireflies.ai, OpenAI, Airtable, and Google Calendar. It analyzes meeting transcripts, creates tasks, notifies participants, and schedules follow-up calls.

**Trigger:** The workflow is initiated by a webhook from Fireflies.ai, which fires when a meeting recording has been processed.

**Functionality:**

1.  **Get Transcript:** Upon receiving the webhook, it makes a GraphQL API call to Fireflies.ai to retrieve the full meeting transcript, including the title, participants, and a bullet-point summary.
2.  **AI Agent Analysis:** The transcript and summary are passed to an AI Agent powered by OpenAI (GPT-4o). The agent is given a system prompt instructing it to:
    *   Analyze the transcript for action items.
    *   Use a `Create Tasks` tool to log tasks in Airtable.
    *   Use a `Notify Client` tool to email participants their specific action items.
    *   Use a `Create Event` tool if a follow-up call needs to be scheduled.
3.  **Tool: Create Tasks in Airtable:**
    *   This tool is a sub-workflow that the AI agent can call.
    *   When called, it takes a list of tasks (name, description, due date, priority, project name) from the AI.
    *   It then iterates through the list and creates a new record for each task in a specified Airtable base.
4.  **Tool: Notify Client via Gmail:**
    *   This is a Gmail tool the agent can use.
    *   The agent provides the recipient's email and the action items. The tool then sends an email containing the meeting summary and the specific tasks assigned to that participant.
5.  **Tool: Create Google Calendar Event:**
    *   This is a Google Calendar tool.
    *   If the agent determines a follow-up is needed, it can create a new calendar event with a Google Meet link, inviting the relevant participants.

---

## 108. 1/Airtable/AI Agent to chat with Airtable and analyze data.txt

This workflow provides a powerful, conversational AI agent for interacting with and analyzing data stored in Airtable. Users can ask questions in natural language, and the agent will use a suite of tools to fetch, filter, and even perform calculations on the data.

**Trigger:** The workflow starts with a `Chat Trigger`, allowing users to interact with the agent through a chat interface.

**Functionality:**

1.  **Conversational Agent:** The core of the workflow is an AI Agent (OpenAI Functions Agent) that understands user requests. It maintains conversation history using a `Window Buffer Memory` node, allowing for follow-up questions.
2.  **Tool: Get Airtable Bases:** A tool that allows the agent to list all available bases in the connected Airtable account.
3.  **Tool: Get Base Schema:** A tool to retrieve the schema (tables, fields, and field types) for a specific Airtable base. This allows the agent to understand the data structure before querying.
4.  **Tool: Search Records:** The primary tool for data retrieval. The agent can use this to fetch records from a specified table. It can perform simple "get all" requests or apply filters based on the user's query (e.g., "find all orders with a status of 'shipped'").
5.  **Tool: Code for Analysis:** A powerful `Code` node tool that allows the agent to perform actions beyond simple data retrieval:
    *   **Aggregation:** It can execute Python code to perform mathematical operations like counting records, summing values, or calculating averages.
    *   **Visualization:** It can generate graphs and map images (using the Mapbox API) based on the data.
6.  **Dynamic Response:** The agent synthesizes the information gathered from its tools to provide a comprehensive answer to the user's question directly in the chat.

---

## 109. 1/Airtable/Get Airtable data via AI and Obsidian Notes.txt

This workflow creates a seamless integration between the note-taking application Obsidian and Airtable, using an AI agent as the bridge. It allows a user to query their Airtable data directly from within an Obsidian note.

**Trigger:** The workflow is triggered by a webhook, which is designed to be called from the "Post Webhook" plugin in Obsidian.

**Functionality:**

1.  **Initiate from Obsidian:** The user highlights a question within a note in Obsidian (e.g., "How many tasks are in the 'In Progress' status?"). They then use the command palette to send this selected text to the n8n webhook URL.
2.  **AI Agent Receives Query:** The webhook receives the text from Obsidian and passes it to an AI Agent.
3.  **Airtable Tool:** The agent is equipped with a single, powerful tool: the `Airtable` node configured for the "Search" operation.
4.  **Intelligent Querying:** The AI agent interprets the user's natural language question and translates it into a structured query for the Airtable tool. It determines which base and table to search and what filters to apply.
5.  **Fetch Data:** The Airtable tool executes the search and returns the relevant records to the agent.
6.  **Synthesize and Respond:** The agent processes the data returned from Airtable and formulates a concise, human-readable answer.
7.  **Return to Obsidian:** The final text answer is sent back as the response to the webhook. The Obsidian "Post Webhook" plugin then automatically inserts this response into the note, directly below the highlighted question.

---

## 110. 1/Airtable/Handling Job Application Submissions with AI and n8n Forms.txt

This workflow automates the initial stages of a hiring process by using an n8n Form to accept applications and AI to classify and parse the submitted CVs.

**Trigger:** The workflow starts when a candidate submits the `n8n Form Trigger`.

**Functionality:**

1.  **Job Application Form:** A two-step n8n Form is presented to the applicant. The first step requires them to enter their name and upload their CV as a PDF.
2.  **Extract Text from PDF:** Once the form is submitted, the workflow receives the uploaded file. The `Extract from File` node extracts all the raw text content from the PDF.
3.  **Document Classification:** The extracted text is passed to a `Text Classifier` node. This AI-powered node checks if the document is actually a "CV or Resume". This prevents submissions of incorrect document types.
4.  **AI-Powered Information Extraction:** If the document is classified correctly, the text is then sent to an `Information Extractor` node. This node uses an OpenAI model and a predefined schema to parse the unstructured text and extract key information into a structured JSON object. The schema includes fields like:
    *   Name
    *   Address
    *   Email & Telephone
    *   Education
    *   Skills & Technologies
    *   Years of Experience
    *   Cover Letter
5.  **Save to Airtable:** The structured JSON data extracted by the AI is used to create a new record in an "Job Applications" Airtable base.
6.  **Upload Original File:** In a final step, the workflow makes a call to the Airtable API to upload the original PDF file as an attachment to the newly created record.
7.  **Confirmation:** The candidate is shown a success message, confirming their application has been received.

---

## 111. 1/Airtable/vAssistant for Hubspot Chat using OpenAi and Airtable.txt

This workflow creates an AI-powered virtual assistant that integrates directly with HubSpot Chat. It uses an OpenAI Assistant to understand user queries and a combination of Airtable and external APIs as its knowledge sources to provide answers.

**Trigger:** The workflow is triggered by a HubSpot webhook that fires for new inbound messages in the conversation inbox.

**Functionality:**

1.  **Get New Message:** When a new message is received in HubSpot, the workflow retrieves the full message content using its ID.
2.  **Check/Create Airtable Record:** It checks an Airtable base to see if a record for the current HubSpot thread ID already exists.
    *   If **no**, it creates a new OpenAI Assistant thread and saves the new OpenAI `thread_id` to Airtable, linked to the HubSpot `thread_id`.
    *   If **yes**, it retrieves the existing OpenAI `thread_id` from Airtable.
3.  **Send Message to OpenAI:** The user's message is added to the appropriate OpenAI thread.
4.  **Run Assistant:** The workflow triggers a "run" on the OpenAI Assistant. The assistant is pre-configured with a set of tools.
5.  **Tool Execution Loop:**
    *   The workflow enters a loop, continuously checking the status of the "run".
    *   If the status is `requires_action`, it means the assistant needs to use one of its tools.
    *   A `Switch` node routes the request to the correct tool based on the function name called by the assistant.
6.  **Tools:**
    *   **Airtable Knowledge Base:** A tool that allows the assistant to query an Airtable base to find information.
    *   **ListaFirme API:** A tool that calls an external Romanian API (`listafirme.ro`) to look up company information by tax code.
7.  **Submit Tool Output:** The data retrieved by the tool is submitted back to the OpenAI run. The assistant then uses this information to formulate its final answer.
8.  **Get Final Response:** Once the run status is `completed`, the workflow retrieves the last message from the thread, which contains the AI's answer.
9.  **Respond in HubSpot:** The final answer from the AI is sent back as a new message in the HubSpot chat thread, continuing the conversation with the user.
## 112. 1/Database_and_Storage/Chat with Postgresql Database.txt

This workflow provides a conversational AI agent that can connect to and query a PostgreSQL database. It allows users to ask questions in natural language, which the agent translates into SQL queries to fetch the required information.

**Trigger:** The workflow is initiated via a `Chat Trigger`, allowing for interactive conversations.

**Functionality:**

1.  **AI Agent Core:** The central component is an `AI Agent` (OpenAI Functions Agent) powered by an OpenAI chat model. It's given a system prompt that instructs it to act as a database assistant.
2.  **Conversation Memory:** A `Window Buffer Memory` node is used to keep track of the conversation history, enabling the agent to understand follow-up questions and maintain context.
3.  **Tool: Get DB Schema and Tables List:** This `Postgres Tool` executes a query on the `information_schema` to get a list of all tables and their corresponding schemas. This allows the agent to know what tables are available to query.
4.  **Tool: Get Table Definition:** This tool takes a table and schema name and queries the `information_schema` to get the detailed definition of that table, including column names, data types, and foreign key relationships. This helps the agent construct valid queries.
5.  **Tool: Execute SQL Query:** This is the primary action tool. The agent can generate any SQL query based on the user's request and pass it to this tool for execution against the PostgreSQL database.
6.  **Interaction Flow:**
    *   A user asks a question (e.g., "How many customers are from Germany?").
    *   The agent first uses the "Get DB Schema and Tables List" and "Get Table Definition" tools to understand the database structure.
    *   It then constructs the appropriate SQL query (e.g., `SELECT COUNT(*) FROM public.customers WHERE country = 'Germany';`).
    *   It passes this query to the "Execute SQL Query" tool.
    *   The tool runs the query and returns the result to the agent.
    *   The agent synthesizes the result into a natural language response for the user.

---

## 113. 1/Database_and_Storage/Generate SQL queries from schema only - AI-powered.txt

This workflow demonstrates a powerful security-conscious pattern where an AI agent can generate complex SQL queries based *only* on the database schema, without ever having access to the actual data within the database.

**Trigger:** The workflow has two parts: a one-time manual trigger for schema extraction and a `Chat Trigger` for generating queries.

**Functionality:**

**Part 1: Schema Extraction (Run Once)**

1.  **Connect to Database:** It connects to a MySQL database.
2.  **List Tables:** It executes `SHOW TABLES;` to get a list of all tables in the database.
3.  **Describe Tables:** It iterates through each table and runs `DESCRIBE {table_name};` to get the schema (column names, data types, keys, etc.) for each one.
4.  **Save Schema Locally:** The collected schema information for all tables is aggregated and saved as a single JSON file (`chinook_mysql.json`) in the n8n local file system.

**Part 2: AI-Powered Query Generation**

1.  **Chat Interface:** A user interacts with the system via a `Chat Trigger`, asking a question in natural language (e.g., "Can you show me the list of all German customers?").
2.  **Load Local Schema:** The workflow loads the `chinook_mysql.json` file that was saved in Part 1. This provides the necessary context for the AI.
3.  **AI Agent:** The user's request and the database schema are passed to a `Conversational Agent`. The agent's system prompt explicitly tells it that it **does not have a tool to run SQL** and that its job is to generate the query for the user to run.
4.  **Generate SQL:** The agent uses its knowledge of SQL and the provided schema to construct the correct query to answer the user's question.
5.  **Return Query:** The agent's final output is the raw SQL query, which is then displayed to the user in the chat interface. The user can then take this query and run it in their own database client.

---

## 114. 1/Database_and_Storage/MongoDB AI Agent - Intelligent Movie Recommendations.txt

This workflow creates an AI-powered movie recommendation agent that interacts with a MongoDB database. The agent can understand user preferences, query a movie database using MongoDB's aggregation framework, and save user favorites.

**Trigger:** The workflow is initiated by a `Chat Trigger`, allowing users to have a conversation about movies.

**Functionality:**

1.  **Conversational AI Agent:** The core is an `AI Agent` that takes the user's chat input. It uses an OpenAI chat model and maintains conversation history with a `Window Buffer Memory` node.
2.  **Tool: MongoDB Aggregation:**
    *   The agent's primary tool for finding movies is the `MongoDBAggregate` node.
    *   The agent is instructed to construct a MongoDB Aggregation pipeline based on the user's request (e.g., "find me a highly-rated Western movie from the 1960s").
    *   The agent passes this pipeline as a JSON query to the tool, which executes it against the `movies` collection in the MongoDB database.
3.  **Tool: Insert Favorites:**
    *   The agent is also equipped with a tool called `insertFavorites`, which is a separate n8n sub-workflow.
    *   When a user indicates they like a movie and want to save it, the agent calls this tool, passing the movie's title.
    *   The sub-workflow then handles the `insert` operation into a "favorites" collection in MongoDB.
4.  **Interaction Example:**
    *   **User:** "Can you recommend a classic sci-fi movie?"
    *   **Agent:** Constructs an aggregation pipeline like `[{"$match": {"genres": "Sci-Fi", "year": {"$lt": 1980}}}]`.
    *   **Agent:** Executes the pipeline using the `MongoDBAggregate` tool and returns a list of movies.
    *   **User:** "I like '2001: A Space Odyssey'. Add it to my favorites."
    *   **Agent:** Calls the `insertFavorites` tool with the title "2001: A Space Odyssey".

---

## 115. 1/Database_and_Storage/Supabase Insertion & Upsertion & Retrieval.txt

This workflow provides a complete guide to using Supabase as a vector store for a RAG (Retrieval-Augmented Generation) application. It covers all the essential operations: inserting new data, updating existing data (upserting), and retrieving data to answer questions.

**Trigger:** The workflow demonstrates three distinct operations, each triggered differently.

**Functionality:**

**Part 1: Preparation (in Supabase)**

*   The workflow notes require initial setup in the Supabase dashboard, including enabling the `pgvector` extension, creating a table with `embedding`, `metadata`, and `content` columns, and setting up a custom `match_documents` SQL function for efficient similarity searches.

**Part 2: Insertion**

1.  **Load Document:** It starts by loading a document (in this case, an `.epub` file from Google Drive).
2.  **Split Document:** The `Recursive Character Text Splitter` breaks the document down into smaller, manageable chunks of text.
3.  **Generate Embeddings:** Each text chunk is sent to an OpenAI embedding model (`text-embedding-3-small`) to create a vector representation.
4.  **Insert into Supabase:** The `Vector Store Supabase` node, in `insert` mode, takes the text chunks and their corresponding embeddings and inserts them as new rows into the designated Supabase table.

**Part 3: Upsertion (Updating)**

1.  **Get New Content:** A placeholder `Set` node represents the new or updated content to be added.
2.  **Generate Embeddings:** The new content is embedded using the same OpenAI model.
3.  **Update in Supabase:** The `Vector Store Supabase` node is used in `update` mode. It takes the new content, its embedding, and the ID of the record to be updated, and overwrites the existing entry in the database.

**Part 4: Retrieval (Q&A Chatbot)**

1.  **Chat Interface:** A `Chat Trigger` provides a user interface for asking questions about the document.
2.  **Query Embedding:** The user's question is sent to the OpenAI embedding model to create a query vector.
3.  **Similarity Search:** The `Vector Store Supabase` node (in its default retrieval mode) takes the query vector and uses the `match_documents` function in Supabase to find the most semantically similar text chunks from the database.
4.  **QA Chain:** The user's original question and the retrieved text chunks (the context) are passed to a `Question and Answer Chain`.
5.  **Generate Answer:** An OpenAI chat model within the chain synthesizes the information from the retrieved context to generate a final, accurate answer to the user's question.

---

## 116. 1/Database_and_Storage/Talk to your SQLite database with a LangChain AI Agent.txt

This workflow provides a powerful way to interact with a local SQLite database using natural language. It leverages a LangChain SQL Agent to translate user questions into SQL queries, execute them, and return understandable answers.

**Trigger:** The workflow has a one-time setup part and a conversational part. The setup is run manually, and the conversation is initiated via a `Chat Trigger`.

**Functionality:**

**Part 1: One-Time Database Setup**

1.  **Download Database:** It starts by downloading a sample SQLite database (`chinook.zip`) from an online tutorial.
2.  **Extract and Save:** It unzips the archive and saves the `chinook.db` file to the local n8n file system. This step only needs to be run once to make the database available to the workflow.

**Part 2: Conversational SQL Agent**

1.  **Chat Interface:** A user starts a conversation using the `Chat Trigger`.
2.  **Load Local Database:** On every chat message, the workflow first loads the `chinook.db` file from the local file system as binary data.
3.  **Combine Inputs:** The binary data of the database is combined with the user's chat input.
4.  **LangChain SQL Agent:** The combined data is passed to the `AI Agent` node, which is configured as a `sqlAgent`. This specialized agent is designed to interact with SQL databases.
5.  **Intelligent Querying:** The agent analyzes the user's question (e.g., "What are the revenues by genre?"). It can autonomously perform a series of actions:
    *   First, it queries the database schema to understand the tables and columns.
    *   Then, it constructs one or more SQL queries needed to answer the question.
    *   It executes these queries against the in-memory database.
6.  **Memory:** The agent is connected to a `Window Buffer Memory` node, allowing it to remember the context of the conversation for follow-up questions.
7.  **Final Answer:** After executing the necessary queries, the agent synthesizes the results into a final, human-readable answer and displays it in the chat.
## 117. 1/Discord/Discord AI-powered bot.txt

This workflow functions as an AI-powered triage bot for user feedback submitted via a Discord channel or interaction. It intelligently categorizes incoming messages and routes them to the correct department.

**Trigger:** The workflow can be triggered manually for testing or by a webhook, which would be connected to a Discord bot or slash command.

**Functionality:**

1.  **Receive Feedback:** A webhook receives the user's feedback text.
2.  **AI Categorization:** The feedback is sent to an OpenAI model (GPT-4). The AI is given a system prompt instructing it to act as a service desk agent and categorize the message into one of three categories:
    *   `success-story`: For positive feedback or praise.
    *   `urgent-issue`: For critical problems requiring immediate attention.
    *   `ticket`: For all other standard requests or issues.
3.  **Structured JSON Output:** The AI is prompted to return its analysis in a structured JSON format, including the determined `category`, the original `feedback`, and a polite `instruction` (a summary sentence) for the relevant department.
4.  **Parse Response:** A `Set` node parses the JSON string from the AI's response into a usable object.
5.  **Route to Department:** A `Switch` node reads the `category` from the parsed JSON and routes the workflow down the appropriate path.
6.  **Notify Departments on Discord:** Depending on the category, a message is sent to a specific Discord channel using a webhook URL:
    *   **Success Story:** Notifies the "User Success Dept" channel.
    *   **Urgent Issue:** Notifies the "IT Dept" channel.
    *   **Ticket:** Notifies the main "Helpdesk" channel.

---

## 118. 1/Discord/Send daily translated Calvin and Hobbes Comics to Discord.txt

This workflow automates the process of fetching the daily Calvin and Hobbes comic strip, translating its dialogue using AI, and posting it to a Discord channel.

**Trigger:** The workflow is designed to run daily on a `Schedule Trigger`, set for 9 AM.

**Functionality:**

1.  **Get Current Date:** A `Set` node captures the current year, month, and day to construct the correct URL.
2.  **Fetch Comic Page:** An `HTTPRequest` node fetches the HTML content from the gocomics.com URL for the current day's Calvin and Hobbes comic.
3.  **Extract Image URL:** An `Information Extractor` node with a specific prompt parses the HTML to find the `<img>` tag for the comic and extract its `src` URL.
4.  **AI Vision and Translation:** The extracted comic image URL is sent to the `OpenAI` node's image analysis endpoint (GPT-4o Mini). The AI is prompted to:
    *   Read the dialogue from the image.
    *   Translate the dialogue into a target language (in this case, Korean).
    *   Format the output to show the original English dialogue followed by the Korean translation for each line.
5.  **Post to Discord:** A `Discord` node sends a new message to a specified channel. The message includes the date, the comic image itself, and the translated text provided by the AI.

---

## 119. 1/Discord/Share YouTube Videos with AI Summaries on Discord.txt

This workflow monitors a specific YouTube channel for new videos and automatically shares them in a Discord channel along with a concise, AI-generated summary.

**Trigger:** The workflow uses an `RSS Feed Read Trigger` to poll the YouTube channel's video feed every minute.

**Functionality:**

1.  **New Video Detection:** The RSS trigger activates whenever a new video is published on the specified YouTube channel.
2.  **Retrieve Captions:** An `HTTPRequest` node calls the YouTube Data API to get a list of available captions for the new video, using its video ID.
3.  **Find English Captions:** A `Set` node uses a JMESPath expression to parse the API response and find the specific caption track where the language is English (`en`).
4.  **Download Caption File:** Another `HTTPRequest` node downloads the content of the English caption track.
5.  **Extract Text:** The `Extract from File` node converts the downloaded caption file (which is in a specific format) into plain text.
6.  **AI Summarization:** The plain text transcript is sent to an `OpenAI` node (GPT-3.5-Turbo). The AI is prompted to summarize the transcript into three bullet points that explain what the video is about and why someone should watch it.
7.  **Post to Discord:** A final `Discord` node sends a formatted message to a designated channel. The message includes the video title, the AI-generated summary, and a direct link to watch the video on YouTube.
## 120. 1/Forms_and_Surveys/Conversational Interviews with AI Agents and n8n Forms.txt

This workflow creates a dynamic and interactive conversational interview experience using an AI agent and n8n Forms. The AI acts as an interviewer, asking a continuous stream of relevant, open-ended questions on a given topic until the user decides to end the session.

**Trigger:** The workflow is initiated when a user fills out the first `n8n Form Trigger`.

**Functionality:**

1.  **Start Interview:** A user begins by submitting a form with their name. This action creates a new interview session, generating a unique session ID (UUID) and storing it in a Redis database to maintain the transcript.
2.  **Set Interview Topic:** The workflow defines the topic for the interview (e.g., "Your experience preparing for and taking the UK practical driving test").
3.  **AI Agent Interviewer:** The core of the workflow is an AI Agent. It receives the interview topic and the user's previous answer as context. Its primary instruction is to act as a researcher and ask the next logical, open-ended question.
4.  **Structured Response:** The agent is prompted to return its response in a structured JSON format, which includes the `question` to ask next and a boolean flag `stop_interview`.
5.  **Conversational Loop:**
    *   The AI generates a question.
    *   An `n8n Form` node displays this question to the user, with a text area for their answer.
    *   The user's answer is captured and sent back to the AI agent as context for the next turn.
    *   The question and answer pair are appended to the session transcript stored in Redis.
    *   This loop continues, with the AI generating new, context-aware questions each time.
6.  **Ending the Interview:**
    *   The AI is also instructed to analyze the user's answer for an intent to stop (e.g., if the user types "stop interview").
    *   If this intent is detected, the agent sets the `stop_interview` flag to `true`.
    *   An `If` node checks this flag. If true, the loop is broken.
7.  **Conclusion:** The workflow ends, and the session in Redis is cleared to prepare for the next interview. The full transcript is available in the Redis session data until it's cleared.

---

## 121. 1/Forms_and_Surveys/Email Subscription Service with n8n Forms, Airtable and AI.txt

This workflow creates a "learn something new every day" email subscription service. Users can sign up to receive facts about a topic of their choice at a specified frequency. The workflow handles both the user subscription and the scheduled sending of content.

**Trigger:** The workflow has two main triggers: an `n8n Form Trigger` for new subscriptions and a `Schedule Trigger` for sending the emails.

**Functionality:**

**Part 1: Subscription**

1.  **Subscription Form:** A user signs up via an n8n Form, providing their email, a topic of interest, and a desired frequency (daily, weekly, or surprise).
2.  **Save to Airtable:** The submitted information is saved as a new record in an Airtable base, which acts as the subscriber database. The record's status is set to 'active'.
3.  **Confirmation Email:** A confirmation email is sent to the user via Gmail to verify their subscription.

**Part 2: Content Generation and Sending**

1.  **Scheduled Run:** A `Schedule Trigger` runs daily.
2.  **Fetch Subscribers:** The workflow queries the Airtable base to find all subscribers whose `Status` is 'active' and whose `Interval` matches the current schedule (e.g., 'daily', or 'weekly' if it's the correct day).
3.  **Generate Content:** For each active subscriber, the workflow triggers a sub-workflow.
    *   The sub-workflow takes the subscriber's chosen `topic`.
    *   It uses an AI Agent to generate a "fun and interesting factoid" related to that topic.
4.  **Send Email:** The generated factoid is formatted into an HTML email.
5.  **Personalized Unsubscribe Link:** A unique unsubscribe link, containing the user's record ID from Airtable, is generated and included in the email footer.
6.  **Log Send Date:** After the email is sent, the workflow updates the "Last Sent" field in the user's Airtable record to the current timestamp.

**Part 3: Unsubscription**

1.  **Unsubscribe Form:** A separate n8n Form is used for unsubscribing. The user provides their ID (from the email link) and a reason.
2.  **Update Airtable:** The workflow finds the corresponding record in Airtable and updates its `Status` to 'inactive', effectively removing them from the mailing list.

---

## 122. 1/Forms_and_Surveys/Qualifying Appointment Requests with AI & n8n Forms.txt

This workflow creates a smart, multi-step appointment booking form that uses AI to pre-qualify inquiries before allowing a user to book a time slot.

**Trigger:** The workflow begins when a user submits the initial `n8n Form Trigger`.

**Functionality:**

1.  **Initial Inquiry:** A user fills out a form with their name, email, and a description of their inquiry.
2.  **AI Qualification:** The user's inquiry text is sent to an AI `Text Classifier`. The AI is trained to determine if the inquiry is a "Sales" or "Support" request.
    *   If the inquiry is classified as "Support" (or anything other than "Sales"), the workflow is routed to a completion screen that politely informs the user that a meeting is not necessary and provides an email address for support.
    *   If the inquiry is classified as "Sales", the user proceeds to the next step.
3.  **Terms and Conditions:** The user is presented with a non-negotiable terms and conditions page which they must accept to continue.
4.  **Date & Time Selection:** The user is then shown a form with dropdowns to select an available date and time for the appointment. The available dates are dynamically generated to show the next 5 non-weekend days.
5.  **Send Receipt to User:** Once a time is selected, a confirmation email is sent to the user, acknowledging their request and providing a summary.
6.  **Approval Process (Human-in-the-Loop):**
    *   A separate, parallel execution is triggered.
    *   The user's inquiry is first summarized by an AI model.
    *   An approval email is sent to an admin. This email contains the appointment details, the AI-generated summary, and two buttons: "Confirm" and "Decline".
    *   The workflow then pauses, waiting for the admin's response.
7.  **Final Action:**
    *   If the admin clicks **Confirm**, a new event is created in Google Calendar with a Google Meet link, and an invitation is sent to the user.
    *   If the admin clicks **Decline**, a polite rejection email is sent to the user.
## 123. 1/Gmail_and_Email_Automation/📈 Receive Daily Market News from FT.com to your Microsoft outlook inbox.txt

This workflow automates the creation and delivery of a daily financial news summary. It scrapes the Financial Times website, uses an AI to summarize the key stories, and sends the formatted summary to a Microsoft Outlook inbox.

**Trigger:** The workflow is activated daily at 7:00 AM by a `Schedule Trigger`.

**Functionality:**

1.  **Fetch News Page:** An `HTTPRequest` node fetches the main homepage of the Financial Times (ft.com).
2.  **Extract Content:** An `HTML` node uses a series of specific CSS selectors to parse the webpage and extract the text from key sections, such as "Top Stories," "Editor's Picks," "Spotlight," and various regional news categories.
3.  **Aggregate Content:** A `Set` node gathers all the extracted text snippets into a single, large text block.
4.  **AI Summarization:** The aggregated text is passed to an `AI Agent` powered by a Google Gemini chat model. The agent is prompted to act as a financial analyst and summarize all the news in a well-structured HTML format, suitable for an email body.
5.  **Send Email:** The final HTML summary generated by the AI is sent as an email via the `Microsoft Outlook` node to a pre-defined recipient.

---

## 124. 1/Gmail_and_Email_Automation/A Very Simple _Human in the Loop_ Email Response System Using AI and IMAP.txt

This workflow creates an AI-assisted email auto-responder that includes a crucial "human in the loop" step for approving drafted replies before they are sent.

**Trigger:** The workflow starts when a new email is received in a specified inbox, monitored by the `Email Trigger (IMAP)` node.

**Functionality:**

1.  **Summarize Incoming Email:** The HTML content of the new email is converted to markdown and then passed to a `Summarization Chain`. This uses an AI model to create a concise summary of the email's content.
2.  **Draft AI Reply:** The summary is then passed to an `AI Agent`. This agent is prompted to act as a professional email assistant and write a draft reply based on the summary. The agent is instructed to keep the reply under 100 words.
3.  **Send for Approval:** The AI-drafted reply, along with the original email content, is sent to an internal email address for review. This email, sent using the `Email Send` node's "sendAndWait" operation, contains "Approve" and "Reject" buttons. The workflow then pauses, awaiting human intervention.
4.  **Check Approval:** An `If` node checks the response from the approval email.
5.  **Send Final Email:** If the response was "Approved," the workflow proceeds to a final `Send Email` node, which sends the AI-drafted reply to the original sender. If rejected, the workflow simply stops.

---

## 125. 1/Gmail_and_Email_Automation/AI-powered email processing autoresponder and response approval (Yes_No).txt

This workflow automates handling incoming emails by summarizing them, generating a draft response using a RAG-enabled AI agent, and requiring human approval before sending.

**Trigger:** The workflow is triggered by a new email received via an `Email Trigger (IMAP)`.

**Functionality:**

1.  **Summarize Email:** The incoming email's HTML is converted to markdown and summarized by a `Summarization Chain` using a DeepSeek AI model.
2.  **Draft Reply with RAG:** The summary is passed to an `AI Agent`. This agent is equipped with a `Qdrant Vector Store` tool, allowing it to query a knowledge base for relevant information to include in its response. The agent then drafts a professional reply in HTML format.
3.  **Send for Approval:** The drafted reply is sent to a designated Gmail address for approval using the `Gmail` node's "sendAndWait" operation. This email includes "Yes" (Approve) and "No" (Reject) buttons.
4.  **Check Approval:** An `If` node checks if the response was "approved".
5.  **Send Final Email:** If approved, the final `Send Email` node sends the AI-drafted HTML response to the original sender. If not, the workflow terminates.

---

## 126. 1/Gmail_and_Email_Automation/Analyze & Sort Suspicious Email Contents with ChatGPT.txt

This workflow acts as an automated security tool to analyze incoming emails for potential phishing threats and log the findings in Jira.

**Trigger:** The workflow can be triggered by either a `Gmail Trigger` or a `Microsoft Outlook Trigger`, which monitor for new emails.

**Functionality:**

1.  **Variable Setup:** Once an email is received, a `Set` node extracts and standardizes key information, including the HTML body, text body, subject, recipient, and all message headers.
2.  **AI Analysis:** The HTML body and the full email headers are sent to an `OpenAI` node (ChatGPT-4o). The AI is prompted to:
    *   Analyze the content and headers.
    *   Determine if the email is likely malicious or benign.
    *   Provide a verbose summary of its findings, formatted for Jira's wiki-style renderer.
    *   Return the analysis in a structured JSON format with a boolean `malicious` flag and a `summary` string.
3.  **Conditional Ticket Creation:** An `If` node checks the `malicious` flag in the AI's response.
    *   If `true`, it creates a "Potentially Malicious" ticket in a Jira support project.
    *   If `false`, it creates a "Potentially Benign" ticket.
4.  **Attach Evidence:**
    *   The workflow uses the hcti.io API to generate a screenshot of the email's HTML body.
    *   The text body of the email is converted into a `.txt` file.
    *   Both the screenshot and the text file are uploaded as attachments to the newly created Jira ticket, providing full context for a human security analyst.

---

## 127. 1/Gmail_and_Email_Automation/Analyze Suspicious Email Contents with ChatGPT Vision.txt

This workflow is an enhanced version of the email analysis tool, leveraging an AI vision model to provide a more thorough assessment of potential phishing emails.

**Trigger:** The workflow can be triggered by either a `Gmail Trigger` or a `Microsoft Outlook Trigger`.

**Functionality:**

1.  **Variable Setup:** It extracts and standardizes key email information (HTML body, headers, subject, etc.).
2.  **Generate Email Screenshot:** It sends the email's HTML body to the hcti.io API, which renders the HTML and returns a URL for a screenshot of the email. The workflow then downloads this image.
3.  **AI Vision Analysis:** The downloaded screenshot image is sent to the `OpenAI` node, specifically using the GPT-4 Vision model. The prompt asks the AI to:
    *   Analyze the **image** of the email.
    *   Analyze the accompanying text-based **message headers**.
    *   Determine if the email is a phishing attempt based on both visual cues and header information.
4.  **Create Jira Ticket:** A Jira ticket is created with the title "Phishing Email Reported". The description includes the AI's full analysis.
5.  **Attach Evidence:** The screenshot of the email is uploaded as an attachment to the Jira ticket, allowing a human analyst to see exactly what the user saw.
## 128. 1/Gmail_and_Email_Automation/Auto Categorise Outlook Emails with AI.txt

This workflow automates the organization of an Outlook inbox by using a locally-run AI model to categorize incoming emails and move them to appropriate folders.

**Trigger:** The workflow can be triggered manually or on a schedule.

**Functionality:**

1.  **Fetch Unread Emails:** It uses the `Microsoft Outlook` node to get all unread emails from the Inbox.
2.  **Filter Uncategorized:** It filters the results to process only those emails that do not already have a category assigned.
3.  **Prepare Content:** For each email, it converts the HTML body to clean markdown text and then further processes it to remove extra whitespace and special characters, preparing it for the AI model.
4.  **AI Classification:** The cleaned email body and subject are passed to a locally-run `Ollama Chat Model`. The AI is prompted to act as an email assistant and classify the email into a primary `category` and a `subCategory` from a predefined list (e.g., Category: "SaaS", Sub-category: "n8n").
5.  **Parse AI Response:** The JSON output from the Ollama model is parsed to extract the determined category and sub-category.
6.  **Apply Categories and Move:**
    *   The workflow first calls the `Microsoft Outlook` node with the "update" operation to apply the new category labels to the email item in Outlook.
    *   A `Switch` node then routes the email based on its primary category.
    *   Finally, another `Microsoft Outlook` node uses the "move" operation to move the email into the corresponding folder (e.g., an email categorized as "SaaS" is moved to the "SaaS" folder).

---

## 129. 1/Gmail_and_Email_Automation/Auto-label incoming Gmail messages with AI nodes.txt

This workflow automates the process of labeling incoming Gmail messages based on their content, helping to keep the inbox organized.

**Trigger:** The workflow starts with a `Gmail Trigger` that checks for new mail every minute.

**Functionality:**

1.  **Get Message Content:** When a new email arrives, the workflow uses its message ID to fetch the full body content.
2.  **AI Label Assignment:** The email's text is passed to a `LangChain LLM Chain`. The AI model is given a specific prompt with a predefined list of categories ("Partnership", "Inquiry", "Notification") and is instructed to return the most appropriate label(s) in a JSON format.
3.  **Parse and Prepare Labels:**
    *   The JSON output from the AI is parsed.
    *   The workflow then gets a list of all available labels from the user's Gmail account.
    *   It merges the AI-assigned labels with the list of all labels to find the corresponding `label_id` for each assigned label name.
4.  **Apply Labels:** The collected `label_ids` are aggregated into an array and then passed to the `Gmail` node's "addLabels" operation, which applies the new labels to the original message in Gmail.

---

## 130. 1/Gmail_and_Email_Automation/Basic Automatic Gmail Email Labelling with OpenAI and Gmail API.txt

This workflow provides a more sophisticated method for automatically labeling Gmail messages. It uses an AI agent that can interact with the Gmail API to read existing labels, understand email content, and decide whether to use an existing label or create a new one.

**Trigger:** A `Gmail Trigger` polls for new emails every 5 minutes.

**Functionality:**

1.  **AI Agent with Gmail Tools:** The core of the workflow is an `AI Agent` that is equipped with a suite of `Gmail Tools`:
    *   `Gmail - read labels`: Allows the agent to get a list of all existing labels in the user's account.
    *   `Gmail - get message`: Allows the agent to read the full content of a specific email.
    *   `Gmail - create label`: Allows the agent to create a new label if a suitable one doesn't exist.
    *   `Gmail - add label to message`: Allows the agent to apply one or more labels to an email.
2.  **Intelligent Labeling Logic:** The agent is given a detailed system prompt that outlines its objective:
    *   Analyze an email's subject, sender, and content.
    *   Compare it against the list of existing labels to find the best match.
    *   If no suitable label exists, create a new one, attempting to nest it under an existing parent label if appropriate (e.g., creating `AI/New-Tool` if the `AI` label already exists).
    *   If an email is of low importance (e.g., promotion), it should be labeled and have the `INBOX` label removed.
3.  **Execution Flow:** When a new email arrives, the agent is triggered. It will then autonomously decide which tools to use in what order to achieve its goal. For example, it will likely first read the labels, then get the message content, decide on the correct label (or create a new one), and finally apply that label to the message.

---

## 131. 1/Gmail_and_Email_Automation/Classify lemlist replies using OpenAI and automate reply handling.txt

This workflow automates the management of replies from lemlist email outreach campaigns. It uses AI to classify the intent of a reply and then takes appropriate actions in both lemlist and Slack.

**Trigger:** The workflow starts when a new reply is received in a lemlist campaign, captured by the `Lemlist Trigger`.

**Functionality:**

1.  **Clean Email Text:** The incoming email reply text is cleaned up by converting it from HTML to markdown to make it easier for the AI to process.
2.  **AI Reply Classification:** The cleaned text is sent to an `OpenAI Chat Model`. The AI is prompted to classify the email into one of several categories: "Interested", "Out of office", "Unsubscribe", "Not interested", or "Other".
3.  **Route Based on Category:** A `Switch` node directs the workflow based on the category assigned by the AI.
4.  **Automated Actions:**
    *   **All Replies:** A notification is sent to a designated Slack channel (`#automated_outbound_replies`). This message includes the AI-assigned category, the campaign name, lead details, and a preview of the reply.
    *   **If "Unsubscribe":** The workflow calls the `lemlist` node to automatically unsubscribe the lead from the campaign.
    *   **If "Interested":** The workflow makes an HTTP request to the lemlist API to mark the lead as "interested", moving them to the next stage of the sales funnel.

---

## 132. 1/Gmail_and_Email_Automation/Compose reply draft in Gmail with OpenAI Assistant.txt

This workflow automates the creation of email reply drafts in Gmail. It uses a pre-configured OpenAI Assistant to generate context-aware replies and saves them directly into the relevant email thread.

**Trigger:** A `Schedule Trigger` runs the workflow at a set interval (e.g., every minute).

**Functionality:**

1.  **Find Trigger Emails:** The workflow searches Gmail for any email threads that have a specific, user-defined label (e.g., "AI-Draft-Reply").
2.  **Process Each Thread:** It loops through each found thread.
3.  **Get Last Message:** It retrieves all messages in the thread and isolates the content of the most recent one.
4.  **Query OpenAI Assistant:** The content of the last message is sent to a pre-configured `OpenAI Assistant`. The assistant is expected to be trained or prompted to handle specific types of replies (e.g., customer support, sales follow-ups).
5.  **Generate Draft:** The assistant generates a reply based on the email content.
6.  **Format and Encode:** The AI's response (in markdown) is converted to HTML. This HTML is then embedded into a raw RFC 822 formatted email string, which is finally encoded in base64.
7.  **Create Draft in Gmail:** An `HTTPRequest` node makes a call to the Gmail API's `drafts` endpoint, passing the base64-encoded raw message. This creates a new draft reply directly within the correct email thread in the user's Gmail account.
8.  **Clean Up:** The original trigger label is removed from the email thread to prevent it from being processed again in the next run.
## 128. 1/Gmail_and_Email_Automation/create e-mail responses with fastmail and OpenAI.txt

This workflow automates the process of drafting replies to emails in a Fastmail account. It uses an IMAP trigger to detect new emails and OpenAI's GPT-4 to generate a context-aware response, which is then saved as a draft in the user's Fastmail account.

**Trigger:** The workflow starts when a new, unread email is detected in the inbox via the `Email Trigger (IMAP)` node.

**Functionality:**

1.  **Extract Email Content:** When a new email arrives, the workflow extracts key details like the sender, subject, plain text body, and message-id.
2.  **Generate AI Response:** The subject and body of the email are sent to the `OpenAI` node. The AI is prompted to analyze the content and draft a casual, personalized reply, paying attention to the original email's language and level of formality.
3.  **Connect to Fastmail API:** The workflow authenticates with the Fastmail JMAP API to get a session and retrieve the list of all mailboxes.
4.  **Identify Drafts Folder:** It filters the list of mailboxes to find the specific ID of the "Drafts" folder.
5.  **Prepare and Upload Draft:**
    *   A `Set` node gathers all the necessary information for the draft: the recipient's address, the new subject line (prefixed with "Re:"), the AI-generated body, and the `message-id` of the original email to ensure the draft is part of the correct thread.
    *   An `HTTPRequest` node sends a `POST` request to the Fastmail JMAP API, using the `Email/set` method to create a new email draft with the prepared content and place it in the identified "Drafts" folder.

---

## 129. 1/Gmail_and_Email_Automation/Effortless Email Management with AI-Powered Summarization & Review.txt

This workflow provides a comprehensive, human-in-the-loop system for managing email responses. It uses AI to summarize incoming emails and draft replies with information from a knowledge base, then allows a human to review, edit, and approve the final message.

**Trigger:** The workflow is initiated by a new email received via the `Email Trigger (IMAP)`.

**Functionality:**

1.  **Summarize Incoming Email:** The new email's content is passed to a `Summarization Chain` to create a concise summary.
2.  **Draft Reply with RAG:** The summary is sent to an `AI Agent`. This agent is equipped with a `Qdrant Vector Store` tool, which it uses to retrieve relevant information from a company knowledge base. The agent then uses this retrieved context to draft a professional reply.
3.  **Human Review and Approval:**
    *   The AI-drafted reply, along with the original email, is sent to a designated reviewer via the `Gmail` node's "sendAndWait" operation.
    *   This special operation allows the reviewer to **reply directly to the approval email with edits**.
4.  **Classify Reviewer's Response:** The text of the reviewer's reply is sent to a `Text Classifier`. The AI determines if the response is an "Approved" message or a "Declined" one (which implies edits were made).
5.  **Send Final Email:**
    *   If the reply was classified as "Approved," the original AI-drafted email is sent.
    *   If it was "Declined," the **reviewer's edited text** is sent as the final email, allowing for seamless human correction.

---

## 130. 1/Gmail_and_Email_Automation/Email Summary Agent.txt

This workflow acts as a daily email briefing agent. It runs once a day, fetches all emails from the last 24 hours, uses AI to summarize them and extract action items, and then sends a neatly formatted report to a designated email address.

**Trigger:** A `Schedule Trigger` fires every day at 7 AM.

**Functionality:**

1.  **Fetch Emails:** The `Gmail` node is configured with a search query (`q`) to fetch all emails received in the last 24 hours.
2.  **Aggregate Data:** The workflow organizes the data from all fetched emails, extracting the ID, From, To, CC, and a snippet for each one. All the data is aggregated into a single item.
3.  **AI Summarization and Action Extraction:** The aggregated email data is sent to an `OpenAI` node (GPT-4o Mini). The AI is given a specific prompt to:
    *   Go through all the email snippets.
    *   Create a high-level summary of the day's communications.
    *   Identify and list out specific action items, assigning each action to a person if mentioned.
    *   Return the output in a structured JSON format containing a `summary_of_emails` array and an `actions` array.
4.  **Send HTML Report:** The structured JSON from the AI is used to populate a pre-formatted HTML email template. This report, which includes the summary points and the list of actions, is then sent via the `Gmail` node to a team email address or stakeholder.

---

## 131. 1/Gmail_and_Email_Automation/Extract spending history from gmail to google sheet.txt

This workflow automates personal expense tracking by extracting transaction details from emails and logging them in a Google Sheet.

**Trigger:** The workflow uses two `Gmail Trigger` nodes to monitor for new emails that have been assigned specific labels: one for "invoice" and one for "payment".

**Functionality:**

1.  **Get Email Content:** When a labeled email is detected, the workflow retrieves its content. If there is a PDF attachment (like an invoice), it extracts the text from the PDF. If not, it uses the email's HTML or plain text body.
2.  **Consolidate Data:** A `Switch` node routes the flow based on the trigger (invoice or payment), and `Set` nodes organize the email's date, subject, and full content into a standardized format.
3.  **AI-Powered Data Extraction:** The consolidated email content is passed to a `Google Gemini` chat model. The AI is prompted to act as a data entry specialist and parse the text to extract specific fields according to a detailed JSON schema. The schema includes:
    *   `date`: Transaction date.
    *   `service`: The name of the store or service.
    *   `details`: Any extra transaction details.
    *   `amount`: The transaction amount.
    *   `category`: The spending category (e.g., "Food & Beverage", "Transportation").
    *   `currency`: The currency code (e.g., "USD", "TWD").
    *   `card`: The payment card used.
4.  **Append to Google Sheets:** The structured JSON object returned by the AI is then passed to the `Google Sheets` node, which appends the extracted data as a new row in a designated expense tracking spreadsheet.

---

## 132. 1/Gmail_and_Email_Automation/Gmail AI Auto-Responder_ Create Draft Replies to incoming emails.txt

This workflow creates an intelligent auto-responder for Gmail that first determines if an email needs a reply and then, if necessary, drafts a response for the user to review.

**Trigger:** A `Gmail Trigger` checks for new incoming emails every minute, ignoring emails sent from the user themselves.

**Functionality:**

1.  **Assess Need for Reply:** The subject and body of the new email are passed to a `LangChain LLM Chain`. The AI model is prompted to assess if the message requires a response (e.g., it's not a marketing email or notification) and to return a simple JSON object: `{"needsReply": true}` or `{"needsReply": false}`.
2.  **Check Assessment:** An `If` node checks the `needsReply` boolean from the AI's response. If `false`, the workflow stops.
3.  **Generate Draft Reply:** If a reply is needed, the email content is passed to a second `LangChain LLM Chain`. This chain is prompted with more detailed instructions for the AI to act as a helpful personal assistant and draft a professional, concise reply. It is also instructed to provide two options (affirmative and negative) if the original email was a yes/no question.
4.  **Create Draft in Gmail:** The final drafted text from the AI is sent to the `Gmail` node, configured with the "Create Draft" operation. This creates a new draft reply within the original email's thread in the user's Gmail account, ready for them to review, edit, and send.
## 133. 1/Gmail_and_Email_Automation/Microsoft Outlook AI Email Assistant with contact support from Monday and Airtable.txt

This workflow functions as an advanced AI assistant for a Microsoft Outlook inbox, designed to automatically categorize emails based on predefined rules and contact lists sourced from a CRM (Monday.com) and a database (Airtable).

**Trigger:** The workflow can be triggered manually or on a schedule (e.g., every 15 minutes).

**Functionality:**

1.  **Contact Sync (Scheduled):** A separate scheduled part of the workflow periodically fetches contact information from a Monday.com board and upserts it into an Airtable base. This ensures the AI has an up-to-date list of known clients and suppliers.
2.  **Fetch Unread Emails:** The main workflow fetches recent, unread, and uncategorized emails from a specified Outlook folder.
3.  **Load Rules and Contacts:** It reads three separate tables from an Airtable base:
    *   **Categories:** A list of possible email categories and sub-categories.
    *   **Delete Rules:** A list of rules for identifying emails that can be immediately deleted (e.g., spam).
    *   **Contacts:** The synced list of known contacts from Monday.com.
4.  **AI Email Analysis:** For each new email, an `AI Agent` is invoked. It is provided with the email's content and the data from the three Airtable tables as context. The agent's system prompt instructs it to:
    *   Analyze the email's subject, body, and sender.
    *   Compare the sender against the known contacts list.
    *   Use the "Categories" rules to assign a primary category and an optional "Action" sub-category.
    *   Return the analysis in a structured JSON format.
5.  **Apply Category and Importance:**
    *   The workflow uses the `Microsoft Outlook` node to update the email with the category assigned by the AI.
    *   If the AI assigned the "Action" sub-category, another `Microsoft Outlook` node is used to flag the email with "High" importance.
6.  **Move to Folder:** Based on the primary category, a `Switch` node routes the email to be moved into the appropriate folder within Outlook (e.g., "SaaS", "Receipts", "Community").

---

## 134. 1/Gmail_and_Email_Automation/Modular & Customizable AI-Powered Email Routing_ Text Classifier for eCommerce.txt

This workflow provides a smart routing system for incoming customer inquiries from a website contact form. It uses AI to classify the message's intent and forwards it to the correct internal department.

**Trigger:** The workflow starts when a user submits a message through an `n8n Form Trigger`.

**Functionality:**

1.  **Receive Inquiry:** The form captures the user's name, email, and message.
2.  **AI Classification:** The user's message is sent to a `Text Classifier` node powered by an OpenAI model. The classifier is configured with a list of potential categories relevant to an eCommerce business, such as:
    *   Request Quote
    *   Product info
    *   General problem
    *   Order
3.  **Route to Department:** A `Switch` node evaluates the category returned by the AI.
4.  **Forward Email and Log Data:** Based on the category, the workflow takes two actions in parallel:
    *   **Email Forwarding:** An `Email Send` node forwards the original inquiry to the appropriate department's email address (e.g., `sales@example.com`, `support@example.com`).
    *   **Google Sheets Logging:** A `Google Sheets` node appends the details of the inquiry (name, email, message, and AI-assigned category) to a central spreadsheet for tracking and analysis.

---

## 135. 1/Gmail_and_Email_Automation/Send a ChatGPT email reply and save responses to Google Sheets.txt

This workflow automates the process of replying to specific emails using ChatGPT and meticulously logs the entire conversation in a Google Sheet for record-keeping.

**Trigger:** The workflow is triggered by a new email arriving in a Gmail inbox, monitored by the `Gmail Trigger`.

**Functionality:**

1.  **Filter by Recipient:** An `If` node checks if the email's sender is on a pre-approved list of recipients defined in a `Configure` node. This allows the user to control which emails the bot responds to.
2.  **Extract Reply:** A `Code` node uses a custom Email Parser library to intelligently extract only the most recent reply from the email thread, ignoring previous messages and signatures.
3.  **Generate AI Reply:** The extracted reply text is sent to an `OpenAI` node. The AI is prompted to generate a suitable response.
4.  **Send Reply:** The AI-generated text is sent as a reply in the original email thread using the `Gmail` node's "reply" operation.
5.  **Log to Google Sheets:**
    *   The workflow checks if a Google Sheet for logging has already been created (by checking for a stored `spreadsheetId` in the workflow's static data).
    *   If not, it creates a new Google Sheet with the specified name.
    *   It then appends a new row to the sheet containing the original message, the AI-generated reply, and a unique ID for the interaction. This creates a comprehensive log of all automated conversations.

---

## 136. 1/Gmail_and_Email_Automation/Send specific PDF attachments from Gmail to Google Drive using OpenAI.txt

This workflow automates the process of finding specific types of PDF attachments in incoming Gmail messages and uploading them to a designated Google Drive folder.

**Trigger:** A `Gmail Trigger` checks for new emails and downloads all attachments.

**Functionality:**

1.  **Iterate Attachments:** A `Code` node iterates through all the attachments of the incoming email, ensuring each is processed individually.
2.  **Filter for PDFs:** An `If` node checks the file extension of each attachment to ensure it is a `.pdf` file before proceeding.
3.  **Read PDF Content:** The `Read PDF` node extracts the text content from the PDF file.
4.  **AI Content Analysis:** The extracted text and the PDF's filename are sent to an `OpenAI` node. The AI is given a simple prompt to determine if the document matches a specific type, defined in a `Configure` node (e.g., "Is this a payslip?"). The AI is instructed to return only "true" or "false".
5.  **Conditional Upload:** An `If` node checks the AI's response.
    *   If the response is `true`, the workflow proceeds.
    *   The `Google Drive` node then uploads the original PDF file to a specific folder, the URL of which is also defined in the `Configure` node.

---

## 137. 1/Gmail_and_Email_Automation/Summarize your emails with A.I. (via Openrouter) and send to Line messenger.txt

This workflow provides a daily personal assistant that reads unread emails, summarizes them using an AI model, and sends the summary to the user via the LINE messaging app.

**Trigger:** The workflow is designed to be run on a schedule, but is shown with a manual `Read emails (IMAP)` trigger for demonstration.

**Functionality:**

1.  **Fetch Unread Emails:** The `Read emails (IMAP)` node connects to an email server and fetches all unread messages.
2.  **AI Summarization:** The workflow iterates through each email. The content of each email (sender, subject, and body) is sent to an AI model (Llama 3.1 70B) via the OpenRouter API. The prompt instructs the AI to:
    *   Summarize the email concisely.
    *   Keep the summary to a single sentence if the email is not important.
    *   Highlight any action items or deadlines, putting deadlines in bold at the top.
    *   Add an emoji to indicate urgency.
3.  **Push to LINE Messenger:** The formatted summary from the AI is then sent as a push notification to a specified user ID via the LINE Messaging API, using an `HTTPRequest` node.
---

## 138. 1/Google_Drive_and_Google_Sheets/✨ Vision-Based AI Agent Scraper - with Google Sheets, ScrapingBee, and Gemini.txt

**Workflow:** Vision-Based AI Agent Scraper - with Google Sheets, ScrapingBee, and Gemini

This workflow automates web scraping using a vision-based AI agent. It reads a list of URLs from a Google Sheet, captures a screenshot of each page using ScrapingBee, and then employs a Google Gemini-powered AI agent to extract structured data directly from the image. The extracted information is then saved back to a separate sheet in the same Google Sheet. The workflow includes a fallback mechanism to retrieve the page's HTML content for data extraction if the vision-based approach fails.

### Trigger

- **Type:** Manual
- **Details:** The workflow must be initiated manually by clicking the 'Test workflow' button.

### Workflow Steps

1.  **Google Sheets - Get URLs:** Retrieves a list of URLs to be scraped from a specified Google Sheet.
2.  **Set Fields:** Prepares the URL for the subsequent scraping and AI processing steps.
3.  **ScrapingBee - Get Screenshot:** Takes a full-page screenshot of the URL.
4.  **Vision-based Scraping Agent (Gemini):** An AI agent analyzes the screenshot to extract predefined data fields (e.g., product title, price, brand).
5.  **HTML-based Scraping Tool (Fallback):** If the vision agent fails, this tool is called to get the page's HTML content for the agent to re-analyze.
6.  **Structured Output Parser:** Formats the extracted data into a structured JSON object.
7.  **Split Out:** Splits the JSON array into individual items.
8.  **Google Sheets - Create Rows:** Appends the extracted data as new rows in the "Results" sheet of the Google Sheet.

---

## 139. 1/Google_Drive_and_Google_Sheets/Author and Publish Blog Posts From Google Sheets.txt

**Workflow:** Author and Publish Blog Posts From Google Sheets

This workflow automates the creation and publication of blog posts from a Google Sheet to a WordPress website. It can be triggered manually or on a schedule, using an OpenAI model to generate content based on topics and configurations defined in the sheet.

### Trigger

- **Type:** Manual or Schedule
- **Details:** Can be run on a recurring schedule (e.g., hourly) or triggered manually.

### Workflow Steps

1.  **Settings:** Defines configuration variables such as Google Sheet URLs, WordPress credentials, and action types.
2.  **Fetch Config:** Retrieves configuration parameters from a "Config" sheet.
3.  **Schedule:** Reads the content schedule from the "Schedule" sheet.
4.  **PreparedData:** For each row in the schedule, it prepares the data and constructs the appropriate prompt for the AI model based on the specified action (e.g., 'Idea', 'Draft', 'Final').
5.  **IfScheduledNow:** Checks if the post is scheduled for the current time.
6.  **AgentLLM (OpenAI):** Sends the prepared prompt to an OpenAI chat model to generate the blog post content.
7.  **RecombinedDataRow:** Processes the AI-generated output, normalizes it, and combines it with the existing row data.
8.  **SaveBackToSheet:** Updates the Google Sheet with the generated content and the new status.
9.  **IfPublish:** Checks if the action is to 'publish'.
10. **WordPress Post:** Publishes the final content to the configured WordPress site.
11. **Log:** Records the action taken in a "Log" sheet.

---

## 140. 1/Google_Drive_and_Google_Sheets/Automated End-to-End Fine-Tuning of OpenAI Models with Google Drive Integration.txt

**Workflow:** Automated End-to-End Fine-Tuning of OpenAI Models with Google Drive Integration

This workflow provides a complete pipeline for fine-tuning an OpenAI model using a dataset from Google Drive. It automates the process of uploading the data, creating the fine-tuning job, and making the newly trained model available for chat-based interaction.

### Trigger

- **Type:** Manual or Chat
- **Details:** The fine-tuning process is initiated manually. Once the model is trained, it can be used in a chat interface triggered by a user message.

### Workflow Steps

1.  **Google Drive Download:** Downloads a `.jsonl` training file from a specified Google Drive location.
2.  **Upload File (OpenAI):** Uploads the training file to OpenAI with the purpose set to `fine-tune`.
3.  **Create Fine-tuning Job:** Makes an HTTP request to the OpenAI API to start a new fine-tuning job using the uploaded file and a specified base model (e.g., `gpt-4o-mini-2024-07-18`).
4.  **Chat Trigger:** (Post-tuning) A chat trigger allows users to interact with the fine-tuned model.
5.  **AI Agent (OpenAI):** An AI agent powered by the newly fine-tuned model responds to user queries.

---

## 141. 1/Google_Drive_and_Google_Sheets/Automatic Background Removal for Images in Google Drive.txt

**Workflow:** Automatic Background Removal for Images in Google Drive

This workflow automates the process of removing backgrounds from images. It monitors a Google Drive folder for new image uploads, uses the Photoroom API to remove the background, and then saves the processed image to a different Google Drive folder.

### Trigger

- **Type:** Google Drive Trigger
- **Event:** `fileCreated`
- **Details:** The workflow starts whenever a new file is added to a specified folder in Google Drive.

### Workflow Steps

1.  **Watch for new images:** The Google Drive Trigger monitors a specific folder for new files.
2.  **Download Image:** Downloads the newly detected image file from Google Drive.
3.  **Get Image Size:** Extracts the dimensions of the image.
4.  **Config:** Sets configuration parameters such as background color, padding, output size, and the Photoroom API key.
5.  **check which output size method is used:** An IF node determines whether to use the original image size or a fixed output size.
6.  **remove background / remove background fixed size (Photoroom):** An HTTP request is sent to the Photoroom API with the image and configuration options to perform the background removal.
7.  **Upload Picture to Google Drive:** Uploads the resulting image (with a transparent or colored background) to a specified output folder in Google Drive.

---

## 142. 1/Google_Drive_and_Google_Sheets/Build an OpenAI Assistant with Google Drive Integration.txt

**Workflow:** Build an OpenAI Assistant with Google Drive Integration

This workflow creates a knowledgeable OpenAI Assistant that can answer questions based on the content of a document stored in Google Drive. It sets up the assistant, provides it with a knowledge file, and enables interaction through a chat interface.

### Trigger

- **Type:** Manual or Chat
- **Details:** The initial setup is triggered manually. Afterward, users can interact with the created assistant via a chat trigger.

### Workflow Steps

1.  **Create Assistant (OpenAI):** Creates a new OpenAI Assistant with a defined name, description, and system instructions.
2.  **Google Drive Download:** Downloads a document (e.g., PDF) from Google Drive to be used as the assistant's knowledge base.
3.  **Upload File (OpenAI):** Uploads the downloaded document to OpenAI with the purpose set to `assistants`.
4.  **Update Assistant (OpenAI):** Updates the assistant created in the first step by attaching the uploaded file's ID, making it part of the assistant's knowledge.
5.  **Chat Trigger:** Awaits user messages to start a conversation.
6.  **OpenAI Assistant Node:** Manages the conversation, sending the user's message to the specific assistant and returning its response.
7.  **Window Buffer Memory:** Maintains a memory of the conversation history to provide context for follow-up questions.
---

## 143. 1/Google_Drive_and_Google_Sheets/Chat with a Google Sheet using AI.txt

**Workflow:** Chat with a Google Sheet using AI

This workflow allows a user to "chat" with a Google Sheet. It uses an AI agent equipped with custom tools to query the sheet's data without needing to load the entire document into the context. The agent can list columns, retrieve specific rows, or get all values from a particular column, enabling complex data analysis through natural language queries.

### Trigger

- **Type:** Chat
- **Details:** The workflow is initiated by a user sending a message in the n8n chat interface.

### Workflow Steps

1.  **Chat Trigger:** Receives the user's query.
2.  **AI Agent (OpenAI):** An agent powered by `gpt-3.5-turbo-0125` receives the query. It is instructed to use a set of custom tools to explore the Google Sheet's data.
3.  **Custom Tools (Sub-workflow):**
    *   `list_columns`: Returns the names of all columns in the sheet.
    *   `column_values`: Fetches all values from a specified column.
    *   `get_customer`: Retrieves all data for a specific row number.
4.  **Sub-workflow Execution:** The agent calls the appropriate tool by triggering a sub-workflow.
    *   **Get Google Sheet Contents:** The sub-workflow reads the data from the specified Google Sheet.
    *   **Check Operation:** A Switch node routes the request based on the tool called (`column_names`, `column_values`, or `row`).
    *   **Data Preparation:** The data is filtered and formatted according to the operation.
    *   **Prepare Output:** The final result is formatted as a JSON string and returned to the agent.
5.  **Response Generation:** The agent uses the tool's output to formulate a final answer to the user's original query.

---

## 144. 1/Google_Drive_and_Google_Sheets/Chat with your event schedule from Google Sheets in Telegram.txt

**Workflow:** Chat with your event schedule from Google Sheets in Telegram

This workflow creates a Telegram bot that can answer questions about an event schedule stored in a Google Sheet. Users can interact with the bot via Telegram or the n8n chat interface to get information about meetups and events.

### Trigger

- **Type:** Telegram Message or n8n Chat
- **Details:** The workflow can be triggered by a new message sent to the Telegram bot or a message in the n8n chat.

### Workflow Steps

1.  **Input Trigger:** Receives a message from either Telegram or the n8n chat.
2.  **Settings:** Sets variables based on the input source (e.g., `chatId`, `inputMessage`).
3.  **Retrieve Schedule:** Fetches the event schedule from a Google Sheet.
4.  **ScheduleToMarkdown:** Converts the schedule data into a markdown table to be used as context for the AI.
5.  **ScheduleBot (AI Agent):** An AI agent, powered by an OpenRouter model, receives the user's question along with the markdown-formatted schedule as context.
6.  **Memory:** A Window Buffer Memory node maintains the conversation history for contextual understanding.
7.  **SetResponse:** Prepares the agent's final output message.
8.  **Switch:** Routes the response back to the correct platform (Telegram or n8n).
9.  **Send Response:** Sends the answer to the user via Telegram or displays it in the n8n chat.

---

## 145. 1/Google_Drive_and_Google_Sheets/Extract Information from a Logo Sheet using forms, AI, Google Sheet and Airtable.txt

**Workflow:** Extract Information from a Logo Sheet using forms, AI, Google Sheet and Airtable

This workflow automates the extraction of information from an image containing multiple logos (a "logo sheet"). It uses an AI vision model to identify tools, their attributes, and their relationships, and then stores this structured data in an Airtable base.

### Trigger

- **Type:** n8n Form
- **Details:** A user submits an image of a logo sheet and an optional additional prompt through a web form.

### Workflow Steps

1.  **On form submission:** Receives the logo sheet image and any additional text prompt.
2.  **Retrieve and Parser Agent (AI):** An AI agent with vision capabilities analyzes the image. It is prompted to extract the name of each tool, its attributes (categories, features), and any similar tools shown in the image, outputting the result as a structured JSON.
3.  **JSON it & Split Out Tools:** The JSON output from the agent is parsed and split into individual items, one for each tool identified.
4.  **Attribute Creation & Mapping:**
    *   The workflow loops through the attributes of each tool.
    *   It uses an `Upsert` operation to create new records for any attributes that don't already exist in the "Attributes" table in Airtable.
    *   It then maps the string-based attributes from the AI's output to their corresponding Airtable Record IDs.
5.  **Tool Creation & Linking:**
    *   A unique hash is generated for each tool name to prevent duplicates.
    *   It performs an `Upsert` operation in the "Tools" table in Airtable, creating a new record if the tool doesn't exist.
    *   Finally, it updates the tool's record, linking it to the newly created/mapped attribute records.

---

## 146. 1/Google_Drive_and_Google_Sheets/Flux Dev Image Generation (Fal.ai) to Google Drive.txt

**Workflow:** Flux Dev Image Generation (Fal.ai) to Google Drive

This workflow generates images based on a text prompt using the Fal.ai Flux Dev API and saves the resulting image to Google Drive.

### Trigger

- **Type:** Manual
- **Details:** The workflow is started manually.

### Workflow Steps

1.  **Edit Fields:** Sets the parameters for the image generation, including the prompt, width, height, steps, and guidance scale.
2.  **Fal Flux (API Request):** Sends a POST request to the Fal.ai API with the specified parameters to initiate the image generation process.
3.  **Wait & Check Status Loop:**
    *   The workflow waits for 3 seconds.
    *   It then sends a request to the Fal.ai API to check the status of the generation job.
    *   An IF node checks if the status is "COMPLETED". If not, it loops back to the wait step.
4.  **Get Image Result URL:** Once the job is complete, it retrieves the URL of the generated image.
5.  **Download Image:** Downloads the image from the result URL.
6.  **Google Drive Upload:** Uploads the downloaded image file to a specified folder in Google Drive.

---

## 147. 1/Google_Drive_and_Google_Sheets/Qualify new leads in Google Sheets via OpenAI_s GPT-4.txt

**Workflow:** Qualify new leads in Google Sheets via OpenAI's GPT-4

This workflow automates the process of qualifying new leads that are added to a Google Sheet. It uses OpenAI's GPT-4 to analyze each new lead based on predefined criteria and then updates the sheet with the qualification status.

### Trigger

- **Type:** Google Sheets Trigger
- **Event:** `rowAdded`
- **Details:** The workflow is triggered whenever a new row is added to the specified Google Sheet.

### Workflow Steps

1.  **Check for new entries:** The Google Sheets trigger detects a new row (a new lead).
2.  **Qualify leads with GPT (OpenAI):** The lead's information (name, email, business area, team size) is sent to the OpenAI GPT-4 model. The model is given a system prompt with instructions to qualify the lead based on whether they are a decision-maker and have a corporate email domain.
3.  **Extract JSON reply:** The model is instructed to reply with a JSON object containing a "rating" (`qualified` or `not qualified`) and an "explanation". This node parses the JSON string from the AI's response.
4.  **Merge:** The original lead data from the Google Sheet is combined with the qualification data from OpenAI.
5.  **Update lead status:** The workflow updates the original row in the Google Sheet, adding the qualification rating to a "Rating" column.
---

## 148. 1/Google_Drive_and_Google_Sheets/RAG Chatbot for Company Documents using Google Drive and Gemini.txt

**Workflow:** RAG Chatbot for Company Documents using Google Drive and Gemini

This workflow creates a Retrieval-Augmented Generation (RAG) system that keeps a Pinecone vector store synchronized with documents in a Google Drive folder. It then provides a chat interface for users to ask questions about the documents. The system is designed to function as an HR assistant, answering employee questions based on company policies.

### Trigger

- **Type:** Google Drive Trigger (File Created/Updated) or Chat
- **Details:** The data ingestion pipeline is triggered when a file is created or updated in a specific Google Drive folder. The chatbot is triggered when a user sends a message.

### Workflow Steps

**Data Ingestion (on file change):**
1.  **Google Drive Trigger:** Monitors a folder for new or updated files.
2.  **Download File:** Downloads the file from Google Drive.
3.  **Text Splitter:** Uses a Recursive Character Text Splitter to break the document into chunks.
4.  **Embeddings (Google Gemini):** Converts the text chunks into vector embeddings using the `models/text-embedding-004` model.
5.  **Pinecone Insert:** Inserts the generated embeddings into a Pinecone index named `company-files`.

**Chat Interaction:**
1.  **Chat Trigger:** Receives a question from a user.
2.  **AI Agent (Google Gemini):** An agent powered by a Gemini chat model receives the question. It is instructed to use a custom tool to find answers in the company documents.
3.  **Vector Store Tool:** A tool named `company_documents_tool` is defined to query the Pinecone vector store.
4.  **Pinecone Retrieval:** The tool retrieves relevant document chunks from the `company-files` index based on the user's query.
5.  **Response Generation:** The AI agent uses the retrieved information to formulate an answer and sends it back to the user.

---

## 149. 1/Google_Drive_and_Google_Sheets/RAG_Context-Aware Chunking _ Google Drive to Pinecone via OpenRouter & Gemini.txt

**Workflow:** RAG: Context-Aware Chunking | Google Drive to Pinecone via OpenRouter & Gemini

This workflow implements an advanced Retrieval-Augmented Generation (RAG) pipeline that uses a context-aware chunking strategy. Instead of simply splitting a document into fixed-size chunks, it first uses an AI agent to generate a succinct context for each section of the document. This context is then prepended to the section itself before being embedded and stored in Pinecone, aiming to improve search retrieval accuracy.

### Trigger

- **Type:** Manual
- **Details:** The workflow is initiated manually.

### Workflow Steps

1.  **Get Document:** Downloads a document from Google Drive and extracts its text content.
2.  **Split Into Sections:** A Code node splits the document into logical sections based on a custom separator (`[SECTIONEND]`).
3.  **Loop Over Sections:** The workflow iterates through each section of the document.
4.  **AI Agent - Prepare Context:** For each section, an AI Agent (powered by an OpenRouter model) is prompted to generate a short, succinct context that situates the chunk within the overall document.
5.  **Concatenate Context and Section:** The AI-generated context is prepended to the original section text.
6.  **Embeddings (Google Gemini):** The combined text (context + section) is converted into vector embeddings using the `models/text-embedding-004` model.
7.  **Pinecone Insert:** The resulting embedding is inserted into a Pinecone vector store.

---

## 150. 1/Google_Drive_and_Google_Sheets/Screen Applicants With AI, notify HR and save them in a Google Sheet.txt

**Workflow:** Screen Applicants With AI, notify HR and save them in a Google Sheet

This workflow automates the initial screening process for job applications. It takes applicant information and a CV submitted through an n8n Form, uses a Google Gemini model to analyze the CV against a job description, and then notifies the HR department, sends a confirmation to the applicant, and logs the details in a Google Sheet.

### Trigger

- **Type:** n8n Form
- **Details:** The workflow starts when a candidate submits their application through a web form.

### Workflow Steps

1.  **Application Form:** Collects the applicant's full name, email, salary expectation, LinkedIn profile, and CV (as a PDF).
2.  **Extract PDF Text:** Extracts the text content from the submitted CV.
3.  **AI Analysis & Rating (Google Gemini):** A Google Gemini chat model analyzes the CV text against a predefined job description ("Software Engineer"). It provides a compatibility rating (1-10) and a recommendation on whether to proceed with an interview.
4.  **Save to Google Sheets:** Appends the applicant's details, along with the AI's rating and recommendation, to a "Candidate Lists" Google Sheet.
5.  **Inform HR:** Sends an email to the HR department with the new candidate's details and the AI's analysis.
6.  **Send Confirmation:** Sends a confirmation email to the applicant, acknowledging receipt of their CV.

---

## 151. 1/Google_Drive_and_Google_Sheets/Simple Expense Tracker with n8n Chat, AI Agent and Google Sheets.txt

**Workflow:** Simple Expense Tracker with n8n Chat, AI Agent and Google Sheets

This workflow provides a conversational interface for tracking expenses. A user can enter an expense in natural language (e.g., "car wash; 59.3 usd; 25 jan 2024") via the n8n chat. An AI agent then parses the message, extracts structured data, and saves it to a Google Sheet.

### Trigger

- **Type:** n8n Chat
- **Details:** The workflow is initiated when a user sends a message in the n8n chat interface.

### Workflow Steps

1.  **When chat message received:** The user's expense message is received.
2.  **AI Agent (OpenAI):** A primary AI agent receives the message and is instructed to use a tool to save the expense.
3.  **Parse and Save Tool (Sub-workflow):** The agent calls a sub-workflow to handle the data processing.
    *   **Workflow Input Trigger:** The sub-workflow receives the raw expense message.
    *   **Information Extractor (OpenAI):** An OpenAI model parses the unstructured text and extracts the `cost`, `description`, and `date` into a structured JSON format.
    *   **Save to Google Sheets:** The extracted, structured data is appended as a new row to an "ai-expense" Google Sheet.
4.  **Response to User:** The primary AI agent confirms to the user that the expense has been saved and returns the structured data that was logged.

---

## 152. 1/Google_Drive_and_Google_Sheets/Summarize Google Sheets form feedback via OpenAI_s GPT-4.txt

**Workflow:** Summarize Google Sheets form feedback via OpenAI's GPT-4

This workflow automates the summarization of feedback collected in a Google Sheet from a form. It aggregates all responses, sends them to OpenAI's GPT-4 for analysis, and then emails the formatted summary report.

### Trigger

- **Type:** Manual
- **Details:** The workflow is designed to be run manually to generate a summary report on demand.

### Workflow Steps

1.  **Get Google Sheets records:** Retrieves all rows from a Google Sheet containing form responses.
2.  **Aggregate responses into arrays:** The Aggregate node groups all the answers for each question into separate arrays.
3.  **Summarize via GPT model (OpenAI):** The aggregated feedback is sent to the GPT-4 model. The prompt instructs the AI to analyze the responses for three questions ("What went great?", "How can we improve?", "Chance of recommending"), identify the overall sentiment, and provide a summary report in Markdown format.
4.  **Convert from Markdown to HTML:** The Markdown-formatted summary from the AI is converted into HTML.
5.  **Send via Gmail:** The HTML report is sent as the body of an email to a predefined address.
---

## 153. 1/Google_Drive_and_Google_Sheets/Summarize the New Documents from Google Drive and Save Summary in Google Sheet.txt

**Workflow:** Summarize the New Documents from Google Drive and Save Summary in Google Sheet

This workflow automates the process of summarizing new documents added to a Google Drive folder. It triggers when a new file is created, retrieves the document's content, uses an OpenAI model to generate a summary, and then saves the summary along with metadata to a Google Sheet.

### Trigger

- **Type:** Google Drive Trigger
- **Event:** `fileCreated`
- **Details:** The workflow starts when a new file is added to a specific folder in Google Drive.

### Workflow Steps

1.  **Google Drive Trigger:** Detects a new file in the designated "yashdata" folder.
2.  **Get Document Content:** Retrieves the full content of the newly created Google Doc.
3.  **Generate Summary AI (OpenAI):** An OpenAI model (`gpt-4o-mini`) receives the document's content and is prompted to summarize it. The agent is also equipped with Calculator and Wikipedia tools, although they are not used in the main flow.
4.  **Store Summary in Sheet:** Appends a new row to the "Docs Summarise Data" Google Sheet containing the name and email of the user who last modified the document, and the AI-generated summary.

---

## 154. 1/Google_Drive_and_Google_Sheets/Upload to Instagram and Tiktok from Google Drive.txt

**Workflow:** Upload to Instagram and Tiktok from Google Drive

This workflow automates the process of posting videos to Instagram and TikTok. It watches a Google Drive folder for new video files, uses OpenAI to generate a suitable description, and then uploads the video and description to both platforms via the `upload-post.com` API.

### Trigger

- **Type:** Google Drive Trigger
- **Event:** `fileCreated`
- **Details:** The workflow is initiated when a new video file is uploaded to a specific folder in Google Drive.

### Workflow Steps

1.  **Google Drive Trigger:** Detects a new file in the "Influencersde" folder.
2.  **Download Video:** Downloads the video file from Google Drive.
3.  **Save and Read Video:** The video is temporarily saved to the local filesystem and then read back as a binary file.
4.  **Get Audio from Video (OpenAI):** The audio track is transcribed from the video using OpenAI's Whisper model.
5.  **Generate Description (OpenAI):** The transcribed audio text is sent to the GPT-4o model. The model is prompted to create an engaging social media title and description based on the audio content.
6.  **Upload to Tiktok:** An HTTP request is sent to the `upload-post.com` API to upload the video and the generated description to TikTok.
7.  **Upload to Instagram:** A second HTTP request is sent to the `upload-post.com` API to upload the same video and description to Instagram.
8.  **Error Handling:** If any step fails, an error trigger sends a notification to a Telegram chat.
---

## 155. 1/HR_and_Recruitment/BambooHR AI-Powered Company Policies and Benefits Chatbot.txt

**Workflow:** BambooHR AI-Powered Company Policies and Benefits Chatbot

This workflow creates an AI-powered chatbot that can answer employee questions about company policies and benefits. It retrieves policy documents from BambooHR, loads them into a Supabase vector store, and uses an OpenAI-powered agent to interact with users and query the data. It also includes an optional tool to look up employee details.

### Trigger

- **Type:** Manual (for data loading) and Chat (for interaction)
- **Details:** The initial loading of documents is triggered manually. The chatbot is then available to answer questions via a chat interface.

### Workflow Steps

**Data Ingestion:**
1.  **GET all files (BambooHR):** Retrieves all files from the company's BambooHR account.
2.  **Filter Files:** Filters the files to include only those from the "Company Files" category and that are PDFs.
3.  **Download File (BambooHR):** Downloads each filtered policy document.
4.  **Text Splitter & Embeddings:** The text from each document is split into chunks and converted into vector embeddings using OpenAI.
5.  **Vector Store Insert (Supabase):** The embeddings are stored in a Supabase vector store in a table named `company_files`.

**Chat Interaction:**
1.  **Chat Trigger:** A user asks a question in the chat.
2.  **AI Agent (OpenAI):** An agent receives the query and uses specialized tools to find the answer.
3.  **Company Files Tool:** A vector store tool that queries the Supabase index to find relevant policy information.
4.  **Employee Lookup Tool (Optional):** A workflow tool that can be called to retrieve details about a specific employee or department from BambooHR.
5.  **Response Generation:** The agent synthesizes the information from the tools to provide a comprehensive answer to the user.

---

## 156. 1/HR_and_Recruitment/CV Screening with OpenAI.txt

**Workflow:** CV Screening with OpenAI

This workflow automates the initial screening of a CV against a job description. It takes a URL to a CV, extracts the text, and sends it to OpenAI for a detailed analysis, including a matching score and a summary of the candidate's suitability.

### Trigger

- **Type:** Manual
- **Details:** The workflow is initiated manually.

### Workflow Steps

1.  **Set Variables:** Defines the direct URL to the candidate's CV, the full job description, a system prompt for the AI, and the desired JSON schema for the output.
2.  **Download File:** An HTTP Request node fetches the CV from the provided URL.
3.  **Extract Document PDF:** Extracts the text content from the downloaded PDF.
4.  **OpenAI - Analyze CV:** Sends the extracted CV text and the job description to the OpenAI API (`gpt-4o-mini`). The prompt instructs the AI to act as a strict recruiter and provide a percentage match, a short summary, and lists of reasons why the candidate does and does not suit the role. The `response_format` is set to `json_schema` to ensure a structured output.
5.  **Parsed JSON:** The structured JSON response from OpenAI is parsed for further use.

---

## 157. 1/HR_and_Recruitment/HR & IT Helpdesk Chatbot with Audio Transcription.txt

**Workflow:** HR & IT Helpdesk Chatbot with Audio Transcription

This workflow creates a multi-modal HR and IT helpdesk chatbot that can respond to both text and voice queries via Telegram. It uses a PostgreSQL vector store as its knowledge base, populated with company policy documents.

### Trigger

- **Type:** Telegram Message
- **Details:** The workflow starts when a user sends a text or voice message to the configured Telegram bot.

### Workflow Steps

**Data Ingestion (Manual Setup):**
1.  **HTTP Request:** Downloads a company handbook PDF from a URL.
2.  **Extract from File:** Extracts the text content from the PDF.
3.  **Vector Store Creation (PostgreSQL):** The extracted text is chunked, converted to OpenAI embeddings, and inserted into a PGVector table in a PostgreSQL database.

**Chat Interaction:**
1.  **Telegram Trigger:** Receives an incoming message.
2.  **Verify Message Type:** A Switch node checks if the message is text or voice.
3.  **Handle Voice Message:**
    *   If it's a voice message, the audio file is downloaded from Telegram.
    *   The audio is sent to OpenAI's Whisper model for transcription.
    *   The resulting text proceeds to the AI Agent.
4.  **Handle Text Message:** The text message is passed directly to the AI Agent.
5.  **AI Agent (OpenAI):** An agent receives the user's query (either as original text or transcribed audio).
6.  **Vector Store Tool:** The agent uses a tool connected to the PostgreSQL vector store to retrieve relevant policy information.
7.  **Postgres Chat Memory:** The conversation history is maintained in a PostgreSQL table to allow for follow-up questions.
8.  **Response Generation & Delivery:** The agent formulates a response based on the retrieved context and sends it back to the user on Telegram.

---

## 158. 1/HR_and_Recruitment/HR Job Posting and Evaluation with AI.txt

**Workflow:** HR Job Posting and Evaluation with AI

This comprehensive workflow automates the entire initial phase of the hiring process. It starts with a job application submitted via an n8n Form, uploads the CV to Google Drive, saves applicant details to Airtable, uses AI to evaluate the CV against the job description, and finally updates the Airtable record with the AI's evaluation.

### Trigger

- **Type:** n8n Form
- **Details:** A candidate applies for a job by filling out a form that includes their personal details and CV.

### Workflow Steps

1.  **On form submission:** Captures the applicant's first name, last name, email, phone, years of experience, and CV file. The form description itself contains the full job description for the "Automation Specialist" role.
2.  **Upload CV to Google Drive:** The submitted CV (PDF) is uploaded to a designated folder in Google Drive.
3.  **Applicant Details:** A Set node structures the applicant's information and retrieves the public web view link for the uploaded CV.
4.  **Create Airtable Record:** A new record for the applicant is created in an Airtable "Simple applicant tracker" base with their details.
5.  **Download CV for Analysis:** The CV is downloaded from Google Drive.
6.  **Extract PDF Text:** The text content is extracted from the CV.
7.  **AI Evaluation (OpenAI):** The extracted CV text is sent to an OpenAI model. The prompt instructs the AI to compare the CV against the job description (from the form node) and provide a score (0-4), a summary, and reasons for/against hiring.
8.  **Update Airtable Record:** The Airtable record created in step 4 is updated with the AI-generated score and evaluation notes.
---

## 159. 1/Instagram_Twitter_Social_Media/AI agent for Instagram DM_inbox. Manychat + Open AI integration.txt

**Workflow:** AI agent for Instagram DM/inbox. Manychat + Open AI integration

This workflow creates an AI-powered chatbot for responding to Instagram Direct Messages. It uses ManyChat to handle the connection with Instagram, while n8n processes the incoming messages, generates a response using an OpenAI model, and sends it back.

### Trigger

- **Type:** Webhook
- **Details:** Receives a POST request from a ManyChat flow whenever a new message is sent to the connected Instagram account.

### Workflow Steps

1.  **Getting message from Instagram:** A webhook node listens for incoming messages forwarded from ManyChat. The message content and session ID are passed in the request body.
2.  **Set your system prompt for AI:** A Set node defines the persona and task for the AI. The default prompt instructs the AI to act as an Instagram influencer and answer questions based on the style of their previous posts.
3.  **AI Agent (OpenAI):** An AI agent, powered by a ChatGPT model, receives the user's message and the system prompt.
4.  **Local n8n memory:** A Window Buffer Memory node keeps track of the last 20 messages in the conversation to provide context for follow-up questions.
5.  **Send respond:** The AI-generated response is sent back to the initial webhook, which forwards it to ManyChat to be delivered to the user on Instagram.

---

## 160. 1/Instagram_Twitter_Social_Media/Create dynamic Twitter profile banner.txt

**Workflow:** Create dynamic Twitter profile banner

This workflow dynamically updates a Twitter profile banner to display the profile pictures of the three most recent followers.

### Trigger

- **Type:** Manual
- **Details:** The workflow must be started manually.

### Workflow Steps

1.  **Fetch new followers:** Makes an API call to the Twitter API to get the three most recent followers, requesting their profile image URLs.
2.  **Item Lists:** Splits the list of followers into individual items.
3.  **Image Processing Loop:** For each follower:
    *   **Fetching images:** Downloads the follower's profile picture.
    *   **Resize:** Resizes the image to 200x200 pixels.
    *   **Crop:** Crops the image into a circle.
    *   **Resize1:** Resizes the final circular icon to 75x75 pixels.
4.  **Function:** Combines the three processed follower icons into a single item with binary data properties (`data0`, `data1`, `data2`).
5.  **Fetch bg:** Downloads a predefined template image for the banner background.
6.  **Merge:** Combines the background image with the three follower icons.
7.  **Edit Image:** Composites the three follower icons onto the background banner image at specific coordinates.
8.  **HTTP Request (Update Banner):** Makes an authenticated POST request to the Twitter API to upload and set the newly generated image as the profile banner.

---

## 161. 1/Instagram_Twitter_Social_Media/Generate Instagram Content from Top Trends with AI Image Generation.txt

**Workflow:** Generate Instagram Content from Top Trends with AI Image Generation

This workflow automates the creation and posting of Instagram content by identifying top trending posts for specific hashtags, generating new images inspired by those trends using AI, and then uploading the new content.

### Trigger

- **Type:** Schedule (Cron)
- **Details:** The workflow is scheduled to run twice a day at 13:05 and 19:05.

### Workflow Steps

1.  **Get Top Trends:** Two HTTP Request nodes fetch the top trending posts from Instagram for the hashtags `#blender3d` and `#isometric` using the `instagram-scraper-api2` on RapidAPI.
2.  **Filter and Merge:** The results are filtered to include only images (no videos), and the data from both hashtags is merged.
3.  **Loop Over Items:** The workflow iterates through each trending post.
4.  **Check if Data Exists:** A PostgreSQL node checks if the post has already been processed by looking up its `content_code` in a `top_trends` table.
5.  **Generate Image (Replicate):** If the post is new, it calls the Replicate API to generate a new image. The prompt for the new image is taken from the caption of the trending Instagram post.
6.  **Upload to Instagram:**
    *   The workflow waits for the image generation to complete.
    *   It then uses the Instagram API to upload the newly generated image along with the original caption.
7.  **Save to Database:** The `content_code` of the processed post is saved to the PostgreSQL database to prevent reprocessing.
8.  **Notifications:** The workflow sends notifications to a Telegram chat to confirm successful posts or report errors.

---

## 162. 1/Instagram_Twitter_Social_Media/OpenAI-powered tweet generator.txt

**Workflow:** OpenAI-powered tweet generator

This workflow automates the generation of tweets. It randomly selects a hashtag from a predefined list, uses OpenAI to generate a tweet about that hashtag, and then saves the result to an Airtable base.

### Trigger

- **Type:** Manual
- **Details:** The workflow is initiated by clicking the 'execute' button.

### Workflow Steps

1.  **FunctionItem:** A Function node randomly selects a hashtag from a hardcoded array (e.g., `#techtwitter`, `#n8n`).
2.  **HTTP Request (OpenAI):** Sends a request to the OpenAI Completions API (`text-davinci-001` model). The prompt asks the AI to generate a tweet under 100 characters that includes the randomly selected hashtag.
3.  **Set:** Extracts the generated tweet content and the hashtag into a structured format.
4.  **Airtable:** Appends the hashtag and the generated tweet content as a new record to a table named "main" in an Airtable base.

---

## 163. 1/Instagram_Twitter_Social_Media/Post New YouTube Videos to X.txt

**Workflow:** Post New YouTube Videos to X

This workflow automates the promotion of new YouTube videos on X (formerly Twitter). It periodically checks a YouTube channel for new videos, uses AI to generate a promotional post, and then posts it to a connected X account.

### Trigger

- **Type:** Schedule
- **Details:** The workflow runs every 30 minutes.

### Workflow Steps

1.  **Check Every 30 Min:** The schedule trigger initiates the workflow.
2.  **Fetch Latest Videos:** A YouTube node checks a specified channel for any videos published in the last 30 minutes.
3.  **Generate Post for X with ChatGPT:** If a new video is found, its title and description are sent to an OpenAI model (`gpt-3.5-turbo`). The prompt instructs the AI to write an engaging post for X, no more than 140 characters, including a link to the video.
4.  **Post to X:** The generated text is posted as a new tweet to the configured X account.
---

## 164. 1/Instagram_Twitter_Social_Media/Reddit AI digest.txt

**Workflow:** Reddit AI digest

This workflow searches Reddit for posts containing the keyword "n8n", filters them for relevance, uses OpenAI to classify if they are genuinely about the n8n.io tool, and then generates a summary for the relevant posts.

### Trigger

- **Type:** Manual
- **Details:** The workflow is initiated manually.

### Workflow Steps

1.  **Reddit Search:** Searches all of Reddit for posts containing the keyword "n8n", sorted by "new".
2.  **Filter Posts:** An IF node filters the results to include only posts from the last 7 days with 5 or more upvotes and that are not empty.
3.  **Set:** Trims the post's selftext to the first 500 characters and formats other relevant data like upvotes, subreddit size, and date.
4.  **OpenAI Classify:** An OpenAI model is prompted to decide with a "Yes" or "No" if the post's text is actually about the n8n.io automation tool.
5.  **Merge and Filter:** The classification result is merged with the post data. An IF node then filters out any posts that were classified as "No".
6.  **OpenAI Summary:** For the remaining relevant posts, another OpenAI model is prompted to create a one-sentence summary of the post.
7.  **SetFinal:** The final data, including the summary, is formatted for output.

---

## 165. 1/Instagram_Twitter_Social_Media/Social Media Analysis and Automated Email Generation.txt

**Workflow:** Social Media Analysis and Automated Email Generation

This workflow automates lead generation by analyzing a prospect's social media activity on LinkedIn and Twitter (X). It triggers when a new lead is added to a Google Sheet, fetches their recent posts, uses AI to find a common interest, and generates a personalized outreach email.

### Trigger

- **Type:** Google Sheets Trigger
- **Details:** The workflow starts when a new row is added to a Google Sheet containing lead information (name, email, LinkedIn URL, Twitter handle).

### Workflow Steps

1.  **Set Company Variables:** Defines the user's company name, activity, name, and email for use in the outreach email.
2.  **Filter "done" rows:** An IF node checks if the "done" column for the new row is empty, proceeding only for new, unprocessed leads.
3.  **Get Twitter ID:** Retrieves the user ID for the lead's Twitter handle using the `twitter-api47` on RapidAPI.
4.  **Get Tweets:** Fetches the lead's recent tweets using their user ID.
5.  **Get LinkedIn Posts:** Fetches the lead's recent posts from their LinkedIn profile using the `fresh-linkedin-profile-data` API on RapidAPI.
6.  **Extract and Limit Posts:** Two Code nodes process the raw post data from both platforms, extracting the text and limiting the number of posts to 10 from each.
7.  **Generate Email (OpenAI):** An OpenAI model (`gpt-4o`) receives the collected posts and the user's company information. It is prompted to find a common activity or interest and generate a personalized HTML cover letter and subject line.
8.  **Send Email:** The generated subject and HTML cover letter are sent to the lead's email address, with a CC to the user's email.
9.  **Update Google Sheet:** The "done" column for the lead's row in the Google Sheet is marked with an "X" to prevent reprocessing.

---

## 166. 1/Instagram_Twitter_Social_Media/Speed Up Social Media Banners With BannerBear.com.txt

**Workflow:** Speed Up Social Media Banners With BannerBear.com

This workflow automates the creation of social media event banners. It uses an n8n Form to collect event details, generates a background image with OpenAI's DALL-E 3, combines the image and text using a BannerBear template, and posts the final banner to Discord.

### Trigger

- **Type:** n8n Form
- **Details:** A user submits a form with the event title, location, date, a prompt for the background image, and selects a design template.

### Workflow Steps

1.  **n8n Form Trigger:** Captures the event details from the user.
2.  **Set Parameters:** Structures the form data and maps the selected template name to a BannerBear template ID.
3.  **Generate AI Banner Image (OpenAI):** Sends the user's image prompt to the DALL-E 3 model to generate a background image.
4.  **Upload to Cloudinary:** The generated image is uploaded to Cloudinary to get a public URL. The image URL is optimized for web delivery (`f_auto,q_auto`).
5.  **Send to Bannerbear:** The BannerBear node is called with the template ID and modifications, including the Cloudinary image URL and the event text (title, location, date).
6.  **Download Banner:** The final banner image is downloaded from the URL provided by BannerBear.
7.  **Post to Discord:** The banner image and a message announcing the event are posted to a specified Discord channel.

---

## 167. 1/Instagram_Twitter_Social_Media/Twitter Virtual AI Influencer.txt

**Workflow:** Twitter Virtual AI Influencer

This workflow automates a Twitter account by acting as a virtual influencer. It generates and posts tweets on a schedule or on-demand, based on a configurable persona, writing style, and niche.

### Trigger

- **Type:** Schedule or Manual
- **Details:** Can be configured to post automatically every 6 hours at a random minute or can be triggered manually for on-demand posting.

### Workflow Steps

1.  **Trigger:** The workflow is initiated by either the schedule or a manual trigger.
2.  **Configure your influencer profile:** A Set node defines the persona of the AI influencer. This includes its `niche` (e.g., "Modern Stoicism"), `style` (e.g., "very personal"), and `inspiration` (e.g., specific books on psychology and influence).
3.  **Generate tweet content (OpenAI):** An OpenAI model (`gpt-4-turbo-preview`) is prompted to write a viral tweet. The system prompts are built from the configured influencer profile, and it's instructed to keep the tweet under 280 characters.
4.  **Verify tweet constraints:** An IF node checks if the generated tweet exceeds the 280-character limit.
5.  **Regenerate if needed:** If the tweet is too long, the workflow loops back to the "Configure your influencer profile" step to try again.
6.  **Post tweet:** If the tweet is within the length limit, it is posted to the configured X (Twitter) account.

---

## 168. 1/Instagram_Twitter_Social_Media/Update Twitter banner using HTTP request.txt

**Workflow:** Update Twitter banner using HTTP request

This simple workflow demonstrates how to update a Twitter profile banner by downloading an image from a URL and uploading it to Twitter.

### Trigger

- **Type:** Manual
- **Details:** The workflow is started manually.

### Workflow Steps

1.  **HTTP Request (Download):** Downloads an image from a specified Unsplash URL. The response format is set to "file".
2.  **HTTP Request (Upload):** Makes a POST request to the Twitter API endpoint `1.1/account/update_profile_banner.json`. It uses OAuth 1.0a authentication and sends the downloaded image file as multipart form data.
---

## 169. 1/Notion/Add positive feedback messages to a table in Notion.txt

**Workflow:** Add positive feedback messages to a table in Notion

This workflow processes feedback submitted through a Typeform. It uses Google Cloud Natural Language to analyze the sentiment of the feedback. Positive feedback is then added to a Notion database and a notification is sent to Slack, while negative or neutral feedback is added as a card to a Trello board.

### Trigger

- **Type:** Typeform
- **Details:** The workflow is triggered when a new response is submitted to the connected Typeform.

### Workflow Steps

1.  **Typeform Trigger:** Receives a new form submission containing the user's name and feedback.
2.  **Google Cloud Natural Language:** Analyzes the sentiment of the feedback text and returns a sentiment score.
3.  **IF Node:** Checks if the sentiment score is greater than 0 (positive).
4.  **Positive Feedback Path:**
    *   **Notion:** Creates a new page in a "Feedback" database in Notion, adding the user's name and their feedback.
    *   **Slack:** Sends a message to the #general channel in Slack with the user's name and their positive feedback.
5.  **Neutral/Negative Feedback Path:**
    *   **Trello:** Creates a new card on a Trello board with the sentiment score and the full feedback text for review.

---

## 170. 1/Notion/Analyse papers from Hugging Face with AI and store them in Notion.txt

**Workflow:** Analyse papers from Hugging Face with AI and store them in Notion

This workflow automates the process of fetching, analyzing, and storing academic papers from Hugging Face. It runs on a schedule, scrapes the latest papers, uses OpenAI to extract key details, and saves the structured information to a Notion database.

### Trigger

- **Type:** Schedule
- **Details:** Runs every weekday at 8:00 AM.

### Workflow Steps

1.  **Request Hugging Face Paper:** Fetches the HTML of the Hugging Face papers page for the previous day.
2.  **Extract Paper URLs:** Extracts all the individual paper URLs from the fetched HTML.
3.  **Loop Over Papers:** The workflow iterates through each paper URL.
4.  **Check if Paper Exists:** Queries a Notion database to see if the paper's URL has already been processed and stored.
5.  **Process New Paper:** If the paper is new:
    *   **Request Paper Detail:** Fetches the HTML of the individual paper's page.
    *   **Extract Abstract:** Extracts the paper's title and abstract from the page.
    *   **OpenAI Analysis:** Sends the abstract to an OpenAI model (`gpt-4o-2024-11-20`) with a detailed prompt to extract the core introduction, keywords, key results, technical details, and an academic classification. The output is requested in a specific JSON format.
    *   **Store in Notion:** Creates a new page in the "huggingface-abstract" Notion database, populating it with the paper's URL, title, abstract, and all the structured data extracted by the AI.

---

## 171. 1/Notion/Automate Competitor Research with Exa.ai, Notion and AI Agents.txt

**Workflow:** Automate Competitor Research with Exa.ai, Notion and AI Agents

This workflow automates competitor research by using Exa.ai to find similar companies and then deploying multiple AI agents to gather detailed information about them. The final compiled report is stored in a Notion database.

### Trigger

- **Type:** Manual
- **Details:** The workflow is initiated manually.

### Workflow Steps

1.  **Find Similar Companies (Exa.ai):** An HTTP Request is made to the Exa.ai API to find companies similar to a source company (e.g., "n8n.io").
2.  **Process Competitors:** The list of competitors is filtered for duplicates and then processed one by one.
3.  **Agent 1: Company Overview:**
    *   An AI agent is tasked with finding a general overview of the competitor.
    *   It uses tools to search for Crunchbase, WellFound, and LinkedIn profiles, and a general web scraper (Firecrawl) to read the content of those pages.
    *   It outputs a structured summary including founders, key people, funding status, investors, and recent articles.
4.  **Agent 2: Product & Pricing:**
    *   A second agent investigates the competitor's product offerings and pricing.
    *   It uses a tool to search the company's website for terms like "pricing," "plans," and "features."
    *   It outputs a structured summary of features, pricing plans, and technology used.
5.  **Agent 3: Customer Reviews:**
    *   A third agent searches for customer reviews on sites like Trustpilot and Product Hunt.
    *   It uses a web scraper to read the content of the review pages.
    *   It outputs a summary of positive and negative feedback, common themes, and overall sentiment.
6.  **Compile and Save to Notion:** The outputs from all three agents are merged, and a new page is created in a "Competitor Research" Notion database with the comprehensive report.

---

## 172. 1/Notion/Automate LinkedIn Outreach with Notion and OpenAI.txt

**Workflow:** Automate LinkedIn Outreach with Notion and OpenAI

This workflow automates posting content to LinkedIn. It fetches a scheduled post from a Notion database, uses an OpenAI assistant to reformat the text for better engagement, and then posts it to LinkedIn along with its associated image.

### Trigger

- **Type:** Schedule
- **Details:** The workflow runs daily at 3:00 PM.

### Workflow Steps

1.  **Query Notion for Today's Post:** Queries a "LinkedIn Posts" database in Notion to find an entry where the "Date" column matches today's date.
2.  **Get Page Content:** Retrieves all the content blocks (text and images) from the Notion page for that post.
3.  **Aggregate Content:** Combines all the text blocks into a single string and extracts the URL of the image.
4.  **Reformat Post Text (OpenAI):** The aggregated text is sent to a pre-configured OpenAI Assistant ("LinkedIn Post Reviewer"). The assistant is prompted to reformat the text with appropriate paragraph breaks and lists to improve readability on LinkedIn.
5.  **Fetch Image:** Downloads the image from the URL extracted from the Notion page.
6.  **Combine and Post:** The reformatted text from OpenAI is merged with the downloaded image. The final content is then published as a new post on the connected LinkedIn account.
7.  **Update Notion Status:** The status of the post in the Notion database is updated to "Done" to prevent it from being posted again.

---

## 173. 1/Notion/Notion AI Assistant Generator.txt

**Workflow:** Notion AI Assistant Generator

This advanced workflow acts as a meta-workflow. It provides a chat interface where a user can input the URL of any Notion database, and it will automatically generate and output the JSON for a new, fully functional n8n AI Assistant workflow tailored to that specific database schema.

### Trigger

- **Type:** n8n Chat
- **Details:** A user interacts with a chat interface, providing a Notion database URL.

### Workflow Steps

1.  **Get Notion DB Schema:** The workflow receives the URL from the chat input and uses the Notion API to retrieve the schema of the provided database, including all properties and their types.
2.  **Simplify Schema:** A Code node processes the raw schema, simplifying the properties object to make it more token-efficient for the AI model.
3.  **Generate Workflow Agent (Anthropic):** An AI agent powered by an Anthropic model receives the simplified database schema and a template of the target workflow. It is prompted to modify the template's "Search notion database" tool node, specifically updating the `jsonBody` parameter to include the correct property names and filter conditions based on the new schema.
4.  **Validate and Fix (Loop):**
    *   **Auto-fixing Output Parser:** The agent's output (the new workflow JSON) is passed to a parser that attempts to fix any syntax errors.
    *   **Check for Errors:** A Switch node checks for common errors, such as the AI outputting `[object Object]` instead of a valid filter.
    *   **LLM Validation:** A Text Classifier is used to perform a final check on whether the output is valid n8n workflow JSON.
    *   **Retry with Feedback:** If any check fails, the workflow loops back, providing the failed output and feedback to the agent to try again.
5.  **Return Workflow JSON:** Once a valid workflow is generated, the final JSON is formatted and sent back to the user in the chat interface with instructions to copy and paste it into their n8n canvas.
---

## 174. 1/Notion/Notion knowledge base AI assistant.txt

**Workflow:** Notion knowledge base AI assistant

This workflow creates a conversational AI assistant that can answer questions based on the content of a Notion database. It uses a set of tools to search the database and retrieve page content, allowing a user to query their knowledge base using natural language through the n8n chat interface.

### Trigger

- **Type:** n8n Chat
- **Details:** The workflow is initiated when a user starts a conversation in the chat interface.

### Workflow Steps

1.  **Get database details:** Retrieves the schema of the specified Notion database, including the available tags for filtering.
2.  **Format schema:** A Set node formats the database name, ID, and tag options for use in the AI agent's tool descriptions.
3.  **AI Agent (OpenAI):** An agent powered by `gpt-4o` receives the user's query. It is prompted to act as a helpful assistant and use the provided tools to answer questions.
4.  **Search notion database (Tool):** An HTTP Request tool that queries the Notion database. It allows the agent to filter by a keyword (searching the 'question' property) or by a specific tag.
5.  **Search inside database record (Tool):** Another HTTP Request tool that retrieves the full block content of a specific Notion page using its page ID.
6.  **Window Buffer Memory:** Maintains a history of the conversation to handle follow-up questions.
7.  **Response Generation:** The agent uses the information retrieved from the tools to formulate a response and sends it back to the user in the chat.

---

## 175. 1/Notion/Notion to Pinecone Vector Store Integration.txt

**Workflow:** Notion to Pinecone Vector Store Integration

This workflow automates the process of keeping a Pinecone vector store synchronized with a Notion database. When a new page is added to Notion, the workflow retrieves its content, chunks it, generates embeddings, and inserts them into Pinecone.

### Trigger

- **Type:** Notion Trigger
- **Event:** `Page Added`
- **Details:** The workflow starts whenever a new page is added to a specified Notion database.

### Workflow Steps

1.  **Notion - Page Added Trigger:** Detects a new page in the "Embeddings" database.
2.  **Notion - Retrieve Page Content:** Fetches all the content blocks from the new page.
3.  **Filter Non-Text Content:** Removes any image or video blocks to focus on textual data.
4.  **Summarize - Concatenate Content:** Combines the content of all remaining text blocks into a single text field.
5.  **Create metadata and load content:** A Document Loader prepares the concatenated text for processing and attaches metadata, including the Notion page ID, creation time, and title.
6.  **Token Splitter:** Splits the text into chunks of 256 tokens with an overlap of 30 tokens.
7.  **Embeddings Google Gemini:** Generates vector embeddings for each text chunk using the `models/text-embedding-004` model.
8.  **Pinecone Vector Store:** Inserts the generated embeddings and their associated metadata into the `notion-pages` index in Pinecone.

---

## 176. 1/Notion/Store Notion_s Pages as Vector Documents into Supabase with OpenAI.txt

**Workflow:** Store Notion's Pages as Vector Documents into Supabase with OpenAI

This workflow automates the process of embedding Notion pages and storing them in a Supabase vector store. It triggers on new page additions, processes the page content, generates embeddings with OpenAI, and upserts them into Supabase.

### Trigger

- **Type:** Notion Trigger
- **Event:** `Page Added`
- **Details:** The workflow starts when a new page is added to a specified Notion database.

### Workflow Steps

1.  **Notion - Page Added Trigger:** Detects when a new page is added to the target database.
2.  **Notion - Retrieve Page Content:** Retrieves all content blocks from the newly added page.
3.  **Filter Non-Text Content:** Excludes image and video blocks.
4.  **Summarize - Concatenate Content:** Merges the text from all blocks into a single document.
5.  **Create metadata and load content:** Prepares the text for embedding and attaches metadata like the page ID and title.
6.  **Token Splitter:** Breaks the content into smaller chunks suitable for embedding.
7.  **Embeddings OpenAI:** Generates vector embeddings for each chunk using an OpenAI model.
8.  **Supabase Vector Store:** Inserts the documents and their corresponding embeddings into the specified table in Supabase, which must have a vector column.

---

## 177. 1/Notion/Turn Emails into AI-Enhanced Tasks in Notion (Multi-User Support) with Gmail, Airtable and Softr.txt

**Workflow:** Turn Emails into AI-Enhanced Tasks in Notion (Multi-User Support)

This complex workflow creates a multi-tenant system for turning emails into AI-enhanced tasks in Notion. Users can forward emails to a unique alias, which triggers the workflow to summarize the email content using AI and create a new task in the user's designated Notion database. The system is managed via an Airtable base, potentially with a Softr frontend.

### Trigger

- **Type:** Gmail Trigger
- **Details:** The workflow starts when a new email is received in a specific Gmail inbox.

### Workflow Steps

1.  **Filter for unprocessed mails:** The workflow filters for new emails that have not been processed or marked with an error label. It also ensures the email was sent to a valid `+` alias.
2.  **Extract Route ID:** It extracts a unique ID from the recipient email address (e.g., the `xyz` from `myemail+xyz@gmail.com`).
3.  **Get Route by ID (Airtable):** It uses the extracted ID to look up the corresponding route in an Airtable "Routes" table. This table stores the user's Notion API token and target Notion Database ID.
4.  **AI Summarization (OpenAI):** The body of the email is sent to the `gpt-4o` model with a prompt to summarize the content and extract the sender, subject, and date into a structured JSON format.
5.  **Create Notion Page:** An HTTP Request node makes a call to the Notion API to create a new page in the user's database. It uses the Notion token from Airtable and populates the page with the AI-generated summary and metadata.
6.  **Label and Notify:**
    *   If successful, the original email is labeled "Processed" in Gmail.
    *   If there's an error (e.g., invalid Notion token, database not shared), the route is deactivated in Airtable, the email is labeled "Error", and a notification is sent to the user.

---

## 178. 1/Notion/Upsert huge documents in a vector store with Supabase and Notion.txt

**Workflow:** Upsert huge documents in a vector store with Supabase and Notion

This workflow provides a robust RAG (Retrieval-Augmented Generation) pipeline that keeps a Supabase vector store synchronized with a Notion knowledge base. It periodically checks for updated Notion pages, deletes the old embeddings, and upserts the new, chunked content. It also includes a chat interface for querying the knowledge base.

### Trigger

- **Type:** Schedule (for updates) and n8n Chat (for queries)
- **Details:** A schedule trigger runs every minute to check for updated Notion pages. A separate chat trigger allows users to ask questions.

### Workflow Steps

**Data Synchronization (Scheduled):**
1.  **Get updated pages:** Fetches any pages from a Notion "Knowledge Base" that were edited in the last minute.
2.  **Loop Over Items:** Processes each updated page individually.
3.  **Delete old embeddings:** Deletes all existing vectors from the Supabase `documents` table that match the Notion page ID, ensuring the data is fresh.
4.  **Get page blocks:** Retrieves all content blocks from the updated Notion page.
5.  **Process and Chunk:** The content is concatenated, loaded with metadata, and split into 500-token chunks.
6.  **Embed and Upsert:** Generates OpenAI embeddings for each chunk and upserts them into the Supabase vector store.

**Chat Interaction:**
1.  **When chat message received:** A user asks a question.
2.  **Question and Answer Chain:** An AI agent receives the query.
3.  **Vector Store Retriever:** The agent queries the Supabase vector store to retrieve relevant document chunks.
4.  **Response Generation:** The `gpt-4o` model synthesizes an answer based on the retrieved context and sends it to the user.
---

## 179. 1/OpenAI_and_LLMs/⚡AI-Powered YouTube Video Summarization & Analysis.txt

**Workflow:** AI-Powered YouTube Video Summarization & Analysis

This workflow automates the summarization and analysis of YouTube videos. It is triggered by a webhook containing a YouTube URL, extracts the video's transcript, uses an AI model to create a structured summary, and then sends the results to Telegram and the original webhook caller.

### Trigger

- **Type:** Webhook
- **Details:** Receives a POST request with a JSON body containing a `youtubeUrl`.

### Workflow Steps

1.  **Get YouTube URL:** Extracts the YouTube URL from the webhook body.
2.  **Extract Video ID:** A Code node parses the URL to get the unique video ID.
3.  **Get YouTube Video:** Retrieves video details, including title and description, using the video ID.
4.  **Get YouTube Transcript:** Fetches the full transcript of the video.
5.  **Concatenate Transcript:** The transcript, which is often split into multiple parts, is concatenated into a single block of text.
6.  **Summarize & Analyze Transcript (OpenAI):** The concatenated transcript is sent to a `gpt-4o-mini` model. The prompt instructs the AI to analyze the text and create a structured summary with Level 2 headers for main topics, bullet points for key concepts, and bolding for important terms.
7.  **Format Response:** A Set node structures the final output, combining the AI-generated summary with the video's title, description, and URL.
8.  **Respond to Webhook:** Sends the structured response back to the service that initiated the workflow.
9.  **Send to Telegram:** Sends a message to a Telegram chat containing the video title and URL.

---

## 180. 1/OpenAI_and_LLMs/🎨 Interactive Image Editor with FLUX.1 Fill Tool for Inpainting.txt

**Workflow:** Interactive Image Editor with FLUX.1 Fill Tool for Inpainting

This workflow provides a web-based interactive image editor that allows users to perform inpainting (filling or replacing parts of an image) using the FLUX.1 Fill model. It serves an HTML editor, processes user edits, calls the FLUX API, and returns the generated image.

### Trigger

- **Type:** Webhook
- **Details:** The workflow listens for GET requests to serve the editor and POST requests to process image generation tasks.

### Workflow Steps

**Serving the Editor (GET Request):**
1.  **Webhook:** Receives a GET request.
2.  **Mockups:** A Set node provides an array of default images for the user to choose from.
3.  **Editor Page:** An HTML node serves a complete, self-contained web page built with HTML, CSS, and JavaScript. It includes a Konva.js canvas for drawing masks, sliders for adjusting parameters, and an image comparison tool.

**Processing Inpainting (POST Request):**
1.  **Webhook:** Receives a POST request from the editor's JavaScript. The body contains the original image, the user-drawn mask, a text prompt, and generation parameters (steps, guidance).
2.  **FLUX Fill (API Request):** An HTTP Request node sends the data to the `api.bfl.ml` endpoint for the FLUX Fill model.
3.  **Polling Loop:**
    *   The workflow waits for 3 seconds.
    *   It then checks the status of the generation job.
    *   An IF node checks if the status is "Ready". If not, it waits and checks again.
4.  **Get Fill Image:** Once ready, it downloads the generated image from the result URL.
5.  **Show Image to User:** The final image is sent back as a binary response to the webhook, displaying it to the user.

---

## 181. 1/OpenAI_and_LLMs/🐋DeepSeek V3 Chat & R1 Reasoning Quick Start.txt

**Workflow:** DeepSeek V3 Chat & R1 Reasoning Quick Start

This workflow provides four different methods for interacting with DeepSeek's large language models, demonstrating how to connect via the native Ollama integration, the OpenAI-compatible API, and direct HTTP requests.

### Trigger

- **Type:** n8n Chat
- **Details:** A user sends a message through the n8n chat interface to test the different models.

### Workflow Steps

**Method 1: Ollama Local Model**
1.  **Basic LLM Chain:** The user's input is passed to a chain.
2.  **Ollama DeepSeek:** The chain uses the `Ollama DeepSeek` node to connect to a locally running Ollama instance and query the `deepseek-r1:14b` model.

**Method 2: DeepSeek API (Reasoner R1 - Raw Body)**
1.  **HTTP Request:** Makes a POST request to `https://api.deepseek.com/chat/completions` with the model specified as `deepseek-reasoner`. The message is sent in the raw request body.

**Method 3: DeepSeek API (Chat V3 - JSON Body)**
1.  **HTTP Request:** Makes a POST request to the same endpoint but specifies the model as `deepseek-chat`. The message is sent as a JSON body.

**Method 4: Conversational Agent (OpenAI-Compatible)**
1.  **AI Agent:** A conversational agent is set up.
2.  **DeepSeek Model:** The agent uses the `lmChatOpenAi` node, but the `model` is set to `deepseek-reasoner` and the `baseURL` in the credential points to `https://api.deepseek.com`. This leverages the OpenAI-compatible API format.
3.  **Window Buffer Memory:** The agent maintains a conversation history.

---

## 182. 1/OpenAI_and_LLMs/📚 Auto-generate documentation for n8n workflows with GPT and Docsify.txt

**Workflow:** Auto-generate documentation for n8n workflows with GPT and Docsify

This is a powerful meta-workflow that automatically generates a documentation website for all the workflows in an n8n instance. It fetches workflows, uses GPT to generate descriptions, creates Markdown files, and serves them as a live website using Docsify.js.

### Trigger

- **Type:** Webhook
- **Details:** The workflow is accessed via a webhook, which serves the Docsify-powered website. It can also be run manually to regenerate the documentation.

### Workflow Steps

1.  **Fetch All Workflows:** Retrieves a list of all workflows from the n8n instance via the API.
2.  **Generate Documentation (Loop):** For each workflow:
    *   **Generate Mermaid Chart:** Creates a Mermaid.js flowchart diagram representing the workflow's structure.
    *   **Generate Description (OpenAI):** Sends the workflow's JSON data to a GPT model (`gpt-4-turbo`) and prompts it to generate a detailed description of the workflow and its nodes.
    *   **Create Markdown File:** Combines the AI-generated description and the Mermaid chart into a Markdown file named `docs_{workflow_id}.md`.
    *   **Write File:** Saves the Markdown file to a local project directory.
3.  **Create Summary:** Generates a `summary.md` file that acts as a sidebar for Docsify, linking to all the individual workflow documentation pages.
4.  **Serve Website (Webhook Logic):**
    *   When a user accesses the webhook URL, it routes the request.
    *   If the request is for the main page, it serves an `index.html` file that loads Docsify.
    *   If the request is for a specific `.md` file, it reads the file from the local directory and serves its content.
    *   It also includes an "edit" action, which serves an HTML page with an editor to allow manual refinement of the AI-generated documentation.

---

## 183. 1/OpenAI_and_LLMs/🔐🦙🤖 Private & Local Ollama Self-Hosted AI Assistant.txt

**Workflow:** Private & Local Ollama Self-Hosted AI Assistant

This workflow demonstrates how to create a simple, private, and locally-hosted AI chatbot using n8n and Ollama. It provides a chat interface that connects to a local Llama 3.2 model running via Ollama.

### Trigger

- **Type:** n8n Chat
- **Details:** The workflow is initiated when a user sends a message in the chat interface.

### Workflow Steps

1.  **When chat message received:** The chat trigger captures the user's input.
2.  **Basic LLM Chain:** The input is passed to a LangChain LLM Chain. The prompt is configured to ask the AI to return a JSON object containing both the original prompt and the generated response.
3.  **Ollama Model:** The chain is connected to the `Ollama Model` node, which is configured to use the `llama3.2:latest` model running on a local Ollama instance.
4.  **JSON to Object:** The JSON string returned by the LLM is parsed into a structured object.
5.  **Structured Response:** A Set node formats the final response for the user, showing both their original prompt and the AI's answer.
6.  **Error Handling:** If the LLM chain fails to return a valid JSON, a separate Set node provides a generic error message.
---

## 184. 1/OpenAI_and_LLMs/🔥📈🤖 AI Agent for n8n Creators Leaderboard - Find Popular Workflows.txt

**Workflow:** AI Agent for n8n Creators Leaderboard - Find Popular Workflows

This workflow provides an AI-powered agent that can generate a comprehensive Markdown report about a specific n8n community workflow contributor. It fetches data from the n8n community leaderboard, analyzes it, and presents a detailed summary of the creator's workflows and their impact.

### Trigger

- **Type:** n8n Chat or Execute Workflow
- **Details:** Can be triggered via the n8n chat interface by providing a creator's username, or called by another workflow.

### Workflow Steps

1.  **AI Agent (OpenAI):** The main agent receives the user's query (the creator's username). It is prompted to use a custom tool to retrieve stats and then generate a detailed summary, a Markdown table of workflows, a community analysis, and any additional insights.
2.  **Workflow Tool (`n8n_creator_stats`):** This tool is a sub-workflow that fetches and processes the leaderboard data.
    *   **Global Variables:** Sets up paths to the leaderboard data on GitHub.
    *   **Fetch Data:** HTTP Request nodes get the latest `stats_aggregate_creators.json` and `stats_aggregate_workflows.json` files.
    *   **Filter and Parse:** The data is parsed, and the workflows are filtered by the requested username.
    *   **Aggregate:** The filtered data is aggregated to be returned to the main agent.
3.  **Report Generation:** The AI agent receives the aggregated data from the tool and formats it into the final Markdown report as per the system prompt's instructions.
4.  **Save Report (Optional):** The generated Markdown report is saved locally as a `.md` file.

---

## 185. 1/OpenAI_and_LLMs/🤖🧑_💻 AI Agent for Top n8n Creators Leaderboard Reporting.txt

**Workflow:** AI Agent for Top n8n Creators Leaderboard Reporting

This workflow is nearly identical to the previous one ("AI Agent for n8n Creators Leaderboard - Find Popular Workflows"). It also creates an AI agent to generate reports on n8n community contributors by fetching data from the same GitHub repository. The primary difference appears to be in the specific arrangement and naming of nodes, but the core functionality remains the same.

### Trigger

- **Type:** Execute Workflow
- **Details:** Designed to be called by another workflow, passing in a creator's username.

### Workflow Steps

1.  **Global Variables:** Sets up paths to the n8n community leaderboard data on GitHub.
2.  **Fetch Data:** Retrieves the latest JSON data for creators and workflows.
3.  **Parse and Filter:** The data is parsed, and the workflows are filtered by the provided username.
4.  **Aggregate Data:** The filtered creator and workflow data is aggregated.
5.  **Return Response:** The aggregated data is returned as the output of the workflow.

---

## 186. 1/OpenAI_and_LLMs/🚀 Local Multi-LLM Testing & Performance Tracker.txt

**Workflow:** Local Multi-LLM Testing & Performance Tracker

This workflow provides a framework for testing and comparing the performance of multiple local Large Language Models (LLMs) hosted via LM Studio. It sends the same prompt to each model, captures the response, and logs performance metrics like response time and readability scores to a Google Sheet.

### Trigger

- **Type:** n8n Chat
- **Details:** A user provides a prompt in the chat interface to start the testing process.

### Workflow Steps

1.  **Get Models:** An HTTP Request node queries the LM Studio server (`/v1/models`) to get a list of all currently loaded models.
2.  **Loop Through Models:** The workflow iterates through each available model.
3.  **Capture Start Time:** A DateTime node records the start time before sending the prompt to the model.
4.  **Run Model with Dynamic Inputs:** The `lmChatOpenAi` node is used to send the user's prompt to the current model in the loop. The `baseURL` is configured to point to the local LM Studio server.
5.  **Capture End Time:** Another DateTime node records the time the response is received.
6.  **Calculate Time Difference:** The total response time is calculated.
7.  **Analyze LLM Response Metrics:** A Code node calculates several metrics for the response text, including word count, sentence count, average sentence length, average word length, and the Flesch-Kincaid Readability Score.
8.  **Save Results to Google Sheets:** All the captured data—the prompt, response, model ID, timings, and calculated metrics—is appended as a new row to a Google Sheet for later analysis.

---

## 187. 1/OpenAI_and_LLMs/Actioning Your Meeting Next Steps using Transcripts and AI.txt

**Workflow:** Actioning Your Meeting Next Steps using Transcripts and AI

This workflow automates post-meeting actions by analyzing a Google Meet transcript. It uses an AI agent to identify action items, such as scheduling follow-up meetings, and then uses tools to execute those actions directly in Google Calendar.

### Trigger

- **Type:** Manual
- **Details:** The workflow is initiated manually, presumably after a meeting has concluded.

### Workflow Steps

1.  **Get Calendar Event:** Retrieves a specific Google Calendar event to get its meeting details.
2.  **Get Meeting Conference Records:** Uses the Google Meet API to find the conference record associated with the calendar event.
3.  **Get Meeting Transcript Location:** Retrieves the location of the meeting transcript, which is stored as a Google Doc.
4.  **Get Transcript File:** Downloads the transcript document from Google Drive.
5.  **PDF Loader:** Extracts the text from the downloaded transcript file.
6.  **AI Agent (OpenAI):** An AI agent (`gpt-4o-mini`) receives the transcript text. It is prompted to analyze the transcript, identify next steps, and use available tools to action them.
7.  **Create Calendar Event (Tool):** A custom workflow tool that the agent can call. It takes a title, description, start/end times, and a list of attendees to create a new event in Google Calendar.
8.  **Tool Execution:** If the agent determines a follow-up meeting is needed, it calls the `create_calendar_event` tool with the extracted details, which then creates the event and invites the specified attendees.

---

## 188. 1/OpenAI_and_LLMs/Advanced AI Demo (Presented at AI Developers #14 meetup).txt

**Workflow:** Advanced AI Demo (Presented at AI Developers #14 meetup)

This workflow is a demonstration showcasing several advanced AI use cases in n8n. It includes three distinct examples: categorizing emails, performing RAG with a PDF, and an AI assistant for booking appointments.

### Trigger

- **Type:** Webhook (for email categorization), Manual (for PDF RAG), n8n Chat (for appointment booking)
- **Details:** The workflow has multiple entry points to demonstrate different functionalities.

### Workflow Steps

**Example 1: Email Categorization**
1.  **Webhook:** Receives an email subject and body.
2.  **AI Agent (OpenAI):** An agent uses a `textClassifier` to categorize the email into "Sales," "Support," or "Info."
3.  **Switch Node:** Routes the flow based on the category.
4.  **Action:** Performs an action based on the category, such as sending a Slack message.

**Example 2: RAG with PDF**
1.  **Download PDF:** Downloads a source PDF (e.g., the Bitcoin whitepaper).
2.  **Load and Chunk:** The PDF is loaded, and its text is split into chunks.
3.  **Embed and Store:** OpenAI embeddings are generated for each chunk and stored in a Pinecone vector store under a specific namespace.
4.  **Chat with PDF:** A Q&A chain is set up, allowing a user to ask questions. The chain retrieves relevant chunks from Pinecone to provide contextually accurate answers.

**Example 3: Appointment Booking Assistant**
1.  **Chat Trigger:** A user interacts with the chatbot to book a meeting.
2.  **AI Agent (Anthropic):** An agent is prompted to act as a courteous scheduling assistant for "Max."
3.  **Get Availability (Tool):** A tool makes a request to the Google Calendar API's `freeBusy` endpoint to check for available slots.
4.  **Book Appointment (Tool):** Another tool makes a request to the Google Calendar API to create a new event with the specified details and attendees.
5.  **Conversational Flow:** The agent interacts with the user, checking for availability and confirming the booking using the provided tools.
---

## 189. 1/OpenAI_and_LLMs/AI Agent _ Google calendar assistant using OpenAI.txt

**Workflow:** AI Agent : Google calendar assistant using OpenAI

This workflow creates an AI-powered assistant for managing a Google Calendar. Users can interact with it via the n8n chat interface to create events and retrieve event data using natural language.

### Trigger

- **Type:** n8n Chat
- **Details:** The workflow is initiated when a user sends a message in the chat interface.

### Workflow Steps

1.  **When chat message received:** Captures the user's request.
2.  **Calendar AI Agent (OpenAI):** An agent powered by `gpt-4o` receives the user's message. It is given a detailed system prompt that instructs it on how to behave, including how to handle vague requests, what information to gather for creating or retrieving events, and to use the current date for context.
3.  **Window Buffer Memory:** Maintains a short-term memory of the conversation.
4.  **Google Calendar - Get Events (Tool):** A tool that allows the agent to retrieve a list of calendar events within a specified date range (`start_date`, `end_date`). The agent is responsible for determining these dates based on the user's query.
5.  **Google Calendar - Create events (Tool):** A tool that allows the agent to create a new event. The agent is prompted to gather the `start_date`, `end_date`, `event_title`, and `event_description` from the user before calling this tool.
6.  **Response Generation:** The agent uses the output from the tools (or its own conversational abilities) to respond to the user, either confirming an action or asking for more information.

---

## 190. 1/OpenAI_and_LLMs/AI agent chat.txt

**Workflow:** AI agent chat

This workflow sets up a basic conversational AI agent with the ability to search the web. It uses the n8n chat interface for user interaction, an OpenAI model for language processing, and the SerpAPI tool for web searches.

### Trigger

- **Type:** n8n Chat
- **Details:** The workflow starts when a user sends a message.

### Workflow Steps

1.  **When chat message received:** Captures the user's input.
2.  **AI Agent (OpenAI):** A conversational agent receives the input.
3.  **OpenAI Chat Model:** The agent is powered by the `gpt-4o-mini` model.
4.  **Window Buffer Memory:** Stores the recent conversation history for context.
5.  **SerpAPI (Tool):** The agent is equipped with a SerpAPI tool, which it can use to perform a Google search if it needs information from the internet to answer the user's query.
6.  **Response Generation:** The agent synthesizes information from its internal knowledge and any web search results to formulate and return a response.

---

## 191. 1/OpenAI_and_LLMs/AI Agent for realtime insights on meetings.txt

**Workflow:** AI Agent for realtime insights on meetings

This workflow provides real-time transcription and AI-powered insights during a live meeting. It uses Recall.ai to have a bot join a meeting, sends the live transcript to the workflow via a webhook, and allows an OpenAI assistant to be prompted with keywords to perform actions like creating notes.

### Trigger

- **Type:** Webhook
- **Details:** A webhook receives real-time transcription data from the Recall.ai bot that has joined a meeting.

### Workflow Steps

1.  **Create Recall bot:** A bot is created and instructed to join a specified meeting URL (e.g., Google Meet).
2.  **Create OpenAI thread:** A new thread is created in the OpenAI Assistants API to manage the context of the meeting.
3.  **Create data record (Supabase):** A record is created in a Supabase table to store the meeting data, linking the Recall bot ID and the OpenAI thread ID.
4.  **Webhook (Real-time Transcription):** The workflow listens for POST requests from Recall.ai containing chunks of the meeting transcript.
5.  **Insert Transcription Part:** Each transcript chunk is appended to a `dialog` array in the Supabase record for the current meeting.
6.  **Keyword Trigger (IF node):** An IF node checks if the incoming transcript chunk contains a specific keyword (e.g., "Jimmy").
7.  **Prompt Assistant (OpenAI):** If the keyword is detected, the recent dialogue is sent to a pre-configured OpenAI Assistant. The assistant is equipped with tools to perform actions.
8.  **Create Note (Tool):** A tool is defined that allows the assistant to create a note. The tool is a PostgreSQL query that inserts the note text (provided by the AI) into a `notes` array in the meeting's Supabase record.

---

## 192. 1/OpenAI_and_LLMs/AI agent that can scrape webpages.txt

**Workflow:** AI agent that can scrape webpages

This workflow creates a ReAct-style AI agent that can scrape the content of a webpage. The agent is given a custom tool that makes an HTTP request to a URL. The workflow includes logic to process the HTML, clean it, and handle potential errors.

### Trigger

- **Type:** Manual Chat
- **Details:** A user provides a prompt, typically asking the agent to fetch and summarize the content of a URL.

### Workflow Steps

1.  **ReAct AI Agent (OpenAI):** The agent is initialized with a prompt instructing it to use its tools to answer questions.
2.  **HTTP_Request_Tool (Workflow Tool):** A custom tool is defined that allows the agent to fetch webpage content. The agent is prompted to provide the input as a query string (e.g., `?url=https://example.com&method=simplified`).
3.  **Sub-workflow Execution:** When the agent calls the tool, it triggers a sub-workflow:
    *   **Parse Query:** The query string is parsed into a JSON object.
    *   **HTTP Request:** The URL is fetched.
    *   **Error Handling:** An IF node checks if the request was successful. If not, an error message is returned.
    *   **HTML Processing:** If successful, the `<BODY>` content is extracted. Scripts, styles, and other non-essential tags are removed.
    *   **Simplify (Optional):** If the `method` was `simplified`, all `href` and `src` attributes are removed to save tokens.
    *   **Convert to Markdown:** The cleaned HTML is converted to Markdown.
    *   **Length Check:** The final content is checked against a character limit. If it's too long, an error is returned.
4.  **Response Generation:** The agent receives the processed page content from the tool and uses it to formulate the final answer to the user's original question.

---

## 193. 1/OpenAI_and_LLMs/AI Agent To Chat With Files In Supabase Storage.txt

**Workflow:** AI Agent To Chat With Files In Supabase Storage

This workflow creates a RAG (Retrieval-Augmented Generation) pipeline that allows a user to chat with files stored in Supabase Storage. It periodically checks for new files, embeds their content, stores the vectors in a Supabase vector database, and provides a chat interface for querying.

### Trigger

- **Type:** Manual (for indexing) and n8n Chat (for querying)
- **Details:** The indexing process is run manually to sync files. The chat interface is then used to ask questions about the file content.

### Workflow Steps

**Indexing (Manual):**
1.  **Get All files (Supabase Storage):** Lists all files in a "private" bucket in Supabase Storage.
2.  **Get All Files (Supabase DB):** Retrieves a list of files already processed from a `files` table in the database.
3.  **Filter New Files:** An IF node compares the two lists and continues only with files that have not yet been indexed.
4.  **Loop and Process:** For each new file:
    *   **Download:** Downloads the file from Supabase Storage.
    *   **Extract Text:** Extracts text content from the file (handles PDF and TXT).
    *   **Embed and Store:** The text is chunked, embedded using OpenAI's `text-embedding-3-small` model, and inserted into a `documents` table in Supabase, which has a vector column.
    *   **Create File Record:** A record of the processed file is added to the `files` table.

**Chatting (Chat Trigger):**
1.  **When chat message received:** A user asks a question.
2.  **AI Agent (OpenAI):** An agent receives the query.
3.  **Vector Store Tool:** The agent is equipped with a tool that queries the Supabase `documents` vector store to find relevant information to answer the user's question.
---

## 194. 1/OpenAI_and_LLMs/AI Agent to chat with Supabase_PostgreSQL DB.txt

**Workflow:** AI Agent to chat with Supabase/PostgreSQL DB

This workflow creates a conversational AI agent that can interact with a PostgreSQL database (hosted on Supabase). The agent is equipped with tools to understand the database schema and execute custom SQL queries, allowing users to ask questions about their data in natural language.

### Trigger

- **Type:** n8n Chat
- **Details:** The workflow starts when a user sends a message in the chat interface.

### Workflow Steps

1.  **When chat message received:** Captures the user's query.
2.  **AI Agent (OpenAI):** An OpenAI Functions Agent receives the user's request. It is prompted to act as a DB assistant and use its tools to answer the query.
3.  **DB Schema (Tool):** A PostgreSQL tool that executes a query on `information_schema.tables` to get a list of all tables in the public schema. This helps the agent understand the database structure.
4.  **Get table definition (Tool):** A PostgreSQL tool that retrieves the column names, data types, and constraints for a specific table name provided by the agent.
5.  **Run SQL Query (Tool):** A PostgreSQL tool that allows the agent to execute any custom SQL query it constructs based on the user's request and its knowledge of the schema. The agent is prompted to use the `->>` operator to extract data from JSONB columns.
6.  **Response Generation:** The agent uses the results from the tools to formulate a natural language response and sends it back to the user.

---

## 195. 1/OpenAI_and_LLMs/AI Agent to chat with you Search Console Data, using OpenAI and Postgres.txt

**Workflow:** AI Agent to chat with you Search Console Data, using OpenAI and Postgres

This workflow provides an AI agent that can retrieve and analyze data from the Google Search Console. It uses a webhook to receive user requests, calls the Search Console API, and presents the data in a structured format. Chat history is maintained in a PostgreSQL database.

### Trigger

- **Type:** Webhook
- **Details:** Receives a POST request containing a `chatInput` and a `sessionId`.

### Workflow Steps

1.  **Set fields:** Extracts the `chatInput`, `sessionId`, and current date from the incoming request.
2.  **AI Agent (OpenAI):** An agent powered by `gpt-4o` receives the user's query. It is prompted to first retrieve a list of available Search Console properties and then construct an API call based on the user's natural language request for specific insights.
3.  **Postgres Chat Memory:** The conversation history is stored in and retrieved from a PostgreSQL table named `insights_chat_histories`, allowing for contextual follow-up questions.
4.  **Call Search Console Tool (Workflow Tool):** A custom tool that triggers a sub-workflow to handle the actual API calls.
    *   **Switch Node:** The sub-workflow routes the request based on whether the agent asked for the `website_list` or `custom_insights`.
    *   **Get Site List:** Calls the Search Console API to get a list of all accessible web properties.
    *   **Get Custom Insights:** Constructs a detailed query to the Search Console API's `searchAnalytics` endpoint based on parameters (start/end dates, dimensions, row limits) provided by the AI agent.
5.  **Response Generation:** The agent receives the data from the tool and formats it into a markdown table for the user.
6.  **Respond to Webhook:** The final formatted response is sent back to the webhook caller.

---

## 196. 1/OpenAI_and_LLMs/AI Agent with Ollama for current weather and wiki.txt

**Workflow:** AI Agent with Ollama for current weather and wiki

This workflow creates a conversational AI assistant that uses a locally-hosted Ollama model (`llama3.2:latest`) and is equipped with tools to fetch current weather information and look up articles on Wikipedia.

### Trigger

- **Type:** Manual Chat
- **Details:** A user starts the conversation by sending a message in the n8n chat interface.

### Workflow Steps

1.  **On new manual Chat Message:** Captures the user's input.
2.  **AI Agent:** A conversational agent receives the prompt. The system message instructs it to use its tools to find location coordinates before fetching weather, and to use Wikipedia for general information.
3.  **Ollama Chat Model:** The agent is powered by a local `llama3.2:latest` model running via Ollama.
4.  **Window Buffer Memory:** Maintains a history of the last 20 messages.
5.  **Weather HTTP Request (Tool):** A tool that calls the Open-Meteo API. The agent must provide the `latitude` and `longitude` to get the current temperature.
6.  **Wikipedia (Tool):** A standard LangChain tool that allows the agent to search for and retrieve summaries of Wikipedia articles.
7.  **Response Generation:** The agent synthesizes the information from the tools to answer the user's question.

---

## 197. 1/OpenAI_and_LLMs/AI Automated HR Workflow for CV Analysis and Candidate Evaluation.txt

**Workflow:** AI Automated HR Workflow for CV Analysis and Candidate Evaluation

This workflow automates the HR process of screening and evaluating job candidates. It triggers from a form submission, extracts data from the submitted CV using AI, summarizes the candidate's profile, evaluates it against a job description, and stores all the information in a Google Sheet.

### Trigger

- **Type:** n8n Form
- **Details:** A candidate applies for a job by submitting their name, email, and CV (PDF).

### Workflow Steps

1.  **On form submission:** Captures the applicant's data.
2.  **Upload CV:** Uploads the submitted CV to a specific folder in Google Drive.
3.  **Extract from File:** Extracts the full text content from the PDF CV.
4.  **Extract Personal Data (AI):** An Information Extractor chain (OpenAI) parses the CV text to pull out structured data like `telephone`, `city`, and `birthdate`.
5.  **Extract Qualifications (AI):** A second Information Extractor chain parses the CV text to get a summary of `Educational qualification`, `Job History`, and a bulleted list of `Skills`.
6.  **Merge Data:** The outputs from the two extractor chains are merged.
7.  **Summarization Chain (AI):** A summarization chain creates a concise, conversational summary of the candidate's entire profile based on the extracted data.
8.  **HR Expert Evaluation (AI):** A final AI chain acts as an "HR Expert." It receives the candidate's summary and a predefined job profile (`profile_wanted`). It is prompted to provide a `vote` (a score from 1-10) and a `consideration` (a textual motivation for the score).
9.  **Save to Google Sheets:** All the collected and generated data—including the original submission, extracted details, summary, and AI evaluation—is appended as a new row to a Google Sheet for review.

---

## 198. 1/OpenAI_and_LLMs/AI chat with any data source (using the n8n workflow tool).txt

**Workflow:** AI chat with any data source (using the n8n workflow tool)

This workflow demonstrates a powerful pattern where an AI agent can query any data source by using another n8n workflow as a custom tool. In this example, the agent is tasked with answering questions about Hacker News, and the tool it calls is a sub-workflow that fetches and processes data from the Hacker News API.

### Trigger

- **Type:** Manual Chat
- **Details:** A user asks a question about Hacker News in the chat interface.

### Workflow Steps

1.  **On new manual Chat Message:** Captures the user's question.
2.  **AI Agent (OpenAI):** A ReAct-style agent receives the prompt.
3.  **Custom Tool (`hn_tool`):** The agent is given a single tool, which is defined as another n8n workflow. The tool's description tells the agent that it "Returns a list of the most popular posts ever on Hacker News, in json format."
4.  **Sub-workflow Execution:** When the agent decides to use the tool, it triggers the sub-workflow:
    *   **Hacker News Node:** Fetches the top 50 posts from the Hacker News API.
    *   **Clean up data:** A Set node extracts and formats relevant fields like `title`, `points`, `url`, `created_at`, and `author`.
    *   **Stringify:** A Code node converts the array of cleaned-up post objects into a single JSON string.
5.  **Response Generation:** The agent receives the JSON string of Hacker News posts from the tool. It then uses this data to find the specific information needed to answer the user's original question and formulates a final response.
### 194. 1/OpenAI_and_LLMs/AI chatbot that can search the web.txt
- **Description:** This workflow creates a conversational AI agent capable of searching the web to answer user queries.
- **Trigger:** The workflow is initiated manually through a Chat Trigger.
- **Functionality:**
    1. **On new manual Chat Message:** The workflow starts when a user sends a message in the chat interface.
    2. **AI Agent:** The user's input is passed to an AI Agent.
    3. **Chat OpenAI:** The agent uses the `gpt-4o-mini` model to understand the query and generate responses.
    4. **Tools (SerpAPI & Wikipedia):** The agent is equipped with two tools: SerpAPI for performing real-time web searches and Wikipedia for looking up factual information. It can decide which tool to use based on the user's question.
    5. **Window Buffer Memory:** The agent maintains a conversation history of the last 20 messages, allowing it to understand context in an ongoing dialogue.
    6. **Response:** The agent uses the information gathered from its tools to formulate and return a comprehensive answer to the user.

### 195. 1/OpenAI_and_LLMs/AI Crew to Automate Fundamental Stock Analysis - Q&A Workflow.txt
- **Description:** This workflow automates fundamental stock analysis by first processing and storing financial documents (PDFs) and then providing a Q&A interface to query that data.
- **Trigger:** The workflow has two distinct parts with different triggers:
    1. **Data Ingestion:** Triggered manually to process and store a new financial document.
    2. **Q&A:** Triggered by a Webhook when a user asks a question about a specific company.
- **Functionality:**
    - **Part 1: Data Ingestion (Manual Trigger)**
        1. **Google Drive:** Downloads a specified PDF file (e.g., a company's financial report) from Google Drive.
        2. **Binary to Document:** Converts the PDF file into a text-based document.
        3. **Recursive Character Text Splitter:** Splits the document's text into smaller, manageable chunks.
        4. **Embeddings OpenAI:** Creates vector embeddings for each text chunk using an OpenAI model.
        5. **Qdrant Vector Store:** Inserts the generated embeddings into a Qdrant vector database under a specific collection name for that company.
    - **Part 2: Q&A (Webhook Trigger)**
        1. **Webhook:** Receives a POST request containing a user's `query` and the `company` they are asking about.
        2. **Retrieval QA Chain:** Manages the process of answering the query.
        3. **Vector Store Retriever:** Retrieves the most relevant text chunks from the Qdrant Vector Store by searching the collection corresponding to the specified `company`.
        4. **OpenAI Chat Model:** Uses the retrieved text chunks as context to generate a precise answer to the user's query.
        5. **Respond to Webhook:** Sends the final generated answer back as the response to the initial webhook request.

### 196. 1/OpenAI_and_LLMs/AI Customer feedback sentiment analysis.txt
- **Description:** This workflow automates the process of collecting and analyzing customer feedback. It captures submissions from a form, uses OpenAI to determine the sentiment, and logs the results in a Google Sheet.
- **Trigger:** The workflow starts when a user submits an n8n Form titled "Customer Feedback".
- **Functionality:**
    1. **Submit form with customer feedback:** A user fills out a form with their name, feedback category, feedback text, and contact information.
    2. **Classify feedback with OpenAI:** The text from the "Your feedback" field is sent to the OpenAI API with a prompt to classify its sentiment (e.g., positive, negative, neutral).
    3. **Merge sentiment with form content:** The sentiment returned by OpenAI is merged with the original data submitted in the form.
    4. **Add customer feedback to Google Sheets:** The complete, enriched data—including the original feedback, user details, and the AI-generated sentiment—is appended as a new row to a Google Sheet for tracking and analysis.

### 197. 1/OpenAI_and_LLMs/AI Data Extraction with Dynamic Prompts and Airtable.txt
- **Description:** A powerful, reactive workflow that uses an Airtable table as a dynamic front-end for AI-powered data extraction from PDFs. Users can define what data to extract simply by adding a description to a column in Airtable, which the workflow then uses as a prompt for an LLM.
- **Trigger:** The workflow is triggered by a webhook from Airtable, which fires on three event types: `row.updated`, `field.created`, or `field.updated`.
- **Functionality:**
    1. **Event Router:** A Switch node directs the workflow based on the event type from Airtable.
    2. **Get Table Schema:** The workflow fetches the schema of the Airtable table to identify which fields have a description. These descriptions are treated as dynamic prompts.
    3. **Scenario A: Row is Updated (`row.updated`)**
        - This typically happens when a user uploads a PDF to the 'File' field of a specific row.
        - The workflow identifies which columns in that row are empty but have a prompt (description).
        - For each of these columns, it downloads the PDF, extracts its text, and uses an OpenAI LLM Chain. The prompt for the LLM is the column's description (e.g., "Extract the total amount due").
        - The value returned by the LLM is then used to update the corresponding cell in that Airtable row.
    4. **Scenario B: Field is Created or Updated (`field.created` / `field.updated`)**
        - This occurs when a user adds a new column or changes the description (prompt) of an existing one.
        - The workflow iterates through *every row* in the table that contains a PDF.
        - It applies the new or updated prompt to each PDF, extracting the relevant data and populating the corresponding cell in every row.
    5. **Update Airtable:** The final extracted data is written back to the appropriate cells in the Airtable base.

### 198. 1/OpenAI_and_LLMs/AI Data Extraction with Dynamic Prompts and Baserow.txt
- **Description:** This workflow mirrors the functionality of the dynamic Airtable extraction template but is built for Baserow. It allows users to define data extraction tasks from PDFs by writing prompts in the descriptions of Baserow table fields.
- **Trigger:** A webhook that receives event notifications from a Baserow table, such as `rows.updated`, `field.created`, or `field.updated`.
- **Functionality:**
    1. **Event Router:** A Switch node routes the workflow based on the `event_type` received from the Baserow webhook.
    2. **Get Table Schema:** The workflow calls the Baserow API to fetch the table's schema and identify fields that have descriptions, which serve as the dynamic prompts.
    3. **Scenario A: Row is Updated (`rows.updated`)**
        - Triggered when a user modifies a row, typically by uploading a PDF to a 'File' field.
        - The workflow identifies which fields in that specific row need to be populated (i.e., are empty but have a prompt).
        - For each of these fields, it downloads the attached PDF, extracts the text, and feeds it to an OpenAI LLM Chain, using the field's description as the prompt.
        - The extracted values are collected and sent back to the Baserow API in a `PATCH` request to update the specific row.
    4. **Scenario B: Field is Created or Updated (`field.created` / `field.updated`)**
        - Triggered when a user adds a new field or modifies an existing field's description.
        - The workflow fetches *all rows* from the table that have a PDF file.
        - It then iterates through every row, applying the new extraction logic to populate the new or modified field across the entire table.
    5. **Update Baserow:** The extracted data is written back to the Baserow table via API calls.
### 199. 1/OpenAI_and_LLMs/AI Fitness Coach Strava Data Analysis and Personalized Training Insights.txt
- **Description:** This workflow acts as a personalized AI triathlon coach. It analyzes an athlete's activity data from Strava and provides motivational, data-driven feedback and improvement plans via email or WhatsApp.
- **Trigger:** The workflow is triggered when an athlete's activity is updated on Strava.
- **Functionality:**
    1. **Strava Trigger:** The workflow starts when an activity (run, swim, or bike) is updated.
    2. **Combine Everything:** The raw JSON data from the Strava activity is flattened into a single text string to be used as context for the AI.
    3. **Fitness Coach (AI Agent):** An AI Agent, powered by the Google Gemini Flash model, receives the activity data. The agent is given a detailed system prompt defining its persona as an expert triathlon coach. It is instructed to analyze performance metrics, provide tailored feedback, suggest improvement plans, and maintain a motivational tone.
    4. **Structure Output:** The text output from the AI agent is parsed and structured into headings, lists, and paragraphs for better readability.
    5. **Convert to HTML:** The structured text is converted into an HTML document.
    6. **Send Email/WhatsApp:** The final HTML-formatted coaching feedback is sent to the user via a standard email or a WhatsApp message.

### 200. 1/OpenAI_and_LLMs/AI Powered Web Scraping with Jina, Google Sheets and OpenAI _ the EASY way.txt
- **Description:** This workflow demonstrates a simplified approach to web scraping by combining Jina.ai for content fetching and OpenAI for structured data extraction, with the results saved to Google Sheets.
- **Trigger:** The workflow is triggered manually.
- **Functionality:**
    1. **Jina Fetch:** It makes an HTTP request to a Jina.ai reader URL (`r.jina.ai`), which fetches the content of a target webpage (in this case, a book catalogue). Jina simplifies scraping by returning the page content in a clean format.
    2. **Information Extractor:** The fetched content is passed to a LangChain Information Extractor node. This node uses an OpenAI Chat Model to extract specific pieces of information based on a provided JSON schema (title, price, availability, image_url, product_url).
    3. **Split Out:** The workflow splits the JSON array of extracted book data into individual items.
    4. **Save to Google Sheets:** Each item (representing a single book) is appended as a new row to a specified Google Sheet.

### 201. 1/OpenAI_and_LLMs/AI Social Media Caption Creator creates social media post captions in Airtable.txt
- **Description:** This workflow automates the creation of social media captions. It uses an AI agent to generate creative, audience-specific captions based on a briefing in an Airtable record and then updates that same record with the generated text.
- **Trigger:** The workflow is triggered when a record is updated in a specific Airtable view (likely filtered by a status like "Bitte formulieren" - "Please formulate").
- **Functionality:**
    1. **Airtable Trigger:** The workflow starts when a record is updated.
    2. **Get Airtable Record Data:** It fetches the full data for the triggering record.
    3. **AI Agent:** An AI Agent, powered by `gpt-4o`, is tasked with creating an Instagram caption.
        - **System Prompt:** The agent is given a detailed prompt to act as an expert caption creator. It must use a tool to get background info on the target audience and communication style.
        - **Input:** The agent receives the 'Briefing' text from the Airtable record.
    4. **Format Fields:** The output from the AI agent is formatted and placed into a field named "SoMe Text".
    5. **Post Caption into Airtable Record:** The workflow updates the original Airtable record, populating the "SoMe_Text_KI" field with the newly generated caption.

### 202. 1/OpenAI_and_LLMs/AI Voice Chat using Webhook, Memory Manager, OpenAI, Google Gemini & ElevenLabs.txt
- **Description:** This workflow creates a complete voice-based AI chatbot. It listens for an incoming voice message, transcribes it, uses an LLM to generate a response while maintaining conversation history, converts the text response back to audio, and sends it back.
- **Trigger:** The workflow is triggered by a Webhook that receives a POST request with a binary audio file (e.g., from a voice recorder app).
- **Functionality:**
    1. **Webhook:** Catches the incoming voice message.
    2. **OpenAI - Speech to Text:** The incoming audio data is sent to OpenAI's Whisper model to be transcribed into text.
    3. **Memory Management:**
        - **Get Chat:** Retrieves the previous conversation history using a Memory Manager node.
        - **Aggregate:** Combines the historical messages into a single context block.
    4. **Basic LLM Chain:** A Google Gemini model generates a response. It receives the transcribed user question and the aggregated conversation history to provide a context-aware answer.
    5. **Memory Management (Insert):** The new user question and the AI's response are inserted back into the memory to keep the conversation history updated.
    6. **ElevenLabs - Generate Audio:** The text response from the LLM is sent to the ElevenLabs API to be converted into a realistic voice audio file.
    7. **Respond to Webhook:** The generated binary audio data is sent back as the response to the initial webhook call.

### 203. 1/OpenAI_and_LLMs/AI Voice Chatbot with ElevenLabs & OpenAI for Customer Service and Restaurants.txt
- **Description:** This workflow creates a sophisticated voice-enabled RAG (Retrieval-Augmented Generation) chatbot, designed for use cases like customer service for a restaurant. It uses ElevenLabs for the voice interface and a Qdrant vector store for its knowledge base.
- **Trigger:** The workflow is initiated by a webhook, which is called by an ElevenLabs voice agent.
- **Functionality:**
    - **Part 1: Knowledge Base Setup (Manual Trigger)**
        1. **Create/Refresh Collection:** Manually trigger HTTP requests to create a new collection in Qdrant or clear an existing one.
        2. **Get Folder:** Fetches documents (e.g., menus, FAQs) from a specified Google Drive folder.
        3. **Download Files:** Downloads the files from Google Drive.
        4. **Data Loader & Splitter:** The documents are loaded and split into smaller chunks using a Token Splitter.
        5. **Embeddings & Storage:** OpenAI is used to create embeddings for the chunks, which are then inserted into the Qdrant vector store.
    - **Part 2: Voice Chat (Webhook Trigger)**
        1. **Listen (Webhook):** An ElevenLabs voice agent calls this webhook, sending the user's transcribed question in the request body.
        2. **AI Agent:** The user's question is passed to an AI Agent powered by an OpenAI model.
        3. **Vector Store Tool:** The agent is equipped with a tool that allows it to query the Qdrant vector store. It uses this tool to retrieve relevant information from the knowledge base to answer the user's question.
        4. **Window Buffer Memory:** The agent maintains conversation history to understand context.
        5. **Respond to ElevenLabs:** The agent's final text response is sent back via the `Respond to Webhook` node. ElevenLabs then converts this text to speech and speaks it to the user.
### 204. 1/OpenAI_and_LLMs/AI web researcher for sales.txt
- **Description:** This workflow automates the process of researching companies for sales purposes. It takes a company name or domain from a Google Sheet, uses an AI agent to find specific information online, and then updates the sheet with the enriched data.
- **Trigger:** The workflow can be triggered manually or on a schedule.
- **Functionality:**
    1. **Get rows to enrich:** It reads rows from a Google Sheet, filtering for those that need enrichment (e.g., where `enrichment_status` is not 'done').
    2. **Loop Over Items:** The workflow processes one company at a time.
    3. **AI Researcher Agent:** An AI Agent, powered by `gpt-4o`, is tasked with researching the company.
        - **Tools:** The agent has two tools:
            1. **SerpAPI:** To perform Google searches.
            2. **Get website content:** A sub-workflow that can visit a URL and extract its text content.
        - **Task:** The agent uses its tools to find information like the company's domain, LinkedIn URL, pricing, integrations, and case studies.
    4. **Structured Output Parser:** The agent's unstructured text output is parsed into a clean JSON object based on a predefined schema.
    5. **Google Sheets - Update Row:** The structured data is used to update the corresponding row in the original Google Sheet, and the `enrichment_status` is set to 'done'.

### 205. 1/OpenAI_and_LLMs/AI Youtube Trend Finder Based On Niche.txt
- **Description:** This workflow acts as a YouTube trend analysis tool. A user can chat with an AI agent, specify a niche, and the agent will search for recent, relevant, high-performing videos to identify current trends.
- **Trigger:** The workflow is initiated by a message from a user in a chat interface.
- **Functionality:**
    1. **Chat Trigger:** The workflow starts when a user sends a message.
    2. **AI Agent:** An AI Agent, powered by an OpenAI model, manages the conversation.
        - **System Prompt:** The agent is instructed to help creators find trending topics. It must first ask for a niche if one isn't provided.
        - **Tool (`youtube_search`):** The agent is equipped with a tool that is a sub-workflow. This tool searches YouTube for the top 3 most relevant videos from the last 48 hours based on a search term. It returns detailed data for each video (views, likes, comments, tags, etc.).
        - **Analysis:** The agent is instructed to call the tool multiple times with different search terms related to the niche, analyze the aggregated results to find patterns (in tags, titles, content), and provide an insightful summary of what is currently trending, rather than just listing the videos.
    3. **Window Buffer Memory:** The agent maintains a memory of the conversation to understand context across multiple messages.

### 206. 1/OpenAI_and_LLMs/AI_ Ask questions about any data source (using the n8n workflow retriever).txt
- **Description:** This workflow demonstrates how to use the `Workflow Retriever` to perform Question-Answering over data provided by another n8n workflow.
- **Trigger:** The workflow is triggered manually.
- **Functionality:**
    1. **Example Prompt:** A Set node provides a sample question: "What notes can you find for Jay Gatsby and what is his email address?"
    2. **Retrieval QA Chain:** This chain orchestrates the Q&A process.
    3. **Workflow Retriever:** This is the key component. It's configured to "retrieve" data from a different, specified n8n workflow. That target workflow would contain the data source (e.g., a database, a spreadsheet of contacts). The retriever effectively runs the other workflow and uses its output as the context for the Q&A.
    4. **OpenAI Chat Model:** An OpenAI model takes the user's question and the context provided by the `Workflow Retriever` to generate a final answer.

### 207. 1/OpenAI_and_LLMs/AI_ Summarize podcast episode and enhance using Wikipedia.txt
- **Description:** This workflow creates a detailed "digest" of a podcast episode. It summarizes a provided transcript, extracts key topics and questions, enriches the topics with information from Wikipedia, and emails the final digest.
- **Trigger:** The workflow is triggered manually.
- **Functionality:**
    1. **Podcast Episode Transcript:** A Code node provides the full text transcript of a podcast episode.
    2. **Summarize Transcript:** The transcript is chunked and fed into a `refine` summarization chain using GPT-3.5 to create a concise summary.
    3. **Extract Topics & Questions:** The summary is then passed to a GPT-4 LLM Chain. Using a structured output parser, it extracts a list of key topics discussed and a list of interesting questions to ponder, based on the summary.
    4. **Research & Explain Topics (AI Agent):** The workflow loops through each extracted topic. An AI Agent, equipped with a Wikipedia tool, is asked to research and explain each topic within the context of the podcast summary.
    5. **Format topic text & title:** The enriched topic explanations, the original summary, and the questions are formatted into a clean HTML structure.
    6. **Send Digest:** The final HTML digest is sent as an email via Gmail.

### 208. 1/OpenAI_and_LLMs/AI-Driven Lead Management and Inquiry Automation with ERPNext & n8n.txt
- **Description:** This workflow automates the initial processing of new leads coming from a website into an ERPNext system. It uses an AI agent to analyze the lead's inquiry, find the correct internal contact, and draft a notification email.
- **Trigger:** A webhook receives a notification from ERPNext when a new Lead is created with the source "Website" and status "Open".
- **Functionality:**
    1. **Webhook & Filters:** The workflow starts when a new lead is created in ERPNext, and IF nodes filter for leads from the "Website" source with an "Open" status and that have notes.
    2. **Customer Lead AI Agent:** An AI Agent, powered by an OpenAI model, analyzes the lead's details (name, company, notes, etc.).
        - **Tools:** The agent is given access to several tools to gather context:
            - Google Sheets tools to look up abbreviations and a contact database.
            - Google Docs tools to read company profiles and policies.
        - **Task:** The agent's prompt instructs it to analyze the lead's notes, determine which product/service is being inquired about, use its tools to find the responsible employee(s) from the contact database, and draft a system notification email. If the lead is invalid (e.g., a job application), it should state that.
    3. **Parse Output:** The agent's text output, which contains the email address, subject, and body, is parsed into separate fields.
    4. **Format Email:** The email body is converted into a clean HTML format.
    5. **Send Email:** The drafted notification email is sent to the correct internal contact(s) via Microsoft Outlook, including a direct link back to the Lead record in ERPNext.
### 209. 1/OpenAI_and_LLMs/AI-Generated Summary Block for WordPress Posts.txt
- **Description:** This workflow automates the process of adding a styled "AI Summary" block to WordPress posts. It fetches posts, checks if they've already been processed, generates a summary using OpenAI, updates the post, logs the action in Google Sheets, and sends a Slack notification.
- **Trigger:** The workflow can be triggered manually for testing, on a schedule (e.g., every 30 seconds to check for new posts), or via a webhook when a post is published.
- **Functionality:**
    1. **Get Posts:** Retrieves recent posts from WordPress.
    2. **Check for Existing Summary:** For each post, it checks a Google Sheet to see if a summary has already been generated for that post ID to prevent duplication.
    3. **Classify Content:** It uses an OpenAI text classifier to double-check if the post content already contains the summary block.
    4. **Generate Summary:** If no summary exists, the post's HTML content is converted to Markdown and sent to an OpenAI model with a detailed prompt to generate a concise, bullet-point summary within a specific HTML structure.
    5. **Update WordPress Post:** The generated HTML summary block is prepended to the existing content of the WordPress post via an API call.
    6. **Log to Google Sheets:** A new row is added to a Google Sheet with the post ID, a link to the post, and the date of summarization.
    7. **Notify on Slack:** A message is sent to a designated Slack channel, notifying the team that a new post has been updated with an AI summary and providing a direct link to view it.

### 210. 1/OpenAI_and_LLMs/AI-Powered Candidate Shortlisting Automation for ERPNext.txt
- **Description:** This workflow automates the screening process for job applicants in ERPNext. When a new applicant is added, the workflow analyzes their attached resume against the job description, scores them, and updates their status in ERPNext.
- **Trigger:** A webhook from ERPNext that fires when a new "Job Applicant" document is created.
- **Functionality:**
    1. **Webhook and Filters:** The workflow starts upon receiving the webhook, then uses IF nodes to ensure the applicant has an attached resume and has applied for a specific job opening. If not, their status is updated to "Rejected" or "Hold".
    2. **Get Job Opening Data:** It fetches the details of the "Job Opening" document from ERPNext to get the full job description.
    3. **Download Resume:** It downloads the applicant's resume file from the provided link.
    4. **Extract Text:** The resume (PDF) is converted into plain text.
    5. **AI Agent Analysis:** An AI Agent (powered by Google Gemini) is given a prompt to act as a recruitment specialist. It receives the job description and the applicant's resume text and is tasked with evaluating the candidate's suitability.
    6. **Parse AI Output:** The agent's response, which includes a "FitLevel", "Score", and "Justification", is parsed into separate fields.
    7. **Update ERPNext with AI Analysis:** The `applicant_rating`, `justification_by_ai`, `fit_level`, and `score` fields are updated on the applicant's record in ERPNext.
    8. **Accept/Reject Based on Score:** An IF node checks the AI-generated score. If the score is 80 or above, the applicant's status is updated to "Accepted"; otherwise, it's updated to "Rejected".

### 211. 1/OpenAI_and_LLMs/AI-Powered Email Automation for Business_ Summarize & Respond with RAG.txt
- **Description:** A sophisticated email automation workflow that uses a RAG (Retrieval-Augmented Generation) pipeline to handle incoming business inquiries. It reads, summarizes, and classifies emails, then uses a knowledge base to draft and send context-aware replies.
- **Trigger:** An IMAP trigger that activates when a new email is received.
- **Functionality:**
    - **Part 1: Knowledge Base Setup (Manual)**
        1.  Documents (e.g., company info, product details) are loaded from Google Drive.
        2.  The documents are chunked, embedded using OpenAI, and stored in a Qdrant vector store to create a searchable knowledge base.
    - **Part 2: Email Processing and Response (Triggered)**
        1. **Email Trigger (IMAP):** Fetches a new incoming email.
        2. **Summarize & Classify:** The email body is summarized, and a text classifier determines its category (e.g., "Company info request").
        3. **AI Agent (Drafting):** If the email is a valid request, an AI Agent is tasked with writing a reply.
            - **Tool (RAG):** The agent is equipped with a tool connected to the Qdrant vector store. It uses this tool to retrieve relevant information from the knowledge base to answer the specific inquiry in the email.
        4. **AI Agent (Review):** The drafted email is passed to a second LLM chain for review and formatting into clean HTML.
        5. **Send Email:** The final, reviewed email is sent back to the original sender.

### 212. 1/OpenAI_and_LLMs/AI-Powered RAG Workflow For Stock Earnings Report Analysis.txt
- **Description:** This workflow provides a powerful RAG (Retrieval-Augmented Generation) system for financial analysis. It ingests quarterly earnings reports (PDFs) into a vector store and then uses an AI agent to analyze the data and generate a detailed report in Google Docs.
- **Trigger:** The data ingestion is manual, while the analysis part is triggered manually by a user prompt.
- **Functionality:**
    - **Part 1: Data Ingestion (Manual)**
        1. **List Of Files:** A Google Sheet contains links to Google Drive PDFs of company earnings reports.
        2. **Download & Process:** The workflow loops through the list, downloads each PDF, loads it as a document, and splits it into smaller text chunks.
        3. **Embed & Store:** It uses Google Gemini's embedding model to create vector embeddings for each chunk and inserts them into a Pinecone vector store.
    - **Part 2: Report Generation (Manual Trigger)**
        1. **AI Agent:** An AI Agent, acting as a skilled financial analyst, is given a prompt (e.g., "Give me a report on Google's last 3 quarter earnings").
        2. **Tools:** The agent is equipped with two tools:
            - **Vector Store Tool:** To retrieve relevant financial data from the earnings reports stored in Pinecone.
            - **Google Docs Tool:** To write the final report.
        3. **Analysis & Synthesis:** The agent uses the vector store to find the necessary data, analyzes trends and key metrics, and synthesizes the information.
        4. **Save Report to Google Docs:** The agent uses its tool to write a structured, professional financial report directly into a specified Google Doc.

### 213. 1/OpenAI_and_LLMs/AI-Powered Social Media Amplifier.txt
- **Description:** This workflow automates a content amplification strategy by finding interesting GitHub projects on Hacker News, generating unique posts for Telegram, Twitter, and LinkedIn, and then publishing them. It uses Airtable to track posted content to avoid duplicates.
- **Trigger:** A schedule trigger that runs periodically (e.g., every 4 hours).
- **Functionality:**
    1. **Crawl Hacker News:** An HTTP Request node scrapes the Hacker News homepage.
    2. **Extract GitHub Posts:** A Python script using BeautifulSoup parses the HTML to find and extract metadata for all posts linking to GitHub repositories.
    3. **Filter Unposted Items:** The workflow checks an Airtable base to see which of the newly scraped posts have already been processed and filters them out.
    4. **Generate Social Posts (AI Agent):** For each new GitHub link, the workflow does the following:
        - **Visit GH Page:** It scrapes the content of the GitHub repository's main page.
        - **AI Agent:** An AI Agent is prompted to act as a "Social Media Manager." It receives the GitHub page content and is tasked with creating three distinct posts: a concise one for Twitter, a professional one for LinkedIn, and an engaging one for Telegram.
    5. **Publish Posts:** The generated content is published to the respective platforms (Telegram, Twitter, LinkedIn).
    6. **Update Airtable:** After each successful post, the Airtable base is updated to mark the item as "Done" for that specific platform, preventing future reposts.
### 214. 1/OpenAI_and_LLMs/AI-powered WooCommerce Support-Agent.txt
- **Description:** This workflow creates an AI-powered support agent for a WooCommerce store. The agent can help customers by retrieving their order history and tracking shipment information from DHL.
- **Trigger:** The workflow is initiated by a chat message, likely from a website chat widget.
- **Functionality:**
    1. **Find WooCommerce User:** The workflow first gets the user's email address from the chat input. It then queries the WooCommerce API to find the corresponding customer ID.
    2. **Get Orders:** If a user is found, it retrieves all past orders for that customer ID.
    3. **Extract Tracking Data:** For each order, it checks for shipment tracking metadata.
    4. **Query DHL:** If DHL tracking numbers are found, it queries the DHL API to get the latest shipment status for each package.
    5. **AI Agent:** All the collected data (user info, order history, tracking status) is passed to an AI Agent. The agent is prompted to act as a helpful customer support representative for the specific store, using the provided data to answer the user's questions about their orders or shipments.
    6. **Conversation Memory:** A Window Buffer Memory node is used to maintain the context of the conversation, allowing for follow-up questions.

### 215. 1/OpenAI_and_LLMs/Ask a human for help when the AI doesn_t know the answer.txt
- **Description:** This workflow demonstrates a "human-in-the-loop" pattern. It sets up an AI agent that can answer questions but is also equipped with a special tool to ask for human help when it's not confident in its answer.
- **Trigger:** The main workflow is triggered by a user message in a chat interface.
- **Functionality:**
    1. **AI Agent:** A user interacts with an AI agent. The agent is instructed to use the `dont_know_tool` if it cannot answer a question.
    2. **Custom Tool (`dont_know_tool`):** This tool is a sub-workflow within the main workflow. When the agent calls this tool, it triggers the sub-workflow.
    3. **Sub-workflow Logic:**
        - **Check for Email:** The sub-workflow first checks if the user's original query contains an email address.
        - **If No Email:** It responds to the user, asking them to repeat their question and provide an email address.
        - **If Email Provided:** It sends a message to a designated Slack channel, notifying a human support team that a user needs help and providing the user's original message. It then responds to the user, letting them know that a human has been contacted.

### 216. 1/OpenAI_and_LLMs/Automate Customer Support Issue Resolution using AI Text Classifier.txt
- **Description:** This workflow automates the management of Jira support tickets. It periodically scans for old, unresolved issues, uses an AI agent to analyze the conversation thread, and takes appropriate action, such as providing a solution, sending a reminder, or closing the ticket.
- **Trigger:** A schedule trigger that runs periodically (e.g., daily).
- **Functionality:**
    1. **Get Old Issues:** The workflow fetches a list of Jira issues that are still in "To Do" or "In Progress" and were created more than 7 days ago.
    2. **Analyze Issue Thread:** For each issue, it retrieves all comments and simplifies the thread for an AI to process.
    3. **KnowledgeBase Agent:** An AI agent analyzes the entire issue thread (title, description, comments).
        - **Task:** The agent determines if a solution has been found in the conversation. It also provides a short summary of the issue and a suggested response.
        - **Output:** The agent's findings are structured into a JSON object with `solution_found` (boolean), `short_summary_of_issue`, and `response`.
    4. **Decision Logic (IF nodes):**
        - **If Solution Found:** The agent's suggested response is posted as a comment on the Jira issue, and the issue is closed.
        - **If No Solution & Last Comment is from User:** The workflow assumes the support team needs to respond. It sends a notification to a Slack channel with the issue summary, alerting the team to the "zombie ticket".
        - **If No Solution & Last Comment is from Bot:** The workflow assumes the user needs to respond. It posts an automated reminder comment on the Jira issue.

### 217. 1/OpenAI_and_LLMs/Automate Image Validation Tasks using AI Vision.txt
- **Description:** This workflow uses a multimodal AI vision model to automate the validation of images against a set of specific criteria, using passport photos as an example.
- **Trigger:** The workflow is triggered manually.
- **Functionality:**
    1. **Import Photos:** A Set node provides a list of URLs for portrait photos stored in Google Drive.
    2. **Download and Resize:** The workflow loops through the list, downloads each photo, and resizes it to a standard dimension (1024x1024) suitable for the AI model.
    3. **Passport Photo Validator (LLM Chain):** The core of the workflow. It uses a Google Gemini 1.5 Pro vision model.
        - **System Prompt:** The model is given a detailed system prompt containing the complete, official UK government rules for passport photos (e.g., plain background, no shadows, neutral expression, eyes open).
        - **Input:** The resized image is provided as binary data to the model.
    4. **Structured Output Parser:** The model is instructed to return its analysis in a specific JSON format, indicating if the photo `is_valid` (boolean), providing a `photo_description`, and listing the `reasons` for invalidity if applicable.

### 218. 1/OpenAI_and_LLMs/Automate Your RFP Process with OpenAI Assistants.txt
- **Description:** This workflow automates the tedious process of responding to a Request for Proposal (RFP). It receives an RFP document, uses an LLM to extract all the questions, and then leverages a pre-trained OpenAI Assistant to answer each question based on company knowledge.
- **Trigger:** A webhook that receives an API request containing the RFP document.
- **Functionality:**
    1. **Webhook Trigger:** A user submits the RFP (as a PDF) via an API call.
    2. **Extract RFP Data:** The text content is extracted from the PDF.
    3. **Create Response Document:** A new Google Doc is created to hold the generated answers for this specific RFP.
    4. **Extract Questions From RFP:** An LLM chain is used to read through the entire RFP text and extract a clean list of all the questions being asked.
    5. **Answer Questions (Loop):** The workflow loops through each extracted question one by one.
        - **OpenAI Assistant:** For each question, it calls an OpenAI Assistant. This Assistant has been pre-configured and given files (e.g., marketing materials, technical specifications) containing knowledge about the company.
        - **Generate Answer:** The Assistant uses its knowledge base to generate an appropriate answer for the current question.
    6. **Record Question & Answer:** The original question and the AI-generated answer are appended to the Google Doc created in step 3.
    7. **Notify Team:** Once all questions have been answered, the workflow sends a notification to the sales team via both email (Gmail) and Slack, letting them know the draft RFP response is ready for review.
### 219. 1/OpenAI_and_LLMs/Chat Assistant (OpenAI assistant) with Postgres Memory And API Calling Capabalities.txt
- **Description:** This workflow creates a sophisticated, tool-enabled chatbot using an OpenAI Assistant. It maintains conversation history in a PostgreSQL database and can interact with external APIs and a MySQL database to answer user queries.
- **Trigger:** A public-facing Chat Trigger, which can be embedded on a website.
- **Functionality:**
    1. **Chat Trigger & Initial Data:** The workflow starts when a user sends a message. It can also receive initial `leadData` (name, age, city, etc.) to pre-populate the conversation.
    2. **Postgres Chat Memory:** It uses a PostgreSQL database to store and retrieve the conversation history for each user session, allowing for long-term memory.
    3. **OpenAI Assistant:** The user's input, along with the conversation history, is sent to a pre-configured OpenAI Assistant.
    4. **Tools:** The Assistant is equipped with several powerful tools:
        - **External API:** Can make POST requests to an external API (e.g., to find user information by name and birthdate).
        - **Knowledge Base:** Can make GET requests to another API to fetch knowledge base articles.
        - **Products in Database:** Can query a MySQL database to find product information based on parameters extracted from the user's query (e.g., city, age, number of people).
    5. **Response Generation:** The Assistant uses the appropriate tool(s) to gather the necessary information and formulates a comprehensive response.
    6. **Update Memory:** The new user message and the AI's response are saved back to the PostgreSQL database.

### 220. 1/OpenAI_and_LLMs/Chat with local LLMs using n8n and Ollama.txt
- **Description:** This workflow provides a simple way to create a chat interface for a locally hosted Large Language Model (LLM) using Ollama.
- **Trigger:** A chat message is received through the n8n chat interface.
- **Functionality:**
    1. **When chat message received:** The workflow is initiated by a user's message.
    2. **Chat LLM Chain:** The user's input is sent to a Chat LLM Chain.
    3. **Ollama Chat Model:** This chain is configured to use the Ollama Chat Model, which connects to a locally running Ollama server (e.g., `http://localhost:11434`).
    4. **Response:** The local LLM processes the input and generates a response, which is then sent back to the user in the chat interface.

### 221. 1/OpenAI_and_LLMs/Chat with OpenAI Assistant (by adding a memory).txt
- **Description:** This workflow demonstrates how to add persistent memory to an OpenAI Assistant, which natively manages its own memory within a single thread but loses it across different workflow executions. This pattern allows for continuous conversations over time.
- **Trigger:** A chat message from the n8n chat interface.
- **Functionality:**
    1. **Chat Trigger:** A user sends a message.
    2. **Chat Memory Manager (Get):** The workflow first retrieves the past conversation history for the current user session from n8n's built-in memory.
    3. **Aggregate:** It combines all past messages into a single block of text.
    4. **OpenAI Assistant:** The user's current message is prepended with the entire aggregated conversation history and sent to the OpenAI Assistant. This gives the Assistant the full context of the conversation so far.
    5. **Chat Memory Manager (Insert):** The user's latest message and the Assistant's new response are saved back into the memory, ensuring the context is available for the next interaction.
    6. **Response:** The Assistant's output is sent back to the user in the chat.

### 222. 1/OpenAI_and_LLMs/Configure your own Image Creation API Using OpenAI DALLE-3.txt
- **Description:** This workflow turns n8n into a simple, personal API for generating images using OpenAI's DALL-E 3 model.
- **Trigger:** A Webhook that receives a GET request.
- **Functionality:**
    1. **Webhook:** The workflow is triggered by accessing a specific URL. The image prompt is passed as a URL query parameter (e.g., `?input=a%20white%20siamese%20cat`).
    2. **OpenAI:** The `input` text from the webhook's query is passed directly to the OpenAI node, which is configured to use the image generation resource (DALL-E).
    3. **Respond to Webhook:** The raw binary data of the generated image is sent back as the direct response to the webhook request. This means the image will render directly in the browser or can be consumed by any application that calls the URL.

### 223. 1/OpenAI_and_LLMs/Convert text to speech with OpenAI.txt
- **Description:** This workflow demonstrates how to use OpenAI's Text-to-Speech (TTS) API to convert a string of text into an audio file.
- **Trigger:** The workflow is triggered manually.
- **Functionality:**
    1. **Set input text and TTS voice:** A Set node defines the `input_text` to be converted and the desired `voice` (e.g., "alloy", "echo", "fable").
    2. **Send HTTP Request to OpenAI's TTS Endpoint:** An HTTP Request node makes a POST call to the `https://api.openai.com/v1/audio/speech` endpoint.
        - **Body:** The request body includes the `model` ("tts-1"), the `input` text, and the selected `voice`.
        - **Authentication:** It uses an OpenAI API key for authorization.
    3. **Output:** The workflow outputs the binary data for the generated MP3 audio file.
### 224. 1/OpenAI_and_LLMs/Create a Branded AI-Powered Website Chatbot.txt
- **Description:** This workflow creates a fully functional, branded AI assistant for a website, designed to act as an intelligent personal assistant for a company founder. It can check calendar availability, book meetings, and escalate complex inquiries to a human.
- **Trigger:** A public-facing webhook designed to be used with a website chat widget.
- **Functionality:**
    1. **AI Agent:** The core of the workflow is an AI Agent powered by `gpt-4o`. It's given a detailed persona as a professional executive PA for a founder named Wayne.
    2. **Conversation Memory:** A Window Buffer Memory node ensures the conversation is persistent and context-aware across multiple user messages.
    3. **Tools for Action:** The agent is equipped with three powerful tools that are implemented as separate sub-workflows:
        - **`Get_availability`:** When asked about availability, the agent triggers a sub-workflow that queries the user's Microsoft Calendar for the next 14 days, calculates free slots within business hours, and returns them to the agent.
        - **`Make_Appointment`:** Once a time is agreed upon, the agent uses this tool to create a new event in the Microsoft Calendar, inviting the customer and setting up a Microsoft Teams meeting.
        - **`Send_email`:** If the user isn't ready to book or has a complex query, the agent uses this tool to send a detailed email notification to the founder.
    4. **Dynamic Response:** The agent intelligently decides which tool to use based on the conversation, creating a natural and effective user experience for booking meetings or making inquiries.

### 225. 1/OpenAI_and_LLMs/Custom LangChain agent written in JavaScript.txt
- **Description:** This workflow is a technical demonstration for developers, showcasing how to create custom LangChain components using the n8n Code node.
- **Trigger:** The workflow is triggered manually.
- **Functionality:**
    1. **Custom LLM Chain:** The first part shows how to write JavaScript code within a Code node to create a basic LLM Chain. It takes a prompt and an LLM connection as inputs and executes the chain, demonstrating programmatic control over LangChain primitives.
    2. **Custom Tool:** The second part demonstrates how to create a custom tool from scratch. The example wraps the `WikipediaQueryRun` function from the LangChain library, making it available as a tool for an AI agent within the n8n environment. This allows developers to integrate any custom logic or external API as a tool for their agents.

### 226. 1/OpenAI_and_LLMs/Daily meetings summarization with Gemini AI.txt
- **Description:** This workflow acts as an automated executive assistant that provides a daily summary of all calendar events.
- **Trigger:** A schedule trigger that runs every day at a specified time (e.g., 9 AM).
- **Functionality:**
    1. **Calendar AI Agent:** The workflow is driven by an AI Agent powered by Google's Gemini 1.5 Flash model.
    2. **System Prompt:** The agent is instructed to summarize the day's meetings. The current date is dynamically injected into the prompt for context.
    3. **Google Calendar Tool:** The agent is equipped with a tool that can get events from a specified Google Calendar. When triggered, the agent uses this tool to fetch all of today's meetings.
    4. **Summarization:** The agent receives the list of events and generates a concise summary of the day's schedule.
    5. **Slack Notification:** The final summary generated by the AI is posted as a message to a designated Slack channel, keeping the user informed of their daily agenda.

### 227. 1/OpenAI_and_LLMs/Daily Podcast Summary.txt
- **Description:** This workflow automates the creation of a daily email digest of the top podcasts in a specific genre. It fetches popular episodes, transcribes them, summarizes the content, and sends a formatted HTML email.
- **Trigger:** A schedule trigger that runs daily.
- **Functionality:**
    1. **Get Top Podcasts:** It makes a POST request to the Taddy GraphQL API to get a list of the top 10 trending podcast episodes for a specified genre (e.g., TECHNOLOGY).
    2. **Download and Transcribe:** The workflow loops through each episode:
        - It downloads the audio file from the provided URL.
        - It uses an external service (Aspose.app) to crop the audio to a manageable length.
        - The cropped audio is sent to OpenAI's Whisper API for transcription.
    3. **Summarize Podcast:** The generated transcript is then sent to an OpenAI model (`gpt-4o-mini`) with a prompt to summarize the key points in 3-4 paragraphs.
    4. **Aggregate and Format:** The results for all processed podcasts (podcast name, episode name, URL, and AI summary) are aggregated.
    5. **Generate HTML:** The aggregated data is formatted into a clean HTML table.
    6. **Send Email:** The final HTML digest is sent to the user via Gmail.

### 228. 1/OpenAI_and_LLMs/Detect hallucinations using specialised Ollama model bespoke-minicheck.txt
- **Description:** This workflow provides a sophisticated fact-checking pipeline to detect hallucinations or factual inaccuracies in a given text by comparing it against a source document.
- **Trigger:** The workflow can be triggered manually or executed by another workflow.
- **Functionality:**
    1. **Input:** The workflow takes two inputs: a `facts` document (the source of truth) and a `text` document (the article or claim to be checked).
    2. **Sentence Splitting:** The `text` to be checked is split into individual sentences.
    3. **Fact-Checking with Ollama:** The workflow loops through each sentence and uses a specialized, locally-hosted Ollama model called `bespoke-minicheck`. For each sentence ("claim"), it asks the model to verify it against the `facts` document. The model responds with a simple "Yes" or "No".
    4. **Filter Incorrect Statements:** The workflow filters the results to isolate only the sentences that were marked as "No" (incorrect).
    5. **Generate Summary Report:** The list of incorrect statements is passed to another LLM (Ollama `qwen2.5:1.5b`) which is prompted to generate a structured summary, including a count of errors, a list of the incorrect statements, and a final assessment of the article's factual accuracy.
### 229. 1/OpenAI_and_LLMs/Dynamically generate a webpage from user request using OpenAI Structured Output (1).txt
- **Description:** This workflow is an experimental demonstration of using OpenAI's Structured Output (JSON Schema mode) to dynamically generate a complete HTML webpage based on a simple user query.
- **Trigger:** A webhook that accepts a `query` parameter (e.g., `?query=a%20signup%20form`).
- **Functionality:**
    1. **Webhook:** Receives a user's request for a webpage.
    2. **OpenAI - Using Structured Output:** An HTTP Request node makes a call to the OpenAI Chat Completions API.
        - **System Prompt:** The model (`gpt-4o`) is instructed to act as a UI designer and copywriter.
        - **Response Format:** Crucially, the `response_format` is set to `json_schema`. A detailed JSON schema is provided that defines the structure of a webpage with nested components (div, p, h1, button, etc.) and attributes (like Tailwind CSS classes).
        - **Output:** OpenAI is forced to return a JSON object that conforms perfectly to the provided schema, representing the entire webpage structure.
    3. **OpenAI - JSON to HTML:** The structured JSON from the previous step is passed to a second OpenAI call. This model is prompted to convert the JSON structure into a single, clean HTML string.
    4. **Format the HTML result:** The generated HTML is embedded into a full HTML document structure, including the Tailwind CSS script tag.
    5. **Respond to Webhook:** The final, complete HTML is sent back as the response, which renders the generated webpage directly in the user's browser.

### 230. 1/OpenAI_and_LLMs/Dynamically generate a webpage from user request using OpenAI Structured Output.txt
- **Description:** This workflow is identical to the previous one, demonstrating the use of OpenAI's Structured Output feature to generate a webpage from a user prompt.
- **Trigger:** A webhook that accepts a `query` parameter.
- **Functionality:**
    1. **Webhook:** Receives a user's request for a webpage.
    2. **OpenAI - Using Structured Output:** An HTTP Request node calls the OpenAI API with a prompt and a strict JSON schema defining UI components and attributes.
    3. **OpenAI - JSON to HTML:** A second OpenAI call converts the structured JSON response into a flat HTML string.
    4. **Format the HTML result:** The HTML string is placed within a complete HTML document, including a `<script>` tag for Tailwind CSS.
    5. **Respond to Webhook:** The final HTML is returned, rendering the dynamically generated page in the browser.

### 231. 1/OpenAI_and_LLMs/Easy Image Captioning with Gemini 1.5 Pro.txt
- **Description:** This workflow showcases how to use a multimodal AI model (Google Gemini 1.5 Pro) to generate a descriptive caption for an image and then overlay that caption directly onto the image.
- **Trigger:** The workflow is triggered manually.
- **Functionality:**
    1. **Get Image:** An HTTP Request node downloads a sample image from a URL.
    2. **Image Captioning Agent:** A LangChain LLM Chain is configured to use the Gemini 1.5 Pro vision model.
        - **Input:** The downloaded image is passed as binary data to the model.
        - **Prompt:** The model is prompted to generate a "punny" caption title and a descriptive caption text for the image.
        - **Structured Output:** A parser ensures the output is a clean JSON object with `caption_title` and `caption_text`.
    3. **Calculate Positioning:** A Code node calculates the correct coordinates and font size to position the caption at the bottom of the image, accounting for the image's dimensions and the length of the text.
    4. **Apply Caption to Image:** The Edit Image node performs a multi-step operation:
        - First, it draws a semi-transparent black rectangle at the bottom of the image to act as a background for the text.
        - Second, it overlays the generated caption text on top of the rectangle.
    5. **Output:** The final output is the modified image with the AI-generated caption embedded.

### 232. 1/OpenAI_and_LLMs/Enrich FAQ sections on your website pages at scale with AI.txt
- **Description:** This is a large-scale content generation workflow designed to automatically create comprehensive FAQ pages for various n8n integrations. It reads lists of integrations from a Google Sheet, uses pre-defined templates to generate question-answer pairs, enriches them with AI, and saves the final content as JSON files in Google Drive.
- **Trigger:** The workflow is triggered manually.
- **Functionality:**
    1. **Define Sheets:** The workflow starts by defining a list of Google Sheet tabs to process (e.g., "Single Integration Native", "Categories").
    2. **Loop Through Sheets:** It loops through each sheet name.
    3. **Get Services:** For each sheet, it fetches all the rows (e.g., all native integrations, all categories).
    4. **Loop Through Services:** It then loops through each individual service/category.
    5. **Generate Q&A Template:** A Set node uses a JavaScript switch statement to select the appropriate Q&A template based on the sheet name. These templates contain pre-written questions and partial answers, with placeholders for the specific service name (e.g., `How can I set up {{ $json.data.displayName }} integration in n8n?`).
    6. **AI Completion:** For questions marked with `ai_completion: true`, the workflow calls an OpenAI model (`gpt-4o-mini`) to generate the rest of the answer, providing context from the question and the partial answer.
    7. **Aggregate and Format:** All the generated Q&A pairs for a service are aggregated.
    8. **Save to Google Drive:** The final JSON object containing the list of questions and answers is saved as a new file in a designated Google Drive folder.

### 233. 1/OpenAI_and_LLMs/Extract personal data with self-hosted LLM Mistral NeMo.txt
- **Description:** This workflow demonstrates how to use a self-hosted LLM (Mistral NeMo via Ollama) to perform structured data extraction from unstructured text, with a built-in auto-fixing mechanism to ensure reliable JSON output.
- **Trigger:** A chat message is received via the n8n chat interface.
- **Functionality:**
    1. **Chat Trigger:** A user provides a piece of text (e.g., "Contact John Doe at john.doe@example.com to discuss the project proposal tomorrow.").
    2. **Basic LLM Chain:** The text is sent to a local Ollama model (`mistral-nemo`).
        - **Structured Output Parser:** The chain is configured with a `StructuredOutputParser` that expects a specific JSON schema (name, surname, commtype, contacts, timestamp, subject).
    3. **Auto-fixing Output Parser:** This is the key component. The `Basic LLM Chain` is wrapped in an `Auto-fixing Output Parser`. If the LLM's initial response doesn't perfectly match the required JSON schema, the auto-fixer automatically calls the LLM again with a new prompt, telling it to correct its previous output based on the parsing error. This significantly improves the reliability of getting structured data from the LLM.
    4. **Output:** The final, validated JSON object with the extracted personal data.
### 234. 1/OpenAI_and_LLMs/Fetch Dynamic Prompts from GitHub and Auto-Populate n8n Expressions in Prompt.txt
- **Description:** This workflow demonstrates a dynamic prompting technique where a prompt template is fetched from a GitHub repository, and its placeholders are automatically filled with values from the workflow's context.
- **Trigger:** The workflow is triggered manually.
- **Functionality:**
    1. **Set Variables:** A Set node defines several variables, such as `company`, `product`, `features`, and the details of the GitHub repository (`Account`, `repo`, `path`, `prompt` file name).
    2. **Fetch Prompt from GitHub:** A GitHub node retrieves the content of a specified markdown file (e.g., `keyword_research.md`) from a public repository. This file contains the prompt template with placeholders like `{{ company }}`.
    3. **Check for Missing Variables:** A Code node parses the fetched prompt to find all `{{...}}` placeholders. It then compares this list against the variables defined in the `setVars` node.
    4. **Error Handling:** If any placeholders in the prompt do not have a corresponding variable in the `setVars` node, the workflow stops and throws an error listing the missing keys.
    5. **Replace Variables:** If all variables are present, another Code node dynamically replaces the placeholders in the prompt template with their corresponding values.
    6. **AI Agent:** The final, populated prompt is sent to an AI Agent (powered by an Ollama Chat Model) for execution.

### 235. 1/OpenAI_and_LLMs/Flux AI Image Generator.txt
- **Description:** This workflow provides a public-facing web form that allows users to generate images using the FLUX.1-schnell model hosted on Hugging Face. It offers several pre-defined artistic styles.
- **Trigger:** An n8n Form Trigger that serves a web page with a prompt input and a style dropdown.
- **Functionality:**
    1. **n8n Form Trigger:** A user submits a text prompt and selects a style (e.g., "Hyper-Surreal Escape", "AI Dystopia", "Neon Fauvism").
    2. **Route by Style:** A Switch node routes the workflow based on the selected style.
    3. **Set Style Prompt:** Each route leads to a Set node that defines a detailed `stylePrompt` containing specific artistic instructions and parameters (e.g., `golden ratio, rule of thirds, cyberpunk, glitch art, octane render`).
    4. **Call Hugging Face Inference API:** An HTTP Request node makes a POST call to the Hugging Face Inference API for the FLUX.1 model. It sends the user's prompt combined with the selected style prompt.
    5. **Upload to S3:** The generated image (binary data) is uploaded to a Cloudflare R2 (S3-compatible) bucket.
    6. **Serve Webpage:** The workflow responds to the initial form submission by rendering an HTML page that displays the newly generated image, along with the last four previously generated images.

### 236. 1/OpenAI_and_LLMs/Force AI to use a specific output format.txt
- **Description:** This workflow demonstrates a robust method for forcing an LLM to return data in a specific JSON format, using a combination of a structured output parser and an auto-fixing parser.
- **Trigger:** The workflow is triggered manually.
- **Functionality:**
    1. **Prompt:** A Set node defines the initial prompt: "Return the 5 largest states by area in the USA with their 3 largest cities and their population."
    2. **LLM Chain:** The prompt is sent to an LLM Chain.
    3. **Structured Output Parser:** This parser is configured with a specific JSON schema that defines the desired output structure (an object with a `state` and an array of `cities`, each with `name` and `population`).
    4. **Auto-fixing Output Parser:** This is the key component. It wraps the `Structured Output Parser`. If the initial response from the LLM doesn't perfectly match the JSON schema, the auto-fixer will automatically call the LLM *again*. In this second call, it provides the original prompt, the faulty output, the parsing error, and instructs the LLM to "Please try again" and correct its mistake.
    5. **LLMs:** The workflow uses two separate OpenAI Chat Models: one for the initial attempt and another for the auto-fixing attempt. This ensures that even if the first response is slightly malformed, the workflow can self-correct to produce a valid, structured JSON output.

### 237. 1/OpenAI_and_LLMs/Generate 9_16 Images from Content and Brand Guidelines.txt
- **Description:** This workflow automates the creation of short-form video content (9:16 aspect ratio) by generating a script and corresponding images based on a blog post and brand guidelines stored in Airtable.
- **Trigger:** The workflow is triggered manually.
- **Functionality:**
    1. **Retrieve Brand Guidelines:** It fetches brand guidelines (e.g., style, tone, colors) from an Airtable base.
    2. **Retrieve Content:** It fetches a blog post from another Airtable table, filtered by a specific keyword (e.g., "ai automation").
    3. **Script & Image Prompt Generation:** The blog post content is sent to an OpenAI model (`gpt-4o-mini`) with a prompt to:
        - Create a 4-scene script for a short video (<30 seconds).
        - Generate a detailed image prompt for each of the 4 scenes.
        - Generate a separate image prompt for a video thumbnail.
    4. **Image Generation (Loop):** The workflow loops through the 5 generated image prompts (4 scenes + 1 thumbnail).
        - **Improve Prompt:** Each prompt is sent to the Leonardo.ai API to be improved and expanded for better image generation results.
        - **Generate Image:** The improved prompt is used to generate an image via the Leonardo.ai API.
    5. **Output:** The workflow outputs the generated images, ready to be assembled into a short-form video.

### 238. 1/OpenAI_and_LLMs/Generate audio from text using OpenAI and Webhook _ Text to Speech Workflow.txt
- **Description:** This workflow creates a simple API endpoint that converts text to speech using OpenAI's TTS (Text-to-Speech) model.
- **Trigger:** A webhook that receives a POST request.
- **Functionality:**
    1. **Webhook:** The workflow is triggered by a POST request to a specific URL (`/generate_audio`). The request body is expected to contain a JSON object with a `text_to_convert` field.
    2. **OpenAI:** The text from the webhook body is passed to the OpenAI node, which is configured to use the `audio` resource. The voice is set to "fable" by default.
    3. **Respond to Webhook:** The workflow responds to the initial request with the binary data of the generated MP3 audio file. This allows any application to call this endpoint and receive an audio file in return.
### 239. 1/OpenAI_and_LLMs/Generate Text-to-Speech Using Elevenlabs via API.txt
- **Description:** This workflow provides a simple API endpoint to generate speech from text using the ElevenLabs API.
- **Trigger:** A webhook that listens for POST requests at the `/generate-voice` path.
- **Functionality:**
    1. **Webhook:** The workflow is triggered by a POST request containing a `voice_id` and the `text` to be converted in its body.
    2. **Input Validation:** An IF node checks if both `voice_id` and `text` parameters are present. If not, it responds with an error.
    3. **Generate Voice:** An HTTP Request node makes a POST call to the ElevenLabs API endpoint (`https://api.elevenlabs.io/v1/text-to-speech/{voice_id}`). It sends the text in the request body and includes the necessary API key for authentication.
    4. **Respond to Webhook:** The workflow responds with the binary audio data (MP3) generated by ElevenLabs.

### 240. 1/OpenAI_and_LLMs/Generating Image Embeddings via Textual Summarisation.txt
- **Description:** This workflow demonstrates a method for creating searchable text-based embeddings for images. Instead of embedding the image directly, it analyzes the image to generate a rich text description, which is then embedded and stored in a vector database.
- **Trigger:** The workflow is triggered manually.
- **Functionality:**
    1. **Get Image:** Downloads an image from Google Drive.
    2. **Image Analysis:**
        - **Get Color Information:** An Edit Image node extracts color channel statistics (histograms) from the image.
        - **Get Image Keywords:** An OpenAI vision model analyzes the image and generates a comma-separated list of descriptive keywords (subjects, objects, mood, lighting, etc.).
    3. **Combine Analysis:** The keywords and color information are merged into a single text document. This document serves as the textual representation of the image.
    4. **Create Document for Embedding:** The combined text is prepared as a document, and relevant metadata (source filename, format, background color) is attached.
    5. **Store in Vector Store:** The final document is passed to an In-Memory Vector Store node. An OpenAI embedding model creates a vector from the text, which is then stored in the memory, making the original image searchable via text queries.
    6. **Example Search:** A final node demonstrates how to perform a similarity search against the in-memory store using a simple text prompt like "student having fun".

### 241. 1/OpenAI_and_LLMs/lemlist __ GPT-3_ Supercharge your sales workflows.txt
- **Description:** This workflow automates sales outreach follow-up by categorizing email replies from a lemlist campaign using OpenAI and then taking appropriate action in other tools like HubSpot and Slack.
- **Trigger:** A lemlist trigger that fires when a lead replies to an email campaign.
- **Functionality:**
    1. **Lemlist Trigger:** The workflow starts when a new email reply is received in a lemlist campaign.
    2. **Categorize Reply with OpenAI:** The body of the email reply is sent to an OpenAI model. The model is prompted to classify the reply into one of four categories: "Interested", "Out of Office", "Unsubscribe", or "Other".
    3. **Switch based on Category:** A Switch node routes the workflow based on the AI's categorization:
        - **Interested:** Marks the lead as "interested" in lemlist, finds or creates the corresponding contact in HubSpot, creates a new deal associated with that contact, and sends a notification to a Slack channel with a link to the new deal.
        - **Out of Office:** Finds the contact in HubSpot and creates a follow-up task for the sales team.
        - **Unsubscribe:** Unsubscribes the lead from the lemlist campaign.
        - **Other:** Sends a notification to a Slack channel for manual review.

### 242. 1/OpenAI_and_LLMs/Narrating over a Video using Multimodal AI.txt
- **Description:** This workflow demonstrates an advanced use of a multimodal AI model to generate a narration script for a video. It breaks the video into frames, generates a script for batches of frames, and then uses a Text-to-Speech model to create the final audio narration.
- **Trigger:** The workflow is triggered manually.
- **Functionality:**
    1. **Download Video:** Downloads a sample video file.
    2. **Extract Frames:** A Python Code node with the OpenCV library extracts up to 90 evenly distributed frames from the video.
    3. **Generate Narration Script (Loop):** The workflow loops through the frames in batches of 15.
        - In each loop, it sends the batch of 15 frames to an OpenAI vision model (`gpt-4o`).
        - The model is prompted to generate a short voiceover script in the style of David Attenborough, continuing from the script generated in the previous loop to ensure a cohesive narrative.
    4. **Combine Script:** All the generated script portions are aggregated into a single, complete narration script.
    5. **Generate Voice Over:** The full script is sent to OpenAI's Text-to-Speech API to generate an MP3 audio file of the narration.
    6. **Upload to GDrive:** The final MP3 file is uploaded to Google Drive.

### 243. 1/OpenAI_and_LLMs/OpenAI assistant with custom tools.txt
- **Description:** This workflow showcases how to build a powerful OpenAI Assistant and equip it with custom tools created from other n8n workflows.
- **Trigger:** A manual chat trigger for user interaction.
- **Functionality:**
    1. **OpenAI Assistant:** The core of the workflow is an OpenAI Assistant.
    2. **Custom Tools:** The assistant is given access to two custom tools:
        - **`country_capitals_tool`:** This tool is a sub-workflow within the main workflow. It can be called in two ways:
            - With the input "list", it returns a list of all fictional countries it knows about.
            - With a specific country name, it returns that country's capital.
        - **`date_tool`:** A simple Code node tool that returns the current timestamp.
    3. **Interaction:** A user can chat with the assistant and ask questions like "What is the capital of Wakanda?" or "What time is it?". The assistant will intelligently decide which tool to use to answer the question, call the corresponding n8n workflow or node, and use the returned information to formulate its final response.
### 244. 1/OpenAI_and_LLMs/OpenAI Assistant workflow_ upload file, create an Assistant, chat with it!.txt
- **Description:** This workflow provides a complete, end-to-end example of how to programmatically create a knowledgeable OpenAI Assistant. It involves fetching a document, uploading it to OpenAI as a knowledge source, creating a new Assistant that uses this file, and then making that Assistant available for conversation.
- **Trigger:** The workflow can be initiated manually to perform the setup, and it includes a Chat Trigger for users to interact with the final assistant.
- **Functionality:**
    1. **Get File:** Downloads a document (e.g., a PDF about a music festival) from Google Drive.
    2. **Upload File to OpenAI:** The downloaded file is uploaded to OpenAI's file storage with the purpose set to "assistants".
    3. **Create new Assistant:** A new OpenAI Assistant is created with a specific name, description, and a detailed system prompt that defines its personality and rules (e.g., "You are an assistant for the Summer Eclectic Marathon Music Festival. Use ONLY the attached document to answer questions."). The ID of the file uploaded in the previous step is attached to the assistant for knowledge retrieval.
    4. **Chat Trigger:** A final Chat Trigger node allows users to start a conversation with the newly created, file-aware Assistant.

### 245. 1/OpenAI_and_LLMs/OpenAI examples_ ChatGPT, DALLE-2, Whisper-1 – 5-in-1.txt
- **Description:** This is a comprehensive gallery workflow showcasing five different ways to use the OpenAI node in n8n, covering both legacy and modern models for text, image, and audio tasks.
- **Trigger:** The workflow is triggered manually.
- **Functionality:**
    1. **Text Completion (Legacy):** Demonstrates using the `davinci-003` model to summarize a block of text.
    2. **Text Edit (Legacy):** Shows how to use the older edit endpoint to perform tasks like translation.
    3. **ChatGPT (Chat Completion):** Provides multiple examples of using the chat endpoint (`gpt-3.5-turbo`) for summarization, translation, and following system-level instructions (e.g., "Always add 5 emojis to your answer").
    4. **Chained AI Calls:** A multi-step example where the workflow first summarizes text with ChatGPT, then uses another ChatGPT call to generate a creative DALL-E 2 prompt from that summary, and finally calls the DALL-E 2 model to generate images.
    5. **Code Generation:** An example of using ChatGPT to generate HTML code for an SVG image.

### 246. 1/OpenAI_and_LLMs/Organise Your Local File Directories With AI.txt
- **Description:** This workflow acts as an AI-powered file manager for a local directory. It monitors a folder for new files and uses a Mistral AI model to intelligently sort them into appropriate subdirectories.
- **Trigger:** A Local File Trigger that activates whenever a file is added to a specified directory that n8n has access to.
- **Functionality:**
    1. **List Files and Folders:** When triggered, the workflow executes a shell command (`ls`) to get a list of all files and sub-folders in the target directory.
    2. **AI File Manager:** The lists of files and folders are passed to a Mistral AI model. The AI is prompted to act as a file manager, analyze the filenames, and decide which existing folder each file should be moved to. If no suitable folder exists, it can suggest a new one (e.g., "misc").
    3. **Structured Output:** A parser ensures the AI's suggestions are returned in a clean JSON format, like `[{ "folder": "Images", "files": ["photo1.jpg", "photo2.png"] }]`.
    4. **Move Files:** The workflow loops through the AI's suggestions and executes a `mv` shell command to move each file into its designated subdirectory, creating the directory first if it doesn't exist.

### 247. 1/OpenAI_and_LLMs/Personal Shopper Chatbot for WooCommerce with RAG using Google Drive and openAI.txt
- **Description:** This workflow creates a dual-capability AI chatbot for a WooCommerce store. It acts as a personal shopper by searching for products and also answers general questions about the store using a RAG knowledge base.
- **Trigger:** A chat trigger for user interaction.
- **Functionality:**
    - **RAG Setup (Manual):** Documents with store information (e.g., opening hours, return policy) are loaded from Google Drive and embedded into a Qdrant vector store.
    - **Chat Interaction (Triggered):**
        1. **Information Extractor:** When a user sends a message, an initial LLM call extracts key entities to determine the user's intent. It identifies if the user is searching for a product and extracts keywords, price ranges, or SKUs.
        2. **AI Agent:** The main AI Agent orchestrates the response. It has two primary tools:
            - **`personal_shopper` (WooCommerce Tool):** If the Information Extractor identified a product search, the agent uses this tool. It takes the extracted keywords, prices, etc., and queries the WooCommerce API to find matching products.
            - **`RAG` (Vector Store Tool):** If the user asks a general question, the agent uses this tool to query the Qdrant vector store to find the answer from the store's documents.
        3. **Response Generation:** The agent uses the information from the selected tool to formulate and deliver a helpful response to the user.

### 248. 1/OpenAI_and_LLMs/Prompt-based Object Detection with Gemini 2.0.txt
- **Description:** This workflow demonstrates the prompt-based object detection capabilities of the Google Gemini 2.0 vision model. Instead of detecting all objects, it finds specific objects requested in a text prompt.
- **Trigger:** The workflow is triggered manually.
- **Functionality:**
    1. **Get Image:** Downloads a test image (e.g., a picture with several animals).
    2. **Gemini 2.0 Object Detection:** An HTTP Request node calls the Gemini 2.0 API.
        - **Input:** It sends both the image and a text prompt, such as "I want to see all bounding boxes of rabbits in this image."
        - **Response Schema:** It instructs the model to return the response as a JSON array of objects, where each object contains a `label` and a `box_2d` array with four coordinate points.
    3. **Scale Coordinates:** The coordinates returned by Gemini are normalized (on a 0-1000 scale). A Code node scales these coordinates to match the original image's actual pixel dimensions.
    4. **Draw Bounding Boxes:** The workflow uses the Edit Image node to draw rectangles on the original image using the scaled coordinates, visually highlighting the objects that the AI detected based on the prompt.
### 249. 1/OpenAI_and_LLMs/Proxmox AI Agent with n8n and Generative AI Integration.txt
- **Description:** This workflow creates an AI agent capable of interacting with a Proxmox Virtual Environment. The agent can understand natural language commands to perform actions like creating VMs or retrieving cluster status.
- **Trigger:** The workflow can be triggered by various inputs, including a direct chat, a Telegram message, a Gmail message, or a generic webhook.
- **Functionality:**
    1. **AI Agent:** The core is an AI Agent powered by Google Gemini. It's given a system prompt and access to tools.
    2. **Tools:**
        - **Proxmox API Documentation & Wiki:** The agent is provided with the Proxmox API documentation and Wiki via HTTP Request tools, allowing it to learn how to construct valid API calls.
        - **Proxmox Cluster Status:** A tool that directly queries the Proxmox cluster status.
    3. **Structured Output:** The agent is prompted to return its desired action in a structured JSON format, specifying the HTTP method, URL endpoint, and necessary details (e.g., `vmid`, `cores`, `memory` for creating a VM).
    4. **API Execution:** An IF node checks the `response_type` from the agent.
        - If it's a `GET` request, it executes it and formats the response.
        - If it's a `POST` or `DELETE` request, it executes the corresponding action on the Proxmox server.
    5. **Response Formatting:** The final response from the Proxmox API is formatted into a human-readable message before being sent back to the user.

### 250. 1/OpenAI_and_LLMs/Query n8n Credentials with AI SQL Agent.txt
- **Description:** This workflow creates an AI-powered agent that can answer questions about which n8n workflows are using specific credentials by querying a local SQLite database.
- **Trigger:** The workflow has two parts: a manual trigger to populate the database and a chat trigger for querying.
- **Functionality:**
    - **Part 1: Database Population (Manual Trigger)**
        1. **Get Workflows:** The n8n API node fetches all workflows from the instance.
        2. **Map Credentials:** A Set node extracts the `workflow_id`, `workflow_name`, and a list of all `credentials` used in each workflow.
        3. **Save to Database:** A Python Code node with `sqlite3` creates a local database (`n8n_workflow_credentials.db`) and inserts a record for each workflow, storing the credentials list as a JSON string.
    - **Part 2: AI SQL Agent (Chat Trigger)**
        1. **Chat Trigger:** A user asks a question like, "Which workflows use Slack and Google Calendar credentials?"
        2. **AI Agent:** An OpenAI agent is prompted to act as a database query assistant.
        3. **Custom SQL Tool:** The agent is given a custom tool built with a Code node. This tool takes a SQL query as input, executes it against the SQLite database created in Part 1, and returns the results.
        4. **Query Generation:** The agent translates the user's natural language question into a valid SQL query (e.g., `SELECT workflow_name FROM n8n_workflow_credentials WHERE credentials LIKE '%slack%' AND credentials LIKE '%googleCalendar%'`).
        5. **Response:** The agent receives the query results from the tool and presents the answer to the user in a readable format.

### 251. 1/OpenAI_and_LLMs/Suggest meeting slots using AI.txt
- **Description:** This workflow automates email responses for meeting requests. It uses an AI to determine if an email is a meeting request, checks the user's Google Calendar for availability, and suggests appropriate times to the sender.
- **Trigger:** A Gmail trigger that runs every minute, checking for unread emails.
- **Functionality:**
    1. **Classify Email:** The email's subject and snippet are passed to an OpenAI model to classify if it is an appointment request (returns `true` or `false`).
    2. **Check Availability (If Appointment):** If the email is a meeting request, the workflow triggers a sub-workflow.
    3. **Sub-workflow (Get Availability):**
        - Fetches all Google Calendar events for the next month.
        - Filters for confirmed events and formats the start/end times.
        - Returns a stringified JSON array of busy slots.
    4. **Compose Reply (AI Agent):** The main workflow's AI Agent receives the original email content and the stringified list of busy calendar slots.
    5. **System Prompt:** The agent is instructed to act as a scheduling assistant. It must analyze the user's request and the provided availability to suggest specific meeting times, ensuring there's a buffer between meetings.
    6. **Send & Mark as Read:** The AI-generated reply is sent to the original sender, and the incoming email is marked as read in Gmail.

### 252. 1/OpenAI_and_LLMs/Summarize YouTube Videos from Transcript.txt
- **Description:** This workflow automates the summarization of YouTube videos by fetching their transcripts and using an AI model to create a concise summary.
- **Trigger:** An n8n Form where a user can paste a YouTube video URL.
- **Functionality:**
    1. **Form Trigger:** A user submits a YouTube URL.
    2. **Request YouTube Transcript:** An HTTP Request node makes a POST call to an Apify actor designed to scrape YouTube video transcripts.
    3. **Summarization Chain:** The extracted transcript text is passed to a LangChain Summarization Chain.
    4. **Summarization Engine:** The chain uses an OpenAI Chat Model to process the transcript and generate a summary.
    5. **Output:** The final output of the workflow is the generated text summary of the video.

### 253. 1/OpenAI_and_LLMs/Transform Image to Lego Style Using Line and Dall-E.txt
- **Description:** This fun workflow creates a LINE chatbot that transforms any image a user sends into a "Lego style" version using a multi-step AI process.
- **Trigger:** A webhook that receives messages from a LINE chatbot.
- **Functionality:**
    1. **Receive Line Message:** The webhook is triggered when a user sends an image to the LINE bot.
    2. **Get Image Content:** An HTTP Request node fetches the binary data of the image from the LINE content URL.
    3. **Create DALL-E Prompt:** The image is sent to an OpenAI vision model (`gpt-4o-mini`). The model is prompted to analyze the image and create a new, descriptive text prompt for DALL-E that will transform the image into an "isometric LEGO image".
    4. **Generate Lego Image:** The AI-generated text prompt is then sent to the DALL-E API to create the new Lego-style image.
    5. **Send Image Back to Line:** The URL of the newly generated image is used to send an image message back to the user in the LINE chat.
### 254. 1/OpenAI_and_LLMs/Translate audio using AI.txt
- **Description:** This workflow translates a French audio clip into English speech. It takes a French text, generates French audio using ElevenLabs, transcribes it back to text using OpenAI's Whisper, translates the text to English with an LLM, and finally generates the English audio with ElevenLabs.
- **Trigger:** The workflow is triggered manually.
- **Functionality:**
    1. **Set Input:** A Set node provides the initial French text and the ElevenLabs voice ID to be used.
    2. **Generate French Audio:** An HTTP Request node calls the ElevenLabs API to convert the French text into an MP3 audio file.
    3. **Transcribe Audio:** The generated French audio is sent to OpenAI's Whisper-1 model via an HTTP Request node to be transcribed back into text. This step essentially validates the audio generation and prepares the text for translation.
    4. **Translate Text to English:** The transcribed French text is passed to an OpenAI Chat Model with the prompt "Translate to English".
    5. **Generate English Audio:** The translated English text is sent back to the ElevenLabs API to generate the final English speech audio file.

### 255. 1/OpenAI_and_LLMs/Use OpenRouter in n8n versions _1.78.txt
- **Description:** This workflow demonstrates how to use OpenRouter to access a wide variety of LLMs within n8n, allowing for dynamic model selection.
- **Trigger:** A chat trigger that initiates a conversation.
- **Functionality:**
    1. **Chat Trigger:** A user starts a chat.
    2. **Settings:** A Set node defines the `model` to be used (e.g., `deepseek/deepseek-r1-distill-llama-8b`) and passes along the user's `prompt` and the `sessionId`.
    3. **AI Agent:** The user's prompt is sent to a standard AI Agent.
    4. **LLM Model (OpenRouter):** The key part of this workflow is the `lmChatOpenAi` node. Instead of using a standard OpenAI model, it's configured to use OpenRouter credentials and a dynamic model name passed from the "Settings" node. This allows the user to easily switch between any of the hundreds of models available on OpenRouter (like different versions of Llama, Mistral, Qwen, etc.) by simply changing the value in the "Settings" node.
    5. **Chat Memory:** A Window Buffer Memory node maintains the context of the conversation.

### 256. 1/OpenAI_and_LLMs/AI Agent _ Google calendar assistant using OpenAI.txt
- **Description:** This workflow creates a Google Calendar assistant powered by an AI agent. The agent can understand natural language commands to retrieve and create calendar events.
- **Trigger:** A chat trigger for user interaction.
- **Functionality:**
    1. **Calendar AI Agent:** The workflow is centered around an AI Agent powered by `gpt-4o`. The system prompt instructs the agent on how to behave, including asking for clarification if a request is vague and using the current date for context.
    2. **Tools:** The agent is equipped with two Google Calendar tools:
        - **Get Events:** This tool is used when the user asks to retrieve event data. The agent is prompted to ask for a date range if one is not provided and then passes the `start_date` and `end_date` to the tool.
        - **Create Events:** This tool is used to create new events. The agent gathers the `start_date`, `end_date`, `event_title`, and `event_description` from the user before calling the tool.
    3. **Conversation Memory:** A Window Buffer Memory node is used to keep track of the conversation, allowing for multi-turn interactions.

### 257. 1/OpenAI_and_LLMs/AI agent chat.txt
- **Description:** This is a basic but powerful workflow that sets up a conversational AI agent with the ability to search the web.
- **Trigger:** A chat message from the n8n chat interface.
- **Functionality:**
    1. **Chat Trigger:** A user sends a message.
    2. **AI Agent:** The message is processed by an AI Agent.
    3. **LLM:** The agent uses an OpenAI Chat Model (`gpt-4o-mini`) to power its conversational abilities.
    4. **Tool (SerpAPI):** The agent is equipped with a SerpAPI tool, which allows it to perform a Google search to find answers to user questions that require up-to-date information from the internet.
    5. **Memory:** A Window Buffer Memory node stores the recent conversation history, enabling the agent to have contextual follow-up conversations.

### 258. 1/OpenAI_and_LLMs/AI Agent for realtime insights on meetings.txt
- **Description:** This advanced workflow provides real-time AI insights during a live meeting. It uses Recall.ai to have a bot join a meeting, transcribes the conversation in real-time, and uses an OpenAI Assistant to provide summaries or answer questions based on the live transcript.
- **Trigger:** The workflow has two entry points: a manual trigger to start the bot and a webhook to receive real-time transcription data.
- **Functionality:**
    - **Scenario 1: Starting the Bot**
        1. A meeting URL is provided.
        2. An HTTP Request creates a Recall.ai bot and instructs it to join the meeting. The bot is configured to send real-time transcription data to an n8n webhook.
        3. A new OpenAI Assistant thread is created for this meeting.
        4. The bot ID and thread ID are stored in a Supabase database.
    - **Scenario 2: Real-time Transcription**
        1. The Recall.ai bot sends transcription fragments to the n8n webhook as they are generated.
        2. The new transcript part is appended to a `dialog` array in the Supabase record for that meeting.
        3. An IF node checks if a keyword (e.g., "Jimmy") was mentioned.
        4. If the keyword is present, the most recent part of the transcript is sent to the persistent OpenAI Assistant thread created in Scenario 1. The Assistant can then perform a task, such as summarizing the conversation up to that point or answering a question, and the result could be sent to a Slack channel or other destination.
264. **AI Agent to chat with Supabase/PostgreSQL DB**: This workflow provides an AI-powered conversational agent for interacting with a Supabase or PostgreSQL database. Users can ask questions in natural language, and the agent, equipped with tools to query the database schema and execute SQL commands, will retrieve and present the requested data.

265. **AI Agent to chat with Google Search Console Data, using OpenAI and Postgres**: This workflow sets up an AI agent that allows users to conversationally query their Google Search Console data. It uses an OpenAI model, maintains chat history in a PostgreSQL database, and utilizes a custom tool to make API calls to the Search Console. This enables users to request insights and data from their web properties using natural language.

266. **AI Agent with Ollama for current weather and wiki**: This workflow demonstrates a conversational AI agent built with a local Ollama model. The agent is equipped with tools to fetch current weather information via an HTTP request and to look up information on Wikipedia, providing a versatile assistant for general inquiries.

267. **AI Automated HR Workflow for CV Analysis and Candidate Evaluation**: An automated pipeline for human resources, this workflow processes job applications submitted through a form. It extracts text from CVs, uses AI to pull out key information like qualifications and personal data, summarizes the candidate's profile, and then has an "HR Expert" AI evaluate the candidate against the job description. All data is then logged in a Google Sheet.

268. **AI chat with any data source (using the n8n workflow tool)**: This workflow showcases a powerful pattern where an AI agent can use another n8n workflow as a custom tool. The example provided uses a sub-workflow to fetch data from Hacker News, but it can be adapted to connect to any data source, allowing the AI agent to answer questions about that data.
269. **Analyze feedback and send a message on Mattermost**: This workflow triggers on a new Typeform submission, analyzes the sentiment of the feedback using Google Cloud Natural Language, and if the sentiment is negative, sends a notification to a specific Mattermost channel.

270. **Analyze feedback using AWS Comprehend and send it to a Mattermost channel**: Similar to the above, this workflow triggers on a Typeform submission, but uses AWS Comprehend for sentiment analysis. If the feedback is classified as negative, it posts a message to a Mattermost channel.

271. **API Schema Extractor**: A sophisticated workflow that automates the discovery and extraction of API schemas from websites. It uses Apify for web scraping, Google Gemini for text processing and classification, and Qdrant for storing document embeddings. The workflow can be triggered to research, extract, and generate information about API schemas.

272. **Automate Pinterest Analysis & AI-Powered Content Suggestions With Pinterest API**: This scheduled workflow pulls Pinterest pin data, stores it in Airtable, and then uses an AI agent to analyze performance trends. It generates content suggestions based on this analysis, summarizes them, and emails the report to a marketing manager.

273. **Automate Screenshots with URLbox & Analyze them with AI**: This workflow uses the URLbox API to capture a screenshot of a given URL. It then leverages an AI vision model (OpenAI) to analyze the image and generate a one-sentence description of the website's content.
274. **Automate SIEM Alert Enrichment with MITRE ATT&CK, Qdrant & Zendesk in n8n**: A sophisticated cybersecurity workflow that enriches SIEM alerts by correlating them with the MITRE ATT&CK framework. It uses a Qdrant vector store for knowledge base lookups and integrates with Zendesk to update tickets with contextual information. An AI agent helps analyze the alerts and suggest remediation steps.

275. **Automate testimonials in Strapi with n8n**: This workflow automates gathering testimonials from Twitter and form submissions. It searches for tweets mentioning 'strapi' or 'n8n.io', analyzes the sentiment of the content using Google Cloud Natural Language, and if positive, stores the testimonial in a Strapi CMS. It also handles direct form submissions for testimonials.

276. **Bitrix24 Chatbot Application Workflow example with Webhook Integration**: This workflow provides a complete example of a Bitrix24 chatbot application. It handles various events like new messages, bot installation, and users joining a chat. It uses a webhook to receive events from Bitrix24 and then routes them to the appropriate processing logic, sending responses back via HTTP requests.

277. **ChatGPT Automatic Code Review in Gitlab MR**: This workflow automates code reviews in GitLab. It triggers on a webhook from a GitLab merge request, specifically when a trigger comment is added. It then fetches the code changes, uses an OpenAI model to review the code based on a detailed prompt, and posts the review as a discussion in the merge request.

278. **Classify new bugs in Linear with OpenAI's GPT-4 and move them to the right team**: This workflow automates bug triage in Linear. When a new issue is created in a general engineering team, it uses OpenAI's GPT-4 to classify the bug based on its title, description, and a predefined list of teams and their responsibilities. It then updates the issue to assign it to the correct team. If the AI cannot determine the team, it sends a notification to a Slack channel.
279. **Create, update, and get a profile in Humantic AI**: This workflow demonstrates the core functionalities of the Humantic AI node. It creates a profile using a LinkedIn URL, updates it with resume data fetched from a URL, and then retrieves the enriched profile information.

280. **Enhance Customer Chat by Buffering Messages with Twilio and Redis**: This workflow improves the user experience of a chat application by buffering incoming Twilio messages. It uses Redis to hold messages for a short period, allowing a user to send multiple messages in quick succession. The AI agent then processes the entire buffered conversation and sends a single, consolidated reply.

281. **Hacker News Throwback Machine - See What Was Hot on This Day, Every Year!**: A daily scheduled workflow that scrapes the Hacker News front page for the same date across multiple years (from 2007 to the present). It then uses a Google Gemini model to analyze the headlines, identify trends, and generate a "throwback" summary in markdown, which is then posted to a Telegram channel.

282. **Handling Appointment Leads and Follow-up With Twilio, Cal.com and AI**: A comprehensive lead management system. It uses Twilio for SMS communication, an AI agent to qualify leads and schedule appointments with Cal.com, and Airtable to track the entire lead lifecycle. The workflow also includes an automated, scheduled follow-up system for leads who have not yet booked a meeting.

283. **Integrating AI with Open-Meteo API for Enhanced Weather Forecasting**: This workflow showcases an AI agent using a chain of tools to answer a user's request. When asked for a weather forecast, the agent first uses an HTTP request tool to find the city's latitude and longitude via the Open-Meteo geocoding API. It then uses a second tool to pass these coordinates to the weather forecast API to retrieve the requested data.
284. **Introduction to the HTTP Tool**: This workflow serves as a demonstration of the HTTP Request tool within an AI agent context. It includes two examples: one that scrapes a webpage using Firecrawl.dev and another that suggests an activity from the Bored API. It showcases how to configure the tool for different API interactions.

285. **KB Tool - Confluence Knowledge Base**: This workflow acts as a sub-workflow or "tool" for a larger AI agent. It's designed to be called by a parent workflow to query a Confluence knowledge base. It takes a search query, uses the Confluence API to find relevant articles, and returns a formatted response with the title, link, and an excerpt of the content.

286. **LINE Assistant with Google Calendar and Gmail Integration**: A comprehensive personal assistant built for the LINE messaging platform. This AI agent can interact with Google Calendar to create and read events, and with Gmail to read emails. It also uses Wikipedia for general knowledge questions. The workflow handles incoming messages from LINE, processes them with the agent, and sends back a reply.

287. **Monthly Spotify Track Archiving and Playlist Classification**: This is a powerful music management workflow. On a monthly schedule, it retrieves all of a user's liked songs from Spotify, fetches their audio features, and logs them in a Google Sheet. It then uses an Anthropic model to classify the new tracks and add them to the appropriate playlists based on their characteristics and the playlist descriptions.

288. **Obsidian Notes Read Aloud using AI: Available as a Podcast Feed**: This workflow turns your Obsidian notes into a personal podcast. When you send a note to a webhook from Obsidian, it uses OpenAI's TTS to generate an audio version and an AI model to write a short description. The audio is uploaded to Cloudinary, and the details are added to a Google Sheet, which then powers a standard RSS podcast feed that you can subscribe to.
289. **Optimize & Update Printify Title and Description Workflow**: This workflow automates the optimization of product listings on Printify. It fetches products from a shop, uses an AI agent to rewrite titles and descriptions based on brand guidelines and custom instructions (e.g., for a holiday season), and stages these changes in a Google Sheet. When a row in the sheet is marked for upload, a trigger fires to update the corresponding product in Printify via its API.

290. **Qualify replies from Pipedrive persons with AI**: This workflow automates lead qualification from email replies. It triggers on new emails, checks if the sender is a person in a Pipedrive campaign, and if so, uses OpenAI to analyze the email content to determine if the person is interested. If interest is detected, a new deal is automatically created in Pipedrive.

291. **Siri AI Agent: Apple Shortcuts powered voice template**: This template creates a voice-controlled AI assistant using Siri and Apple Shortcuts. A user can say "Hey Siri, Ask Agent," speak their query, and the transcribed text is sent to this n8n workflow. An AI Agent processes the request, and the text response is sent back to the shortcut, where Siri reads it aloud to the user.

292. **Text automations using Apple Shortcuts**: This workflow provides a suite of text manipulation tools accessible via Apple Shortcuts. A user can select text on their device and use a shortcut to trigger this workflow to perform actions like translation, grammar correction, summarization, or expansion using different OpenAI prompts. The modified text is then returned to the shortcut.
293. **Use AI to organize your Todoist Inbox**: This workflow helps manage a Todoist inbox by automatically categorizing new tasks. It uses an AI model to determine which project a task belongs to based on its content and a predefined list of projects, and then sets the appropriate priority.

294. **Using External Workflows as Tools in n8n**: This workflow demonstrates a reusable "tool" workflow. It is designed to be called by other workflows and takes a URL as input, scrapes the content using Firecrawl, and returns the markdown. This showcases a modular approach to building complex automations.

295. **UTM Link Creator & QR Code Generator with Scheduled Google Analytics Reports**: A marketing automation workflow that generates UTM-tagged URLs for campaigns, stores them in Airtable, and creates a corresponding QR code using Quickchart.io. It also includes a scheduled component that uses an AI agent to analyze Google Analytics data and send a summary report via Gmail.

296. **Visualize your SQL Agent queries with OpenAI and Quickchart.io**: This workflow enhances a standard SQL AI agent with data visualization capabilities. After the agent queries a database, a text classifier determines if a chart would be helpful. If so, it uses OpenAI's structured output to generate a Chart.js definition and then creates the chart image using the Quickchart.io API, which is then appended to the agent's response.

297. **Zoom AI Meeting Assistant creates mail summary, ClickUp tasks and follow-up call**: A powerful meeting assistant that processes Zoom meeting recordings. It transcribes the audio, creates a summary, sends it to participants via email, and uses an AI agent to identify action items. These action items are then used to create tasks in ClickUp and schedule follow-up meetings in Microsoft Outlook.
298. **Ask questions about a PDF using AI**: This workflow enables a conversational interface for PDF documents. It fetches a PDF from Google Drive, splits it into manageable chunks, generates embeddings using OpenAI, and stores them in a Pinecone vector store. Users can then ask questions, and the workflow retrieves relevant document chunks to formulate an answer.

299. **Breakdown Documents into Study Notes using Templating MistralAI and Qdrant**: This workflow automates the creation of study materials from documents. When a file is added to a local directory, it's processed and embedded into a Qdrant vector store. The workflow then uses MistralAI with different templates to generate various study aids like a study guide, a timeline of events, and a briefing document, which are then saved locally.

300. **Chat with PDF docs using AI (quoting sources)**: This workflow allows users to chat with a PDF and receive answers with citations. It loads a PDF from Google Drive, chunks the content, and stores it in a Pinecone vector store. When a user asks a question, the system retrieves relevant chunks and uses them to generate an answer, explicitly citing the source chunks in the response.

301. **Convert URL HTML to Markdown Format and Get Page Links**: This workflow takes a list of URLs and uses the Firecrawl.dev API to scrape each page. It converts the HTML content into clean markdown and extracts all hyperlinks from the page. The workflow is designed to handle multiple URLs in batches, respecting API rate limits.

302. **CV Resume PDF Parsing with Multimodal Vision AI**: An innovative approach to resume screening that avoids potential prompt injection attacks. This workflow converts a resume PDF into an image using the Stirling PDF API. It then uses a multimodal vision model (Google Gemini) to analyze the image of the resume, assessing the candidate's qualifications for a role as a human would, thus bypassing any hidden text prompts.
303. **ETL pipeline for text processing**: This workflow demonstrates a classic ETL (Extract, Transform, Load) process. It triggers on a schedule, searches for tweets with a specific hashtag, stores them in MongoDB, analyzes their sentiment with Google Cloud Natural Language, and then loads the tweet and its sentiment score into a PostgreSQL database. It also sends a Slack notification for tweets with a positive sentiment.

304. **Extract and process information directly from PDF using Claude and Gemini**: This workflow compares the capabilities of Anthropic's Claude 3.5 Sonnet and Google's Gemini 2.0 Flash for direct PDF data extraction. It fetches a PDF from Google Drive, converts it to a base64 string, and sends it to both models with the same prompt to extract specified information, allowing for a side-by-side comparison of their performance.

305. **Extract data from resume and create PDF with Gotenberg**: This workflow processes resumes submitted via Telegram. It extracts the text from the PDF, uses OpenAI to parse it into a structured JSON format, converts the various sections (personal info, employment history, etc.) into HTML, and then uses the Gotenberg API to merge these HTML sections into a newly generated, well-formatted PDF.

306. **Extract license plate number from image uploaded via an n8n form**: A straightforward vision AI workflow. A user uploads an image of a car via an n8n form, and the workflow uses a vision-capable model (via OpenRouter) to extract the license plate number from the image and displays it on the form's completion page.

307. **Extract text from PDF and image using Vertex AI (Gemini) into CSV**: This workflow automates data extraction from documents in a Google Drive folder. It triggers when a new file is added, routes PDFs and images through different processing paths (text extraction for PDFs, Gemini Vision for images), uses an AI model to structure the extracted text into CSV format with categories, and uploads the final CSV file back to Google Drive.
308. **Invoice data extraction with LlamaParse and OpenAI**: This workflow automates the extraction of data from invoices received as email attachments. It triggers on new Gmail messages, sends the attached PDF to LlamaParse for advanced parsing, and then uses OpenAI to structure the extracted text into a clean JSON format. The structured data is then appended to a Google Sheet for reconciliation.

309. **Manipulate PDF with Adobe developer API**: This workflow serves as a wrapper for the Adobe PDF Services API. It demonstrates how to authenticate, upload a PDF asset, trigger a processing job (like splitting or extracting data), and then download the resulting file. It's a good example of how to interact with a multi-step, asynchronous API.

310. **Parse PDF with LlamaParse and save to Airtable**: This workflow automates the processing of invoices from Google Drive. When a new invoice PDF is uploaded, it's sent to LlamaParse. A webhook receives the parsed data, which is then processed by OpenAI to extract line items. Finally, the structured invoice and line item data are saved to separate tables in Airtable.

311. **Prepare CSV files with GPT-4**: A utility workflow that uses GPT-4 to generate mock user data in JSON format. It then processes this JSON, converts it into a CSV file, and saves it to disk. This is useful for creating sample data for testing other workflows.

312. **Remove Personally Identifiable Information (PII) from CSV Files with OpenAI**: This workflow takes a CSV file, processes it row by row, and uses an OpenAI model to identify and remove Personally Identifiable Information (PII) from specified fields. The cleaned data is then compiled into a new CSV file.
313. **ETL pipeline for text processing**: This workflow demonstrates a classic ETL (Extract, Transform, Load) process. It triggers on a schedule, searches for tweets with a specific hashtag, stores them in MongoDB, analyzes their sentiment with Google Cloud Natural Language, and then loads the tweet and its sentiment score into a PostgreSQL database. It also sends a Slack notification for tweets with a positive sentiment.

314. **Extract and process information directly from PDF using Claude and Gemini**: This workflow compares the capabilities of Anthropic's Claude 3.5 Sonnet and Google's Gemini 2.0 Flash for direct PDF data extraction. It fetches a PDF from Google Drive, converts it to a base64 string, and sends it to both models with the same prompt to extract specified information, allowing for a side-by-side comparison of their performance.

315. **Extract data from resume and create PDF with Gotenberg**: This workflow processes resumes submitted via Telegram. It extracts the text from the PDF, uses OpenAI to parse it into a structured JSON format, converts the various sections (personal info, employment history, etc.) into HTML, and then uses the Gotenberg API to merge these HTML sections into a newly generated, well-formatted PDF.

316. **Extract license plate number from image uploaded via an n8n form**: A straightforward vision AI workflow. A user uploads an image of a car via an n8n form, and the workflow uses a vision-capable model (via OpenRouter) to extract the license plate number from the image and displays it on the form's completion page.

317. **Extract text from PDF and image using Vertex AI (Gemini) into CSV**: This workflow automates data extraction from documents in a Google Drive folder. It triggers when a new file is added, routes PDFs and images through different processing paths (text extraction for PDFs, Gemini Vision for images), uses an AI model to structure the extracted text into CSV format with categories, and uploads the final CSV file back to Google Drive.
318. **AI-Powered Information Monitoring with OpenAI, Google Sheets, Jina AI and Slack**: This workflow automates the process of monitoring RSS feeds for relevant information. It periodically fetches articles from URLs listed in a Google Sheet, uses an AI model to classify their relevance, scrapes the content of relevant articles with Jina AI, summarizes them with OpenAI, and posts the formatted summaries to a Slack channel.

319. **Creating an AI Slack Bot with Google Gemini**: This workflow sets up a simple AI-powered Slack bot using Google Gemini. It listens for messages via a webhook, processes the user's query with an AI agent that maintains conversation history, and sends the generated response back to the Slack channel.

320. **Customer Support Channel and Ticketing System with Slack and Linear**: This workflow streamlines customer support by creating a ticketing system between Slack and Linear. It periodically scans a designated Slack channel for messages marked with a ticket emoji, uses an AI model to generate a title and summary, and then creates a new issue in Linear, preventing duplicate tickets.

321. **Enhance Security Operations with the Qualys Slack Shortcut Bot!**: This workflow acts as a central hub for security operations within Slack. Using a Slack Shortcut, users can open a modal to either initiate a new vulnerability scan or generate a report from a previous scan. The workflow then routes this request to the appropriate sub-workflow to interact with the Qualys API, streamlining security tasks directly from the chat interface.
322. **Enrich Pipedrive's Organization Data with OpenAI GPT-4o & Notify it in Slack**: When a new organization is created in Pipedrive, this workflow scrapes the company's website, uses OpenAI to generate a summary of its services and potential competitors, and adds this information as a note to the Pipedrive organization. It then formats the note and sends a notification to a Slack channel.

323. **IT Ops AI SlackBot Workflow - Chat with your knowledge base**: This workflow creates an IT Ops Slack bot that can answer questions by searching a knowledge base. It uses a custom sub-workflow to query a Confluence instance. The AI agent receives a user's question from Slack, uses the tool to search Confluence, and then formulates a helpful response.

324. **Sentiment Analysis Tracking on Support Issues with Linear and Slack**: This workflow periodically fetches recent issues from Linear, uses an AI model to analyze the sentiment of the comments within each issue, and stores the sentiment analysis in an Airtable base. It also includes a trigger that sends a Slack notification if an issue's sentiment changes from non-negative to negative.

325. **Slack slash commands AI Chat Bot**: This workflow demonstrates how to create a Slack bot that responds to slash commands. It uses a webhook to receive commands, a switch node to route different commands (e.g., `/ask`, `/another`), and an AI model to generate a response, which is then posted back to the Slack channel.
326. **Venafi Cloud Slack Cert Bot**: This workflow provides a Slack bot for requesting TLS certificates from Venafi Cloud. Users can trigger a Slack shortcut to open a modal, enter a domain name, and request a certificate. The workflow then uses the VirusTotal API to check the domain's reputation. If the domain is clean, the certificate is automatically issued. If not, a report is generated for manual approval.
327. **DeepSeek AI Agent + Telegram + LONG TERM Memory** (`1/Telegram/🐋🤖 DeepSeek AI Agent + Telegram + LONG TERM Memory 🧠.txt`): This workflow creates a sophisticated Telegram bot powered by a DeepSeek AI agent. It features long-term memory, using a Google Doc to store and retrieve user-specific information, allowing for personalized conversations. The bot is designed to handle various message types, including text, audio, and images, routing them through different processing logic. It also incorporates a user validation step to ensure that it only interacts with authorized users.

328. **Telegram Messaging Agent for Text/Audio/Images** (`1/Telegram/🤖 Telegram Messaging Agent for Text_Audio_Images.txt`): This workflow sets up a multi-modal Telegram messaging agent capable of processing text, audio, and image inputs. It uses OpenAI's Whisper model to transcribe audio messages and the `gpt-4o-mini` model to analyze incoming images. Text-based conversations are handled by a language model to provide intelligent responses. The workflow also includes tools for setting up and managing the Telegram webhook and for validating user identities.

329. **AI Agent Chatbot + LONG TERM Memory + Note Storage + Telegram** (`1/Telegram/🤖🧠 AI Agent Chatbot + LONG TERM Memory + Note Storage + Telegram.txt`): This workflow implements an advanced AI chatbot for Telegram that is equipped with both long-term memory and a separate note-taking function. Both capabilities are powered by Google Docs, allowing the agent to distinguish between conversational memories and specific user notes. The agent uses a DeepSeek model to interact with users and is triggered by incoming chat messages.

330. **Agentic Telegram AI bot with LangChain nodes and new tools** (`1/Telegram/Agentic Telegram AI bot with with LangChain nodes and new tools.txt`): This workflow creates an agentic AI bot for Telegram built with LangChain nodes. The agent, powered by the `gpt-4o` model, is equipped with custom tools that allow it to generate images using DALL-E 3 and send them directly to the user within the chat. It maintains conversational context using a window buffer memory, enabling more coherent and extended interactions.

331. **AI-Powered Children's Arabic Storytelling on Telegram** (`1/Telegram/AI-Powered Children_s Arabic Storytelling on Telegram.txt`): This creative workflow automates the generation and delivery of children's stories in Arabic to a Telegram channel. Triggered by a schedule, it uses `gpt-4-turbo` to write a new story, translates the text into Arabic, generates a unique illustration for the story using DALL-E, and creates an audio narration. The complete package of text, image, and audio is then published to the designated Telegram channel.
332. **AI-Powered Children's English Storytelling on Telegram with OpenAI** (`1/Telegram/AI-Powered Children_s English Storytelling on Telegram with OpenAI.txt`): This workflow automates the creation and distribution of children's stories in English to a Telegram channel. It runs on a 12-hour schedule, using OpenAI's `gpt-3.5-turbo-16k-0613` model to generate a new story. It then creates a DALL-E prompt to generate a relevant image and also generates an audio version of the story. The text, image, and audio are all sent to the specified Telegram channel.

333. **Angie, Personal AI Assistant with Telegram Voice and Text** (`1/Telegram/Angie, Personal AI Assistant with Telegram Voice and Text.txt`): This workflow creates "Angie," a personal AI assistant on Telegram that can handle both text and voice messages. It uses OpenAI's Whisper for speech-to-text and `gpt-4o-mini` as its core language model. Angie is equipped with several tools, allowing it to fetch unread emails from Gmail, retrieve events from Google Calendar, and access information from Baserow tables for tasks and contacts.

334. **Automated AI image analysis and response via Telegram** (`1/Telegram/Automated AI image analysis and response via Telegram.txt`): This workflow provides automated analysis of images sent to a Telegram bot. When an image is received, it is sent to OpenAI for analysis. The workflow then returns the analysis result to the user in the Telegram chat. It includes a switch to handle cases where a message without an image is sent, prompting the user to upload one.

335. **Chat with OpenAI's GPT via a simple Telegram Bot** (`1/Telegram/Chat with OpenAIs GPT via a simple Telegram Bot.txt`): This workflow sets up a straightforward Telegram bot that allows users to chat with an OpenAI GPT model. It uses a Telegram Trigger to listen for incoming messages, passes the text to an AI Agent, and then sends the agent's response back to the user in the same chat.

336. **Detect toxic language in Telegram messages** (`1/Telegram/Detect toxic language in Telegram messages.txt`): This workflow acts as a content moderator for a Telegram chat. It uses the Google Perspective API to analyze incoming messages for toxicity, specifically looking at identity attack, threat, and profanity. If the profanity score exceeds a certain threshold (0.7), the bot will reply to the offending message with a warning.
337. **Image Creation with OpenAI and Telegram** (`1/Telegram/Image Creation with OpenAI and Telegram.txt`): This workflow allows users to generate images by sending a text prompt to a Telegram bot. The bot receives the message, uses OpenAI to generate an image based on the text, and then sends the resulting image back to the user in the same chat.

338. **Send a random recipe once a day to Telegram** (`1/Telegram/Send a random recipe once a day to Telegram.txt`): This workflow delivers a random vegan recipe to a list of Telegram users daily. It has two main parts: a user registration system and a daily recipe sender. New users are welcomed and their chat IDs are stored in Airtable. A cron job then triggers daily to fetch a random recipe from the Spoonacular API and sends it to all registered users.

339. **Telegram AI bot assistant ready-made template for voice & text messages** (`1/Telegram/Telegram AI bot assistant_ ready-made template for voice & text messages.txt`): This workflow provides a template for a multi-format AI assistant on Telegram. It can process both text and voice messages, using OpenAI's Whisper for transcription and `gpt-4o` for generating responses. The bot is designed to handle different message types and includes error handling for unsupported formats.

340. **Telegram AI bot with LangChain nodes** (`1/Telegram/Telegram AI bot with LangChain nodes.txt`): This workflow creates a sophisticated Telegram AI bot using LangChain nodes. The bot, powered by `gpt-4-1106-preview`, can engage in conversations and use a custom tool to generate images with DALL-E 3. The image generation is handled by a sub-workflow, which is triggered by the main agent when a user requests an image.

341. **Telegram AI Bot NeurochainAI Text & Image - NeurochainAI Basic API Integration** (`1/Telegram/Telegram AI Bot_ NeurochainAI Text & Image - NeurochainAI Basic API Integration.txt`): This workflow demonstrates a basic integration with the NeurochainAI API for a Telegram bot. The bot can respond to text messages using a Llama 3.1 model and can also handle image generation requests. It includes logic to process different commands and handle potential errors during API calls.
342. **Telegram AI Chatbot** (`1/Telegram/Telegram AI Chatbot.txt`): This workflow creates a multi-functional AI chatbot for Telegram. It can handle regular chat conversations, respond to a `/start` command with a greeting, and generate images using the `/image` command. It uses a `gpt-4` model for its conversational abilities and OpenAI's image generation for the image command. A switch node is used to route the user's message to the correct logic based on the command.

343. **Telegram Bot with Supabase memory and OpenAI assistant integration** (`1/Telegram/Telegram Bot with Supabase memory and OpenAI assistant integration.txt`): This workflow builds a Telegram bot that uses an OpenAI assistant and has its memory powered by a Supabase database. It checks if a user already exists in the `telegram_users` table. If not, it creates a new OpenAI thread for the user and saves the new user's information to Supabase. This allows the bot to maintain conversational history and provide a more personalized experience.

344. **Telegram chat with PDF** (`1/Telegram/Telegram chat with PDF.txt`): This workflow enables a user to "chat" with a PDF document through Telegram. When a user uploads a PDF, it is processed, chunked, and its embeddings are stored in a Pinecone vector store. When a user asks a question, the workflow retrieves relevant information from the PDF in Pinecone and uses a Groq chat model (Llama 3.1) to generate an answer based on the document's content.

345. **Telegram to Spotify with OpenAI** (`1/Telegram/Telegram to Spotify with OpenAI.txt`): This workflow allows a user to control their Spotify playback through Telegram. A user can send a song request (e.g., "play 'Bohemian Rhapsody' by Queen") to the bot. OpenAI's `gpt-4o-mini` is used to extract the track and artist from the message. The workflow then searches for the song on Spotify, adds it to the queue, skips to it, and resumes playback.

346. **Translate Telegram audio messages with AI (55 supported languages)** (`1/Telegram/Translate Telegram audio messages with AI (55 supported languages).txt`): This workflow creates a universal translator bot for Telegram. It can take an audio message in one of 55 supported languages, transcribe it using OpenAI's Whisper, translate the text to a target language, and then respond with both the translated text and a new audio file of the translation. The native and target languages are configurable within the workflow.