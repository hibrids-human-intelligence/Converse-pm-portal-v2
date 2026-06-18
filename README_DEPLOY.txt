CONVERSE CANDIDATE PORTAL V2 — GITHUB PAGES

UPLOAD THESE FILES TO THE ROOT OF THE EXISTING GITHUB REPOSITORY:
- index.html
- auth.html
- .nojekyll

CONFIGURED MICROSOFT 365 VALUES
Tenant ID: 3fc5d812-da80-4742-9a7c-03013dfd9059
Client ID: 4947d026-0d22-4128-8a85-1dd657679d1b
Site ID: hibrids.sharepoint.com,a09fa3b1-f238-4cfe-ab0e-0697fdb08431,3a348495-b353-43e0-87b6-a8d8cbcbe993
List ID: f4567c4f-aafe-4386-bd70-bfc3fd1d8ccd
List: CandidateList2

ENTRA API PERMISSIONS
The app requests these delegated Microsoft Graph permissions:
- Sites.ReadWrite.All — read and save evaluations
- Sites.Manage.All — create missing list columns automatically

In Microsoft Entra admin center:
1. App registrations > open client ID 4947d026-0d22-4128-8a85-1dd657679d1b
2. API permissions > Add a permission > Microsoft Graph > Delegated permissions
3. Add Sites.ReadWrite.All and Sites.Manage.All
4. Grant admin consent

REDIRECT URI
Keep/add the exact GitHub Pages auth address under Authentication > Single-page application.
For the existing repository this is normally:
https://hibrids-human-intelligence.github.io/Converse-pm-portal/auth.html

The code calculates auth.html relative to the deployed repository, so it can also work if the repository name changes, provided the new exact auth.html URL is registered in Entra.

SHAREPOINT SCHEMA
On first successful administrator sign-in, the portal checks CandidateList2 and creates these missing columns automatically:
- VacancyKey
- CandidateId
- CandidateName
- EvaluatorKey
- EvaluatorName
- EvaluationData (multiline JSON)
- LastSavedAt
- Source

Title is the standard SharePoint column and is reused as the unique record key.

DATA MODEL
One SharePoint item is stored per Vacancy + Candidate + Evaluator. Scores, comments, recommendation and final comments are kept in EvaluationData JSON. This preserves the portal analytics while avoiding hundreds of rows.

DEPLOYMENT
Replace the existing GitHub Pages files, commit, and wait for Pages deployment. Test the GitHub URL directly before embedding it in Framer. Use an external URL iframe, not srcdoc.


STRICT ACCESS MODE
------------------
This build does not expose the vacancy selector until Microsoft 365 sign-in succeeds and CandidateList2 can be read. It does not load or persist evaluations from browser localStorage. If authentication or SharePoint access fails, the password gate remains locked.
