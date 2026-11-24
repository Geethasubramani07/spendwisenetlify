# SpendWise on Netlify (JavaScript conversion)

This Netlify-only edition keeps the existing static dashboard but replaces the FastAPI/Python backend with a JavaScript Netlify Function and Netlify Blobs storage. Categorisation is keyword-based and anomaly detection uses transparent spending heuristics; it is **not** the original scikit-learn / Isolation Forest model.

## Deploy
1. Push the complete repository to GitHub.
2. In Netlify choose **Add new site → Import an existing project** and connect the repository.
3. Build settings are read from `netlify.toml`: publish directory `app/static`, functions directory `netlify/functions`. No build command is needed.
4. In Site configuration → Environment variables, set `ADMIN_TOKEN` to a long random secret.
5. Deploy. The first call to the API initializes Netlify Blobs storage.

## Important
- Netlify Blobs stores the app's JSON state. This is suitable for a small student demo, not concurrent/high-volume financial workloads.
- Do not upload real bank statements or sensitive financial data.
- Test demo data, CSV import, category budgets, alerts and reset after deployment.
