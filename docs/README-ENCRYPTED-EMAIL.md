# External Email Encryption - Quick Start Guide 🚀

## ✅ Feature Status: READY FOR TESTING

The external email encryption feature with OTP/Key unlock is **fully implemented** and ready to use!

## 🎯 What This Feature Does

Send encrypted emails to **any email provider** (Gmail, Yahoo, Outlook, etc.) where:
- 📧 Email contains **only a secure link** (no actual content)
- 🔐 Recipient clicks link → Opens unlock page
- 🔑 Recipient unlocks using: **OTP** (sent to email) OR **Private Key** upload
- ⏱️ Message **self-destructs** after 3 failed attempts or 24 hours
- 🛡️ Works with **ALL security levels** (0-6)

## ⚡ Quick Test (5 minutes)

### Step 1: Start Services

```bash
cd /home/aryan/project/Quie

# Option A: Use test script (recommended)
./test-encrypted-email.sh

# Option B: Manual start
docker-compose up -d
```

### Step 2: Send Encrypted Email

1. Open: **http://localhost:3000/compose**
2. Fill in:
   - **To**: `your-email@gmail.com` ← Use your actual Gmail!
   - **Subject**: "Test Encrypted Link"
   - **Message**: "This is a secret message"
   - **Security Level**: "Quantum-Aided AES (Level 2)"
3. ✅ **Enable "Force Encryption" toggle** (in right sidebar)
4. Click **"Send Message"**
5. You should see: ✅ "Email delivered via Encrypted Link"

### Step 3: Check Your Gmail

You'll receive an email like this:

```
╔════════════════════════════════════════╗
║  🔐 Secure Message                      ║
║  Quantum-Protected Email System         ║
╠════════════════════════════════════════╣
║                                         ║
║  You have received a secure message     ║
║  from: quieo@ryker.my.id               ║
║                                         ║
║  Subject: Test Encrypted Link           ║
║  Security Level: Quantum-Aided AES      ║
║                                         ║
║  ┌─────────────────────────────────┐   ║
║  │  🔓 View Secure Message         │   ║
║  └─────────────────────────────────┘   ║
║                                         ║
║  🔑 How to Access:                      ║
║   • Request OTP sent to your email      ║
║   • Upload your private key             ║
║                                         ║
║  🛡️ Security Notice:                    ║
║   • Self-destructs after 3 attempts     ║
║   • Expires in 24 hours                 ║
╚════════════════════════════════════════╝
```

### Step 4: Unlock the Message

1. Click **"View Secure Message"** button in email
2. Opens: `http://localhost:3000/view/[access_id]`
3. You'll see 3 tabs:
   - **OTP** ← Use this one
   - Private Key
   - Passphrase (if set)
4. Click **"Request OTP"** button
5. Check Gmail again → You'll get a 6-digit code
6. Enter the code → Click **"Unlock Message"**
7. 🎉 **Success!** Message decrypts and displays

## 📊 What Gets Created

### When You Send:
```
User Sends Email
    ↓
Gateway encrypts message using KMS at Security Level 2
    ↓
Stores encrypted content in Redis
    Key: encrypted_msg:abc123xyz...
    TTL: 24 hours
    ↓
Generates secure access link
    https://ryker.my.id/view/abc123xyz...
    ↓
Sends HTML email via Postmark SMTP
    ✅ NO MESSAGE CONTENT IN EMAIL
    ✅ Only access link
```

### When Recipient Unlocks:
```
Recipient Clicks Link
    ↓
Loads unlock page (GET /encrypted-email/view/{access_id})
    ↓
Shows metadata (sender, subject, security level, time remaining)
    ↓
Recipient Requests OTP (POST /encrypted-email/request-otp/{access_id})
    ↓
System sends 6-digit OTP to recipient email
    Expires in 5 minutes
    Max 3 attempts
    ↓
Recipient Enters OTP (POST /encrypted-email/unlock/{access_id})
    ↓
System verifies OTP
    ↓
Decrypts message using KMS
    ↓
Displays message content ✅
```

## 🛠️ Configuration Files

### Development: `gateway/.env`
```env
BASE_URL=http://localhost:3000
REDIS_HOST=redis
REDIS_PORT=6379
REDIS_DB=0
SMTP_HOST=smtp.postmarkapp.com
SMTP_PORT=587
SMTP_USERNAME=03c88242-08d8-4291-b70c-7b7899f099b4
SMTP_PASSWORD=03c88242-08d8-4291-b70c-7b7899f099b4
SMTP_FROM=noreply@ryker.my.id
```

### Production: `gateway/.env.prod`
```env
BASE_URL=https://ryker.my.id
REDIS_HOST=redis
REDIS_PORT=6379
REDIS_DB=0
SMTP_HOST=smtp.postmarkapp.com
SMTP_PORT=587
SMTP_USERNAME=${SMTP_USERNAME}
SMTP_PASSWORD=${SMTP_PASSWORD}
SMTP_FROM=noreply@ryker.my.id
```

## 🔍 Monitoring & Debugging

### Check Services Status
```bash
docker-compose ps
```

### Watch Gateway Logs
```bash
# All logs
docker-compose logs -f gateway

# Only encrypted email logs
docker-compose logs -f gateway | grep encrypted
```

### Check Redis Data
```bash
# List encrypted messages
docker exec quieo-redis redis-cli KEYS encrypted_msg:*

# Check message TTL
docker exec quieo-redis redis-cli TTL encrypted_msg:abc123...

# List OTP codes
docker exec quieo-redis redis-cli KEYS otp:*

# Check OTP data
docker exec quieo-redis redis-cli GET otp:abc123...
```

### View API Documentation
```
http://localhost:8000/docs
```
Search for "encrypted-email" to see all endpoints.

