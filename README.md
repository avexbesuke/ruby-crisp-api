# ruby-crisp-api

The Crisp API Ruby wrapper. Authenticate, send messages, fetch conversations, access your agent accounts from your Ruby code.

Copyright 2019 Crisp IM SARL. See LICENSE for copying information.

* **📝 Implements**: [Crisp Platform - API ~ v1](https://docs.crisp.chat/api/v1/) at reference revision: 12/31/2017
* **😘 Maintainer**: [@valeriansaliou](https://github.com/valeriansaliou)

## Usage

Add the library to your `Gemfile`:

```bash
gem 'crisp-api', '~> 1.0'
```

Then, import it:

```ruby
require 'crisp-api'
```

Build a new authenticated Crisp client with your `identifier` and `key` tokens.

```ruby
client = Crisp::Client.new

client.authenticate(identifier, key)
```

Then, your client is ready to be consumed!

## Authentication

To authenticate against the API, generate your session identifier and session key **once** using the [Crisp token generation utility](https://go.crisp.chat/account/token/). You'll get a token keypair made of 2 values.

**Keep your token keypair values private, and store them safely for long-term use.**

Then, add authentication parameters to your `client` instance right after you create it:

```ruby
client = Crisp::Client.new

# Authenticate to API (identifier, key)
# eg. client.authenticate("5c0595b2-9381-4a76-a2e0-04aa00c1ede7", "3bdb0812d0f5352bf68901ddc731434dade419b98507971905acdd2f967df61c")
client.authenticate(identifier, key)

# Now, you can use authenticated API sections.
```

**🔴 Important: Make sure to generate your token once, and use the same token keys in all your subsequent requests to the API. Do not generate too many tokens, as we may invalidate your older tokens to make room for newer tokens.**

## Resource Methods

Most useful available Crisp API resources are implemented. **Programmatic methods names are named after their label name in the [API Reference](https://docs.crisp.chat/api/v1/)**.

Thus, it is straightforward to look for them in the library while reading the [API Reference](https://docs.crisp.chat/api/v1/).

In the following method prototypes, `crisp` is to be replaced with your Crisp API instance. For example, instanciate `client = Crisp()` and then call eg: `client.website.list_conversations(website_id, 1)`.

When calling a method that writes data to the API (eg. send a message with: `client.website.send_message_in_conversation()`), you need to submit it this way:

```ruby
website_id = "6497e4a4-b17c-41e0-bfea-eea97ba8115a"
session_id = "session_f32bc993-f7ce-41af-bcd1-110fc147a392"

client.website.send_message_in_conversation(
  website_id, session_id,

  {
    "type" => "text",
    "content" => "This message was sent from python-crisp-api! :)",
    "from" => "operator",
    "origin" => "chat"
  }
)
```

### Website

* **Website Conversations**
  * **List Conversations**: `client.website.list_conversations(website_id, page_number)`

* **Website Conversation**
  * **Create A New Conversation**: `client.website.create_new_conversation(website_id)`
  * **Check If Conversation Exists**: `client.website.check_conversation_exists(website_id, session_id)`
  * **Get A Conversation**: `client.website.get_conversation(website_id, session_id)`
  * **Remove A Conversation**: `client.website.remove_conversation(website_id, session_id)`
  * **Initiate A Conversation With Existing Session**: `client.website.initiate_conversation_with_existing_session(website_id, session_id)`
  * **Get Messages In Conversation**: `client.website.get_messages_in_conversation(website_id, session_id, query)`
  * **Send A Message In Conversation**: `client.website.send_message_in_conversation(website_id, session_id, query)`
  * **Update A Message In Conversation**: `client.website.update_message_in_conversation(website_id, session_id, fingerprint, data)`
  * **Compose A Message In Conversation**: `client.website.compose_message_in_conversation(website_id, session_id, data)`
  * **Mark Messages As Read In Conversation**: `client.website.mark_messages_read_in_conversation(website_id, session_id, data)`
  * **Mark Messages As Delivered In Conversation**: `client.website.mark_messages_delivered_in_conversation(website_id, session_id, data)`
  * **Get Conversation Routing Assign**: `client.website.get_conversation_routing_assign(website_id, session_id)`
  * **Assign Conversation Routing**: `client.website.assign_conversation_routing(website_id, session_id, data)`
  * **Get Conversation Metas**: `client.website.get_conversation_metas(website_id, session_id)`
  * **Update Conversation Metas**: `client.website.update_conversation_metas(website_id, session_id, data)`
  * **List Conversation Pages**: `client.website.list_conversation_pages(website_id, session_id, page_number)`
  * **List Conversation Events**: `client.website.list_conversation_events(website_id, session_id, page_number)`
  * **Get Conversation State**: `client.website.get_conversation_state(website_id, session_id)`
  * **Change Conversation State**: `client.website.change_conversation_state(website_id, session_id, data)`
  * **Get Block Status For Conversation**: `client.website.get_block_status_for_conversation(website_id, session_id)`
  * **Block Incoming Messages For Conversation**: `client.website.block_incoming_messages_for_conversation(website_id, session_id, data)`
  * **Request Email Transcript For Conversation**: `client.website.request_email_transcript_for_conversation(website_id, session_id, data)`

* **Website People**
  * **Get People Statistics**: `client.website.get_people_statistics(website_id)`
  * **List People Segments**: `client.website.list_people_segments(website_id, page_number)`
  * **List People Profiles**: `client.website.list_people_profiles(website_id, page_number)`
  * **Add New People Profile**: `client.website.add_new_people_profile(website_id, data)`
  * **Check If People Profile Exists**: `client.website.check_people_profile_exists(website_id, people_id)`
  * **Get People Profile**: `client.website.get_people_profile(website_id, people_id)`
  * **Save People Profile**: `client.website.save_people_profile(website_id, people_id, data)`
  * **Find People Profile By Email**: `client.website.find_people_profile_by_email(website_id, email)`
  * **Update People Profile**: `client.website.update_people_profile(website_id, people_id, data)`
  * **Remove People Profile**: `client.website.remove_people_profile(website_id, people_id)`
  * **List People Conversations**: `client.website.list_people_conversations(website_id, people_id, page_number)`
  + **Add A People Event**: `client.website.add_people_event(website_id, people_id, data)`
  + **List People Events**: `client.website.list_people_events(website_id, people_id, page_number)`
  + **Get People Data**: `client.website.get_people_data(website_id, people_id)`
  + **Save People Data**: `client.website.save_people_data(website_id, people_id, data)`
  + **Get People Subscription Status**: `client.website.get_people_subscription_status(website_id, people_id)`
  + **Update People Subscription Status**: `client.website.update_people_subscription_status(website_id, people_id, data)`

* **Website Base**
  * **Create Website**: `client.website.create_website(data)`
  * **Get A Website**: `client.website.get_website(website_id)`
  * **Delete A Website**: `client.website.delete_website(website_id)`

* **Website Batch**
  * **Batch Resolve Items**: `client.website.batch_resolve_items(website_id, data)`
  * **Batch Read Items**: `client.website.batch_read_items(website_id, data)`
  * **Batch Remove Items**: `client.website.batch_remove_items(website_id, data)`

* **Website Availability**
  * **Get Website Availability Status**: `client.website.get_website_availability_status(website_id)`

* **Website Operator**
  * **List Website Operators**: `client.website.list_website_operators(website_id)`
  * **List Last Active Website Operators**: `client.website.list_last_active_website_operators(website_id)`

* **Website Settings**
  * **Get Website Settings**: `client.website.get_website_settings(website_id)`
  * **Update Website Settings**: `client.website.update_website_settings(website_id, data)`

* **Website Visitors**
  * **Count Visitors**: `client.website.count_visitors(website_id)`
  * **List Visitors**: `client.website.list_visitors(website_id, page_number)`
  * **Get Session ID**: `client.website.get_session_id_from_token(website_id, token)`

### Bucket

* **Bucket URL**
  * **Generate Bucket URL**: `client.bucket.generate_bucket_url(data)`

