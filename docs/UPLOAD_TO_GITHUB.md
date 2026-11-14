# Upload this portfolio to GitHub

**Do not upload only the ZIP as one repository file** if you want a browsable portfolio.

1. Extract `SOC-Monitoring-Incident-Response-Lab_GitHub_Ready.zip` on your computer.
2. In GitHub, create a new repository, e.g. `SOC-Monitoring-Incident-Response-Lab`.
3. **Start as a Private repository** until you finish the privacy review in `docs/PUBLICATION_CHECKLIST.md`.
4. Select **Add file → Upload files** and upload the *contents of the extracted project folder*, including `README.md`, `.gitignore`, `Configurations`, `Reports`, `Screenshots` and `docs`. If your browser doesn't preserve folders, use GitHub Desktop or Git.
5. Commit the upload. Open the repository homepage and ensure README images load and PDFs open.
6. Review/redact any hostnames/IP addresses/usernames you prefer not to publish. Publish the repository when ready.
7. Add the public repository URL to your LinkedIn **Projects** section and CV portfolio link.

### Optional Git command line

```bash
git init
git add .
git commit -m "Publish Wazuh SOC lab portfolio"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/SOC-Monitoring-Incident-Response-Lab.git
git push -u origin main
```

Run these commands from inside the extracted project folder, after creating the empty remote repository. Replace `YOUR-USERNAME` with your actual account name.
