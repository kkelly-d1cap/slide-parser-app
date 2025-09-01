# Step 3: Set Up AWS S3 Storage (45 minutes)

## 🎯 What We're Doing
Setting up cloud storage for your slide images. Think of this like creating a Google Drive folder that your website can access to show images.

---

## 📋 **Part A: Create AWS Account (10 minutes)**

### 1. Go to AWS
- **Open your browser** and go to: `https://aws.amazon.com`
- **Click "Create an AWS Account"**

### 2. Fill Out Account Information
```
Email address:     [Your work email]
Password:          [Strong password]
AWS account name:  [Your Company Name - Slide Parser]
```

### 3. Contact Information
```
Account type:      [Business] (recommended)
Company name:      [Your Company Name]
Phone number:      [Your work phone]
Address:           [Your company address]
```

### 4. Payment Information
- **Enter credit card** (required, but we'll set up billing alerts)
- **AWS has a free tier** - you likely won't be charged for months

### 5. Identity Verification
- **Phone verification** (they'll call or text you)
- **Enter the verification code**

### 6. Choose Support Plan
- **Select "Basic support - Free"**
- **Click "Complete sign up"**

---

## 📋 **Part B: Create S3 Bucket (15 minutes)**

### 1. Access S3 Service
- **Sign in to AWS Console**
- **Search for "S3"** in the search bar
- **Click "S3"** from the results

### 2. Create Bucket
- **Click "Create bucket"**

### 3. Configure Bucket Settings
```
Bucket name: [yourcompany-slide-parser-images]
             (must be globally unique - try variations)
             
Region:      [US East (N. Virginia) us-east-1]
             (must match your Heroku region)
```

### 4. Configure Permissions
**Block Public Access Settings:**
- **UNCHECK all 4 boxes** (we need public access for images)
- **Check "I acknowledge..."** warning box

**Bucket Versioning:**
- **Leave as "Disable"**

**Default Encryption:**
- **Leave as default**

### 5. Create Bucket
- **Click "Create bucket"**
- **You should see your bucket** in the S3 dashboard

---

## 📋 **Part C: Configure Bucket Permissions (10 minutes)**

### 1. Set Bucket Policy
- **Click on your bucket name**
- **Go to "Permissions" tab**
- **Scroll down to "Bucket policy"**
- **Click "Edit"**

### 2. Copy/Paste This Policy
**Replace `yourcompany-slide-parser-images` with your actual bucket name:**

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::yourcompany-slide-parser-images/*"
        }
    ]
}
```

### 3. Save Policy
- **Click "Save changes"**
- **You should see "Successfully edited bucket policy"**

---

## 📋 **Part D: Create Access Keys (10 minutes)**

### 1. Go to IAM Service
- **Search for "IAM"** in AWS console
- **Click "IAM"** from results

### 2. Create New User
- **Click "Users"** in left sidebar
- **Click "Add users"**
- **User name**: `slide-parser-app`
- **Select "Programmatic access"**
- **Click "Next: Permissions"**

### 3. Set Permissions
- **Click "Attach existing policies directly"**
- **Search for "S3"**
- **Check "AmazonS3FullAccess"**
- **Click "Next: Tags"** (skip tags)
- **Click "Next: Review"**
- **Click "Create user"**

### 4. Save Your Keys
**⚠️ IMPORTANT: Save these immediately - you can't see them again!**

```
Access Key ID:     AKIA... (copy this)
Secret Access Key: wJal... (copy this)
```

**Save these in a secure note** - you'll need them for Heroku.

---

## 📋 **Part E: Connect S3 to Heroku (5 minutes)**

### 1. Go Back to Heroku
- **Open your Heroku app dashboard**
- **Go to Settings → Config Vars**

### 2. Update Environment Variables
**Add the values you just got from AWS:**

```
AWS_ACCESS_KEY_ID:     [Paste your Access Key ID]
AWS_SECRET_ACCESS_KEY: [Paste your Secret Access Key]
S3_BUCKET_NAME:        [Your bucket name]
```

### 3. Restart Your App
- **Click "More" → "Restart all dynos"**
- **Wait 30 seconds** for restart

---

## ✅ **Checkpoint: AWS S3 Complete**

### Test Your S3 Integration:
1. **Go to your Netlify site**
2. **Upload a test PDF**
3. **If it works**: You should be able to select slides and generate HTML
4. **If it fails**: Check the troubleshooting section below

### What You've Accomplished:
- ✅ **AWS account created**
- ✅ **S3 bucket configured for public access**
- ✅ **IAM user created with proper permissions**
- ✅ **Heroku connected to S3**

---

## 🚨 **Common Issues & Quick Fixes**

### **Issue: "Access Denied" errors**
**Fix:**
- Double-check bucket policy has your exact bucket name
- Make sure all 4 "Block public access" settings are unchecked
- Verify IAM user has S3FullAccess policy

### **Issue: "Invalid credentials"**
**Fix:**
- Double-check Access Key ID and Secret Key in Heroku
- Make sure there are no extra spaces when copying/pasting
- Regenerate keys if needed (IAM → Users → slide-parser-app → Security credentials)

### **Issue: "Bucket not found"**
**Fix:**
- Check S3_BUCKET_NAME in Heroku matches your actual bucket name exactly
- Make sure bucket is in us-east-1 region
- Verify bucket was created successfully

---

## 💰 **AWS Billing Setup (Important!)**

### Set Up Billing Alerts:
1. **Go to AWS Billing Dashboard**
2. **Click "Billing preferences"**
3. **Enable "Receive billing alerts"**
4. **Set alert for $10/month** (you'll likely use $5-15/month)

### Expected Costs:
```
S3 Storage (1000 presentations): ~$15/month
S3 Requests:                     ~$2/month
Data Transfer:                   ~$3/month
Total Expected:                  ~$20/month
```

---

## 📞 **Need Help?**

### **AWS Support:**
- **Documentation**: `https://docs.aws.amazon.com/s3/`
- **Community Forum**: `https://forums.aws.amazon.com`
- **Basic Support**: Included with account

### **What to Say:**
*"I'm setting up S3 for a web application to store images. I need help with [specific issue] following a deployment guide."*

---

## ➡️ **Next Step**

**Once your S3 is working (PDF upload succeeds):**
- **Continue to Step 4**: Final testing and team training
- **Your app is basically done!**

**Your complete app URLs:**
- **Main App**: `https://your-site.netlify.app`
- **Backend**: `https://yourcompany-slide-parser.herokuapp.com`
- **Storage**: `https://yourcompany-slide-parser-images.s3.amazonaws.com`

---

## 🎉 **Almost There!**

**Congratulations!** You now have:
- ✅ **Working backend** on Heroku
- ✅ **Working frontend** on Netlify  
- ✅ **Working file storage** on AWS S3
- ✅ **All services connected** and communicating

**One more step and you'll be saving 650 hours per year!**

