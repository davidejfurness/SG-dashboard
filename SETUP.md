# Quick Setup Guide

## Deploy to GitHub Pages in 5 Minutes

### Step 1: Create GitHub Repository
1. Go to https://github.com/new
2. Repository name: `shelford-dashboard` (or your choice)
3. Description: "NHS performance dashboard for Shelford Group trusts"
4. Set to **Public**
5. Click "Create repository"

### Step 2: Upload Files
From your terminal:

```bash
cd shelford-dashboard  # Navigate to your project directory
git init
git add .
git commit -m "Initial commit: Shelford Group dashboard"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/shelford-dashboard.git
git push -u origin main
```

### Step 3: Enable GitHub Pages
1. Go to your repository on GitHub
2. Click **Settings** (top right)
3. Click **Pages** (left sidebar)
4. Under "Source":
   - Branch: `main`
   - Folder: `/ (root)`
5. Click **Save**

### Step 4: Wait for Deployment
- GitHub will build and deploy your site
- Usually takes 1-2 minutes
- Your site will be live at: `https://YOUR-USERNAME.github.io/shelford-dashboard/`

### Step 5: Test Your Dashboard
Visit your deployed site and check:
- ✓ Landing page loads correctly
- ✓ Performance dashboard displays
- ✓ Trust comparison page works
- ✓ Charts render properly

## Customizing Your Dashboard

### Update Trust Data
1. Edit `fetch_data.py` to add NHS API calls
2. Run: `python fetch_data.py`
3. Commit and push changes

### Change Styling
Edit CSS variables in any HTML file:
```css
:root {
    --nhs-blue: #005EB8;          /* Primary brand color */
    --shelford-teal: #007B7F;     /* Secondary color */
    --bg-cream: #FDFBF7;          /* Background */
}
```

### Add New Pages
1. Create new HTML file (e.g., `new-page.html`)
2. Copy structure from existing page
3. Add link in `index.html`
4. Commit and push

## Automated Data Updates

The GitHub Action in `.github/workflows/update-data.yml` will:
- Run daily at midnight UTC
- Fetch latest NHS data
- Update dashboard automatically
- No manual intervention needed

To trigger manually:
1. Go to repository on GitHub
2. Click **Actions** tab
3. Select "Update NHS Data"
4. Click "Run workflow"

## Connecting to Real NHS Data

### Option 1: NHS England Data Dashboard
```python
# In fetch_data.py
import requests

def fetch_ae_data():
    url = "https://data.england.nhs.uk/api/..."  # Add actual endpoint
    response = requests.get(url)
    return response.json()
```

### Option 2: NHS Digital CSV Downloads
```python
import pandas as pd

def fetch_rtt_data():
    url = "https://digital.nhs.uk/data/.../file.csv"
    df = pd.read_csv(url)
    # Filter for Shelford trusts
    shelford_data = df[df['OrgCode'].isin(SHELFORD_TRUSTS.keys())]
    return shelford_data
```

### Option 3: Organisation Data Service API
```python
def get_trust_details(ods_code):
    url = f"https://directory.spineservices.nhs.uk/ORD/2-0-0/organisations/{ods_code}"
    response = requests.get(url)
    return response.json()
```

## Troubleshooting

### Dashboard Not Loading?
- Check GitHub Pages is enabled
- Verify files committed to `main` branch
- Check browser console for errors (F12)

### Charts Not Displaying?
- Ensure Chart.js CDN is accessible
- Check browser console for JavaScript errors
- Verify chart data format in HTML files

### Data Not Updating?
- Check GitHub Actions logs in "Actions" tab
- Verify `fetch_data.py` runs without errors
- Ensure data files in `data/` directory

### Python Script Errors?
```bash
# Install dependencies
pip install -r requirements.txt

# Test script locally
python fetch_data.py

# Check for errors in output
```

## Next Steps

1. **Review Data Sources**: Check `data/data_sources.json`
2. **Implement API Calls**: Update `fetch_data.py` with real NHS APIs
3. **Test Locally**: Open `index.html` in browser before pushing
4. **Monitor Actions**: Check GitHub Actions runs successfully
5. **Share Dashboard**: Send link to colleagues

## Support

- **Issues**: Open GitHub issue in your repository
- **NHS Data Help**: https://digital.nhs.uk/services
- **Shelford Group**: https://shelfordgroup.org

---

**Pro Tips:**
- Commit early, commit often
- Test changes locally before pushing
- Use meaningful commit messages
- Keep README.md updated with changes
