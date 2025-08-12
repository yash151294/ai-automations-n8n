**1) Create a LinkedIn Developer App**

- Go to the LinkedIn Developer Portal, sign in, and select My Apps → Create App.
- Fill required details (App name, company page if you plan to post as an organization, logo, privacy policy URL), accept terms, and create the app.
- In the app’s Products tab, request:
- Share on LinkedIn (required to post).
- Sign In with LinkedIn using OpenID Connect (needed for OAuth flow).
- After provisioning, open the Auth tab and copy Client ID and Client Secret for later.

Tip: If you plan to post on behalf of a Company Page, make sure the app is associated with that page and that your account has Admin rights for the page.

**2) Add n8n’s Redirect URI in LinkedIn**

- In the LinkedIn app → Auth, add n8n’s Authorized Redirect (Callback) URL exactly as shown in the n8n LinkedIn credential screen, then save.
- A mismatch here will cause OAuth failures; ensure the URL matches character-for-character.

**3) Create LinkedIn credentials in n8n**

- In n8n, add a LinkedIn node (or go to Credentials) and Create new Credential.
- Paste the LinkedIn Client ID and Client Secret.
- If posting as a Company Page, enable Organizational Support in the n8n LinkedIn credential; if posting only as a person, leave organizational support disabled.
- Save the credential, then click Connect to complete the OAuth sign-in and grant permissions.

Common issues:

Bad Request when posting as an organization usually means missing organizational permission or you tried to post “as organization” without enabling organizational support and page access; switch to Post as: Person or fix org access and try again.

**4) Build a minimal test workflow in n8n**

- Add a Set (or Edit Fields) node to provide sample text, e.g., text: "This is a post via n8n".
- Add a LinkedIn node:
- Resource: Post → Operation: Create.
- Post As: Person (for first test), then choose your profile from Person Name or ID dropdown.
- Text: Reference the text field from the previous node (e.g., {{$json.text}}).
- For images/links, set Media Category appropriately and ensure images are binary from the immediately preceding node if uploading images.
- Run Once to test; verify the post appears on your profile feed.

**Notes for images:**

The LinkedIn node expects a binary image generated/available in the node directly before it; often you’ll re-create or re-fetch the image right before the LinkedIn node so it passes as binary correctly.

**5) Post to a Company Page (optional)**

- Ensure your LinkedIn app and account have permissions to post as the organization and that you’re a Page Admin.
- In the LinkedIn node:

Post As: Organization

Organization URN: Enter just the numeric ID (e.g., 1234567), not the full urn:li:company:1234567 string

- If you receive authorization errors, revisit:
- Organizational Support toggled in n8n credential.
- App’s product access approved and linked to your page.
- Your account’s Page Admin role.

**6) Automate and extend (optional)**

- Add a Schedule Trigger to post at set times, or pull content from Google Sheets/Notion/RSS and pass into the LinkedIn node.
- Add an AI step (OpenAI or similar) to generate post copy before the LinkedIn node, plus an approval step via email or chat if desired.

**7) Troubleshooting checklist**

- OAuth fails: Confirm the exact Redirect URL is added in LinkedIn and matches n8n’s credential screen.
- Bad Request on organization post: Switch to Post as Person to confirm base setup works; then enable Organizational Support and ensure page admin + product access before retrying Organization posting.
- Can’t see profile/page selectors: Make sure the credential is connected successfully and the correct Post As mode is selected.
- Image upload fails: Ensure the image is binary and supplied by the immediately preceding node.
