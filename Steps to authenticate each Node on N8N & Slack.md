Steps to authenticate Google Drive triggers:  
<br/>**Create a Google Cloud Project:**

- Go to the Google Cloud Console.
- Create a new project or select an existing one.

**Enable the Google Drive API:**

- In your Google Cloud project, go to “APIs & Services” > “Library”.
- Search for “Google Drive API” and enable it.

**Create OAuth 2.0 Credentials:**

- Go to “APIs & Services” > “Credentials”.
- Click “Create Credentials” > “OAuth client ID”.
- Set the application type to “Web application”.
- Add the following to “Authorized redirect URIs”:
  - https://&lt;your-n8n-domain&gt;/rest/oauth2-credential/callback
  - If running locally (through Docker), add: <http://localhost:5678/rest/oauth2-credential/callback>  

**Copy the Client ID and Client Secret.  
**

**In n8n:**

- Go to “Credentials” and create new “Google” credentials.
- Paste your Client ID and Client Secret.
- Authenticate by following the OAuth flow.  

**Use the credentials in your Google Drive Trigger node.**

**  
For the HTTP Request (in case of a word doc):  
<br/>**In addition to the client ID and client Secret, add the scope to the API Key as ‘www.googleapis.com/auth/drive’

Steps to Authenticate OpenAI Node:  
<br/>**Get Your OpenAI API Key:**

- Log in to your OpenAI account.
- Go to the API keys page: <https://platform.openai.com/api-keys>
- Click “Create new secret key” and copy the generated key.  

**(Optional) Get Your Organization ID:**

- If you belong to multiple organizations, go to your Organization Settings: <https://platform.openai.com/account/organization>
- Copy your Organization ID. If you don’t have multiple organizations, you can leave this blank in n8n.

**Add Credentials in n8n:**

- In n8n, go to “Credentials” and create new “OpenAI” credentials.
- Paste your API Key (and Organization ID if needed).
- Save the credentials.

**Use the Credentials:**

- In your OpenAI node, select the credentials you just created.

Steps to Authenticate Anthropic Claude Node:  
<br/>**Get Your Anthropic API Key:**

- Log in to your Anthropic Console: <https://console.anthropic.com>
- Go to Settings > API Keys: <https://console.anthropic.com/settings/keys>
- Click “+ Create Key”, give it a name (e.g., n8n-integration), and copy the generated key.

**Add Credentials in n8n:**

- In n8n, go to “Credentials” and create new “Anthropic” credentials.
- Paste your API Key into the “API Key” field.
- Save the credentials.

**Use the Credentials:**

- In your Anthropic node (e.g., Anthropic Chat Model), select the credentials you just created.

Steps to Authenticate all OAuth 2.0 Credential Logins:

- Slack, Gmail: Simply sign in to your account!
- Hubspot: Marketplace access for apps must be provided to accounts before signing in to N8N.
- LinkedIn: Created a separate document for this purpose.  

Steps to Authenticate Slash and add the App and Slash Command:

- Sign in to your workspace on <https://api.slack.com/apps>
- Create an app with an appropriate name signalling the problem trying to be solved. For example, I used ‘Generate a LinkedIn Post’.
- Go to Features -> Slash Commands -> Create New Command:
  - Command: /linkedin-post
  - Request URL: <https://maxcareeros.app.n8n.cloud/webhook-test/slack-gilfoyle>
  - Short Description: Takes the input as topic for generating a LinkedIn post
  - SAVE
- Head back to Settings -> Install App
- Click on Install. (Note: Every time you make a change or add a new Slash Command, reinstall the App)
