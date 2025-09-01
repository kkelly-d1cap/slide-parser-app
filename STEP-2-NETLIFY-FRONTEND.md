# Step 2: Deploy Frontend to Netlify (30 minutes)

## 🎯 What We're Doing
Setting up the "face" of your Slide Parser app on Netlify. This is the website your team will visit to use the application.

---

## 📋 **Part A: Create Netlify Account (5 minutes)**

### 1. Go to Netlify
- **Open your browser** and go to: `https://netlify.com`
- **Click "Sign up"** (top right corner)

### 2. Choose Sign-Up Method
**Recommended:** Sign up with GitHub (easier for future updates)
- **Click "Sign up with GitHub"**
- **Authorize Netlify** to access your GitHub account

**Alternative:** Sign up with email
- **Enter your email and password**
- **Verify your email address**

### 3. Complete Profile
- **Skip team setup** (click "Skip" if prompted)
- **You should see the Netlify dashboard**

---

## 📋 **Part B: Deploy Your Frontend (10 minutes)**

### 1. Deploy Site
- **Click "Add new site"** (or "Deploy to Netlify")
- **Select "Deploy manually"**

### 2. Upload Your Files
- **Drag and drop** the `frontend-for-netlify.zip` file I provided
- **OR click "browse to upload"** and select the zip file
- **Netlify will automatically extract** and deploy

### 3. Wait for Deployment
- **You'll see "Site deploy in progress"**
- **Wait 1-2 minutes** for completion
- **You'll get a random URL** like `https://amazing-app-123456.netlify.app`

### 4. Test Your Site
- **Click the generated URL**
- **You should see the Slide Parser interface**
- **Try entering fund information** (it should work)

---

## 📋 **Part C: Configure Backend Connection (10 minutes)**

### 1. Update Frontend Configuration
**Problem:** Your frontend needs to know where your backend is.

**Solution:** Update the API URL in your frontend code.

#### **Easy Method: Site Settings**
- **Go to Site settings** in Netlify dashboard
- **Click "Environment variables"**
- **Add new variable:**
  ```
  Key: VITE_API_BASE_URL
  Value: https://yourcompany-slide-parser.herokuapp.com/api/slides
  ```
- **Click "Save"**
- **Trigger new deploy** (Site overview → Deploys → "Trigger deploy")

#### **Alternative: Code Update**
If environment variables don't work:
1. **Download your frontend source code**
2. **Edit `src/App.jsx`**
3. **Find line with `localhost:5000`**
4. **Replace with your Heroku URL**
5. **Re-build and re-upload**

### 2. Update CORS Settings
- **Go back to your Heroku app**
- **Settings → Config Vars**
- **Update ALLOWED_ORIGINS:**
  ```
  Value: https://your-netlify-site.netlify.app
  ```
- **Replace with your actual Netlify URL**

---

## 📋 **Part D: Test Integration (5 minutes)**

### 1. Test the Connection
- **Go to your Netlify site**
- **Enter fund information**
- **Try uploading a PDF**

### 2. Expected Results:
**✅ Success:** Upload works, shows "Processing PDF..."
**❌ Error:** "Failed to fetch" or CORS error

### 3. If You Get Errors:
**Most Common Issue:** CORS configuration
- **Double-check** your Netlify URL in Heroku ALLOWED_ORIGINS
- **Make sure** there are no typos
- **Wait 2-3 minutes** for changes to take effect
- **Try again**

---

## ✅ **Checkpoint: Frontend Complete**

**If you can upload a PDF without errors, your frontend is working!**

### What You've Accomplished:
- ✅ **Netlify account created**
- ✅ **Frontend deployed and accessible**
- ✅ **Backend connection configured**
- ✅ **CORS properly set up**

### Your App URLs:
- **Frontend (Main App)**: `https://your-site.netlify.app`
- **Backend API**: `https://yourcompany-slide-parser.herokuapp.com`

---

## 🎨 **Optional: Custom Domain (10 minutes)**

### If You Want a Custom URL:
Instead of `amazing-app-123456.netlify.app`, you can have `slideparser.yourcompany.com`

### Steps:
1. **Buy a domain** (GoDaddy, Namecheap, etc.) - $15/year
2. **In Netlify**: Site settings → Domain management → Add custom domain
3. **Follow DNS instructions** (copy/paste DNS records)
4. **Wait 24 hours** for DNS propagation

### Benefits:
- **Professional appearance**
- **Easier to remember**
- **Company branding**

---

## 🚨 **Common Issues & Quick Fixes**

### **Issue: "Site not found" or 404 error**
**Fix:** 
- Make sure you uploaded the `dist/` folder contents, not the whole project
- Check that `index.html` is in the root of your upload

### **Issue: "Failed to fetch" when uploading PDF**
**Fix:**
- Check ALLOWED_ORIGINS in Heroku matches your Netlify URL exactly
- Make sure both HTTP and HTTPS are included if needed
- Wait 2-3 minutes after changing config vars

### **Issue: "CORS error" in browser console**
**Fix:**
- Update ALLOWED_ORIGINS in Heroku to include your Netlify URL
- Make sure there are no trailing slashes in URLs
- Restart your Heroku app (More → Restart all dynos)

---

## 📞 **Need Help?**

### **Netlify Support:**
- **Help Center**: `https://docs.netlify.com`
- **Community Forum**: `https://community.netlify.com`
- **Live Chat**: Available in Netlify dashboard

### **What to Say:**
*"I'm deploying a React application and need help with [specific issue]. I'm following a deployment guide and got stuck at [specific step]."*

---

## ➡️ **Next Step**

**Once your frontend can upload PDFs without errors:**
- **Continue to Step 3**: Set up AWS S3 for file storage
- **Keep your Netlify URL** - you'll need it for AWS configuration

**Your frontend URL will be something like:**
`https://amazing-app-123456.netlify.app`

**Write this down - you'll need it for Step 3!**

---

## 🎉 **You're Halfway Done!**

**Great job!** You now have:
- ✅ **Working backend** processing PDFs
- ✅ **Working frontend** with upload interface
- ✅ **Both services talking** to each other

**Next up:** Set up AWS S3 so your slide images get stored in the cloud and you can generate the final HTML code!

