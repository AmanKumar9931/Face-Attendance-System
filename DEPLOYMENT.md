# 🚀 DEPLOYMENT GUIDE - Railway.app

Your FaceAttend system is ready for production! Follow these steps to deploy it live.

---

## **Step 1: Prepare Your Local Repository**

If you haven't already, initialize git locally:

```bash
cd c:\Users\amanr\Desktop\face-attendance-system-main\face-attendance-system-main
git init
git add .
git commit -m "Initial commit: FaceAttend v2.0 ready for production"
```

---

## **Step 2: Create a GitHub Repository**

1. Go to [github.com/new](https://github.com/new)
2. Create a new repository:
   - **Repository name:** `face-attendance-system`
   - **Description:** AI-powered face recognition attendance system
   - **Visibility:** Public (for easier Railway deployment)
   - **Skip README** (we have one)
   - Click **Create Repository**

3. Connect your local repo to GitHub:

```bash
git remote add origin https://github.com/YOUR_USERNAME/face-attendance-system.git
git branch -M main
git push -u origin main
```

---

## **Step 3: Deploy on Railway.app**

### **3.1 Create Railway Account**
- Go to [railway.app](https://railway.app)
- Sign up with GitHub (easiest option)
- Grant repository access

### **3.2 Create New Project**
- Click **+ New Project** → **Deploy from GitHub repo**
- Select your `face-attendance-system` repository
- Railway will auto-detect the Python app

### **3.3 Configure Environment Variables**
Once the project is created:

1. Go to **Variables** section
2. Add the following (copy from `.env.example`):

```
FLASK_ENV=production
FLASK_SECRET_KEY=<generate a random 32-char string>
ADMIN_USERNAME=admin
ADMIN_PASSWORD=<change this!>
EMAIL_SENDER=<your-gmail@gmail.com>
EMAIL_PASSWORD=<your-gmail-app-password>
EMAIL_ENABLED=false
ANTHROPIC_API_KEY=<optional: your Claude API key>
```

⚠️ **Important:**
- Generate a strong `FLASK_SECRET_KEY` (use [this tool](https://generate-secret-key.herokuapp.com/))
- Change `ADMIN_PASSWORD` from default "admin123"
- Don't commit `.env` file to GitHub!

### **3.4 Deploy**
- Railway will automatically deploy when you push changes
- Your app will be live at: `https://<project-name>.railway.app`

---

## **Step 4: First-Time Setup (After Deployment)**

Once your app is live:

1. Open your Railway app URL
2. Login with admin credentials you set in environment variables
3. Test face registration and attendance marking
4. Configure email (Gmail):
   - Create an [App Password](https://myaccount.google.com/apppasswords)
   - Add to `EMAIL_SENDER` and `EMAIL_PASSWORD` environment variables
   - Set `EMAIL_ENABLED=true`

---

## **Step 5: Custom Domain (Optional)**

1. In Railway Dashboard → **Settings** → **Domains**
2. Add custom domain: `attendance.yourcompany.com`
3. Configure DNS records as shown by Railway

---

## **Troubleshooting**

### **Build Fails**
- Check the build logs in Railway Dashboard
- Ensure all dependencies in `requirements.txt` are Python packages
- Face_recognition requires system libraries (Railway has them)

### **App Crashes at Startup**
- Check **Logs** in Railway Dashboard
- Ensure `FLASK_SECRET_KEY` is set (not empty)
- Verify database path is writable

### **Face Recognition Not Working**
- Ensure camera/image upload works in browser
- Check browser console for JavaScript errors
- Verify OpenCV can access video device

### **Email Not Sending**
- Verify Gmail App Password (not regular password)
- Check `EMAIL_ENABLED=true` in environment variables
- Test with a known email address in database

---

## **What's Included**

✅ **app.py** — Flask backend with all features  
✅ **Procfile** — Railway deployment config  
✅ **runtime.txt** — Python version  
✅ **requirements.txt** — Dependencies  
✅ **.env.example** — Environment template  
✅ **templates/** — HTML frontend  

---

## **Key Security Notes**

🔒 **Before going live:**
- [ ] Change admin password from "admin123"
- [ ] Set `FLASK_SECRET_KEY` to a random 32-character string
- [ ] Never commit `.env` to GitHub
- [ ] Configure SSL/TLS (Railway handles this automatically)
- [ ] Consider rate limiting for login attempts
- [ ] Review student data privacy policy

---

## **Performance Tips**

📈 **To improve performance:**
- Use Railway's PostgreSQL add-on for larger deployments
- Add CDN for static files (CSS, JS)
- Enable caching headers in Flask
- Monitor Railway dashboard for resource usage

---

## **Next Steps**

1. ✅ Push code to GitHub
2. ✅ Connect Railway to GitHub repo
3. ✅ Set environment variables
4. ✅ Deploy and test
5. ✅ Share your live URL!

---

**Questions?** Check the README.md or Railway's documentation at [docs.railway.app](https://docs.railway.app)

Happy deploying! 🎉