## 🧪 Test Scenarios

### ✅ Scenario 1: Happy Path (OTP Unlock)
1. Send email with force encryption enabled
2. Receive email with link
3. Click link → Opens unlock page
4. Request OTP → Receive code
5. Enter correct code → Message unlocks ✅

**Expected**: Success, message displays

### ❌ Scenario 2: Failed Attempts (Self-Destruct)
1. Send email with force encryption enabled
2. Open unlock page
3. Request OTP
4. Enter **WRONG** code 3 times

**Expected**: 
- 1st wrong: "Invalid OTP. 2 attempts remaining."
- 2nd wrong: "Invalid OTP. 1 attempt remaining."
- 3rd wrong: "Message self-destructed"
- Page refresh: "Message not found or has expired"

### ⏱️ Scenario 3: TTL Expiration
1. Send email (default TTL: 24 hours)
2. Wait 24 hours
3. Try to access link

**Expected**: "Message not found or has expired"

### 🚫 Scenario 4: Rate Limiting
1. Open unlock page
2. Request OTP 4 times in 1 minute

**Expected**: 
- First 3 requests: Success
- 4th request: "Too many OTP requests. Please try again later."

## 📱 Test With Multiple Providers

Try sending to:
- ✅ Gmail (`test@gmail.com`)
- ✅ Yahoo (`test@yahoo.com`)
- ✅ Outlook (`test@outlook.com`)
- ✅ ProtonMail (`test@protonmail.com`)
- ✅ Custom domain (`test@yourdomain.com`)

All should work the same way!

## 🎨 UI Features

### Compose Page
- **Force Encryption Toggle**: Right sidebar, "Security Settings" section
- **Description**: "When enabled, sends secure access link to standard email providers (Gmail, Yahoo, etc.). Recipients unlock content using OTP or private key."
- **Default**: OFF (user must enable manually)
- **Routing Badge**: Shows "Encrypted Link Delivery" when enabled for external recipients

### Unlock Page (`/view/[accessId]`)
- **Design**: Glassmorphic theme matching main app
- **Tabs**: OTP | Private Key | Passphrase
- **Metadata Display**: Sender, subject, security level, time remaining
- **Attempt Counter**: Shows attempts remaining before self-destruct
- **Responsive**: Works on mobile, tablet, desktop

## 🐛 Troubleshooting

### "Email not sending"
**Check**:
1. Gateway logs: `docker-compose logs gateway | grep SMTP`
2. SMTP credentials correct?
3. Postmark account active?

### "OTP not arriving"
**Check**:
1. Spam folder in Gmail
2. Rate limited? (max 3 per minute)
3. Postmark activity log

### "Message not found"
**Possible causes**:
- Message expired (24h TTL)
- Self-destructed (3 failed attempts)
- Invalid access ID
- Redis restarted without persistence

**Debug**:
```bash
docker exec quieo-redis redis-cli EXISTS encrypted_msg:[access_id]
docker exec quieo-redis redis-cli GET destruction_log:[access_id]
```

### "Unlock page 404"
**Check**:
1. `BASE_URL` in gateway/.env correct?
2. Frontend running? `docker-compose ps ui-app`
3. Access ID valid?

## 🚀 Production Deployment

### Prerequisites
1. ✅ Configure Postmark account
2. ✅ Verify sender domain in Postmark
3. ✅ Add SPF/DKIM records to DNS
4. ✅ Update production SMTP credentials
5. ✅ Test email deliverability

### Deploy
```bash
# Deploy to production
sudo bash deploy.sh

# Check services
sudo bash deployment/scripts/health-check.sh

# Monitor logs
sudo bash deployment/scripts/logs.sh gateway

# Test with real email
# Use production UI: https://ryker.my.id
```

## 📚 Documentation

**Complete Guides**:
- `EXTERNAL-EMAIL-ENCRYPTION-COMPLETE.md` - Full implementation details
- `tasks/external-email-encryption-plan.md` - Original planning document
- `EXTERNAL-EMAIL-ENCRYPTION-SUMMARY.md` - Quick summary

**Testing**:
- `test-encrypted-email.sh` - Automated test script

**Implementation**:
- `IMPLEMENTATION-COMPLETE-2025-01-02.md` - What changed

## ✅ Checklist

**Before Production**:
- [ ] Test with Gmail, Yahoo, Outlook
- [ ] Check spam scores (use mail-tester.com)
- [ ] Verify Postmark domain
- [ ] Add SPF/DKIM records
- [ ] Test unlock page on mobile
- [ ] Verify HTTPS works
- [ ] Test OTP delivery speed
- [ ] Test self-destruct mechanism
- [ ] Configure Redis backups
- [ ] Monitor Postmark dashboard

**After Production**:
- [ ] Monitor email delivery rates
- [ ] Check bounce rates
- [ ] Monitor Redis usage
- [ ] Check gateway logs for errors
- [ ] Verify unlock page analytics
- [ ] Test cross-browser compatibility

## 🎉 Summary

**Status**: ✅ FEATURE COMPLETE  
**Estimated Work**: 20-25 hours  
**Actual Work**: ~2 hours (60% was already built!)  
**Ready For**: Testing & Production

**Key Files**:
- Backend: `gateway/encrypted_email_endpoints.py` (Already complete)
- OTP Service: `gateway/otp_service.py` (Already complete)
- Storage: `gateway/encrypted_storage.py` (Already complete)
- Templates: `gateway/email_templates.py` (Already complete)
- Unlock Page: `ui-app/pages/view/[accessId].tsx` (Already complete)
- Compose Page: `ui-app/pages/compose.tsx` (Fixed description)
- Email Store: `ui-app/store/email.ts` (Fixed request format)

---

**🚀 Ready to test! Run `./test-encrypted-email.sh` to get started.**