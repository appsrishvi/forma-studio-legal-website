# Forma Studio — Legal Website (hosting package)

**Prepared:** 3 November 2026  
**Scope:** Public legal pages for the Forma Studio Android design application and related cloud services.  
**Basis:** `forma_latest_app.zip`, `forma_admin_portal.zip`, `database_supabase.txt` and the app's existing `forma-legal-site/index.html`. Legal text is a carefully drafted publication candidate, not a substitute for review of the live backend or legal advice.

## Files

| File | Use |
| --- | --- |
| `privacy-policy.html` | Public privacy policy for Google Play and in-app links |
| `terms-of-service.html` | Public terms of service for in-app links |
| `account-deletion.html` | Clear external account deletion request instructions |
| `index.html` | Same deletion page, **intentionally retained** so an existing Play Console link to the old website root continues to lead to account deletion |
| `styles.css` | Shared responsive, accessible styling; no external CSS or JavaScript dependencies |
| `assets/forma_mark.svg`, `.png` | Existing app brand artwork |
| `robots.txt` | Allows search-engine indexing |

## Upload to hosting

1. Unzip this package and **upload the files and `assets` directory together** to the public website directory (e.g. Hostinger `public_html/`, or a chosen `/legal/` subdirectory). Do not upload only the two HTML pages without `styles.css` and `assets`.
2. Use HTTPS, and confirm each page is publicly available without login:
   - `https://YOUR-DOMAIN/privacy-policy.html`
   - `https://YOUR-DOMAIN/terms-of-service.html`
   - `https://YOUR-DOMAIN/account-deletion.html`
   - `https://YOUR-DOMAIN/` — account deletion, for compatibility with the previously supplied deletion-page index.
3. In **Google Play Console**, use the public privacy-policy URL in the Privacy Policy field. For app-account deletion, use the public account-deletion URL in the designated account-deletion field.
4. Add working Privacy Policy and Terms links inside the **Forma Studio mobile application**. The reviewed `studio_shell.dart` currently opens a *short hardcoded local dialog*, not these external pages; that should be updated in the app before claiming that users see the published documents.
5. Verify every link on Android, desktop, and mobile browsers. Confirm the email inbox `support@rishvi.co.uk` is monitored and accepts deletion requests.

If the legal files are served from a subfolder, keep all files in **the same subfolder** except the `assets` directory, which should remain directly inside that subfolder; relative links will work.

## Required factual and legal sign-off BEFORE going live

- [ ] **Operator identity:** Confirm the registered legal entity or owner of Forma Studio and publish any name, registered address, and grievance/contact details required by applicable law. The supplied app materials provide the product name and support email, but not a verified legal operator name or postal address. The pages avoid inventing these facts.
- [ ] **Email:** Confirm `support@rishvi.co.uk` is your official support/privacy mailbox (it came from the existing deletion page in your app ZIP).
- [ ] **Live deletion behavior:** Test the deployed Supabase RPC `delete_user_account`. The mobile app invokes this function; its deployed SQL implementation is not present in the submitted database schema. Confirm it really deletes `auth.users`, `profiles` and `user_designs` as intended, handles any other user data, and is not blocked by audit/role FK constraints. Verify the user sees errors if deletion fails.
- [ ] **Cloud data scope:** The reviewed mobile `saveUserDesign` writes `template_id`, `template_version`, `title`, `values` (user-entered text), `export_path`, timestamps, and `user_id` to the Supabase `user_designs` table. Photos and PNGs are saved locally in the reviewed flow. Check the current live build for any additional uploads, logging, SDKs or processors and adjust the policy if these exist.
- [ ] **Translation vendors:** The client can call `forma-translate` and fall back to Google Translate and MyMemory. Client comments describe the edge function as Gemini-backed. Verify exactly which processor is deployed and what happens to text sent to each vendor; make sure any processing and provider-specific disclosures are appropriate.
- [ ] **Retention:** Confirm server backup, auth-log, and audit-log retention periods with the deployed Supabase configuration. The supplied code cannot establish exact time periods. Update the site with specific retention commitments if needed for legal or platform compliance.
- [ ] **Legal decisions:** Confirm the proposed use license for exported designs, the minimum-age approach, and India governing-law language align with your actual business, target audience, and asset licenses. Have qualified counsel approve the final documents if you need legal assurance.
- [ ] **Data safety:** Reconcile the actual deployed app and SDK data flows with the Google Play Data safety form. Disclose any newly added analytics, ads, marketing, payments, advertising identifiers, or remote image processing.
- [ ] **In-app consistency:** The current local Terms dialog in `studio_shell.dart` says all rendered graphics and uploaded assets are the user's "exclusive intellectual property" and describes "encrypted Supabase storage." This should be replaced with accurate text and links to the published Terms and Privacy Policy, which more carefully distinguish user-owned content from licensed templates and device-local images.

The Indian Digital Personal Data Protection framework includes phased commencement. Review the law applicable on **the actual publication date** and keep the documents updated as obligations take effect. A policy page alone does not implement notice, consent, deletion, data security, or grievance procedures.

## Why the root page is account deletion

The uploaded app includes an existing public `forma-legal-site/index.html` headed **Account Deletion & Data Erasure**, apparently prepared for Google Play. This package keeps `index.html` as account deletion and also adds `account-deletion.html`, so an old root URL continues to provide the same user function even after you upload the new Terms and Privacy Policy pages.

## Technical notes

- Static HTML and CSS; no build step or PHP/Node/backend required.
- No external fonts, trackers, scripts, cookies, or CDN dependencies added by these pages.
- Semantic HTML, focus indicators, skip links, section navigation, responsive layout, and print CSS included.
- Links are **relative** so site works in a root folder or subdirectory.
- Effective date is **3 November 2026**. Change it when you make substantive revisions.

## Official requirements to revisit

- Google Play User Data Policy: https://support.google.com/googleplay/android-developer/answer/10144311
- Google Play account deletion guidance: https://support.google.com/googleplay/android-developer/answer/13327111
- Ministry of Electronics and IT, DPDP Rules: https://www.meity.gov.in/documents/act-and-policies/digital-personal-data-protection-rules-2025-gDOxUjMtQWa
