# FYP King — GTM Setup Guide
**GTM ID:** GTM-PB2WNSDS  
**Facebook Pixel ID:** 1640902397253149  
**Site:** https://fyp-king-mobile.vercel.app

---

## ✅ ইতোমধ্যে index.html-এ যা আছে
- [x] GTM Head Script (`<head>` এ)
- [x] GTM Body noscript (`<body>` এর পরে)
- [x] Facebook Pixel Base Code (init + PageView)
- [x] dataLayer Events সব বাটনে

---

## GTM-এ এখন যা করতে হবে

### STEP 1 — tagmanager.google.com যাও → GTM-PB2WNSDS খোলো

---

### STEP 2 — Variables চেক করো
**Variables → Configure → Built-In Variables এ টিক দাও:**
- ✅ Click URL
- ✅ Click Text  
- ✅ Click Element
- ✅ Page URL
- ✅ Scroll Depth Threshold

---

### STEP 3 — Triggers তৈরি করো

**Triggers → New:**

#### Trigger 1: APK Download Click
- Name: `Trigger - APK Download`
- Type: `Custom Event`
- Event Name: `apk_download`
- Save ✅

#### Trigger 2: WhatsApp Contact Click
- Name: `Trigger - WhatsApp Contact`
- Type: `Custom Event`
- Event Name: `whatsapp_contact`
- Save ✅

#### Trigger 3: Bkash Number Copy
- Name: `Trigger - Bkash Copy`
- Type: `Custom Event`
- Event Name: `bkash_number_copy`
- Save ✅

#### Trigger 4: Activate Button Click
- Name: `Trigger - Activate Click`
- Type: `Custom Event`
- Event Name: `activate_click`
- Save ✅

#### Trigger 5: Engaged Visit (60 seconds)
- Name: `Trigger - 60s Engaged`
- Type: `Custom Event`
- Event Name: `time_on_page`
- Save ✅

---

### STEP 4 — Tags তৈরি করো

#### Tag 1: FB Pixel — APK Download (Lead)
- Name: `FB - APK Download Lead`
- Tag Type: `Custom HTML`
- HTML:
```html
<script>
  if(window.fbq){
    fbq('track', 'Lead');
    fbq('trackCustom', 'APK_Download');
  }
</script>
```
- Trigger: `Trigger - APK Download`
- Save ✅

#### Tag 2: FB Pixel — WhatsApp Contact
- Name: `FB - WhatsApp Contact`
- Tag Type: `Custom HTML`
- HTML:
```html
<script>
  if(window.fbq){ fbq('track', 'Contact'); }
</script>
```
- Trigger: `Trigger - WhatsApp Contact`
- Save ✅

#### Tag 3: FB Pixel — Bkash Copy (Interest Signal)
- Name: `FB - Bkash Copy`
- Tag Type: `Custom HTML`
- HTML:
```html
<script>
  if(window.fbq){ fbq('trackCustom', 'BkashCopy'); }
</script>
```
- Trigger: `Trigger - Bkash Copy`
- Save ✅

#### Tag 4: FB Pixel — Activate Click (InitiateCheckout)
- Name: `FB - Activate Button`
- Tag Type: `Custom HTML`
- HTML:
```html
<script>
  if(window.fbq){ fbq('track', 'InitiateCheckout'); }
</script>
```
- Trigger: `Trigger - Activate Click`
- Save ✅

#### Tag 5: FB Pixel — Engaged Visit
- Name: `FB - Engaged Visit`
- Tag Type: `Custom HTML`
- HTML:
```html
<script>
  if(window.fbq){ fbq('trackCustom', 'EngagedVisit'); }
</script>
```
- Trigger: `Trigger - 60s Engaged`
- Save ✅

---

### STEP 5 — Publish করো
1. উপরে **Submit** বাটন ক্লিক করো
2. Version Name: `v2 - FB Pixel Full Tracking`
3. **Publish** ক্লিক করো ✅

---

### STEP 6 — Verify করো

#### Browser Console চেক:
1. Chrome-এ `fyp-king-mobile.vercel.app` খোলো
2. F12 → Console ট্যাব
3. দেখবে: `[FYP King] GTM Tracking Active ✅ GTM-PB2WNSDS`

#### Facebook Events Manager চেক:
1. business.facebook.com → Events Manager
2. Pixel ID: `1640902397253149` সিলেক্ট করো
3. **Test Events** ট্যাব খোলো
4. তোমার site URL বসাও → Open Website
5. ডাউনলোড বাটনে ক্লিক করো
6. Events Manager-এ রিয়েল-টাইম `Lead` ইভেন্ট দেখবে ✅

---

## Facebook-এ যে Events আসবে

| Event Name | কখন Fire হবে | Ads-এ কীভাবে ব্যবহার করবে |
|---|---|---|
| `PageView` | প্রতিবার পেজ লোড হলে | Awareness Campaign Audience |
| `Lead` | APK ডাউনলোড বাটনে ক্লিক | Conversion Campaign Optimize |
| `APK_Download` | APK ডাউনলোড বাটনে ক্লিক | Custom Conversion |
| `InitiateCheckout` | Activate বাটনে ক্লিক | Purchase Funnel |
| `Contact` | WhatsApp বাটনে ক্লিক | Retargeting Audience |
| `BkashCopy` | Bkash নম্বর কপি | Hot Lead Audience |
| `EngagedVisit` | ৬০ সেকেন্ড সাইটে থাকলে | Quality Audience |

---

## Facebook Ads Campaign Strategy

### Campaign 1 — Awareness (Broad)
- Objective: `Reach` বা `Traffic`
- Audience: Bangladesh, 18-35, মোবাইল ইউজার
- Optimize: `Landing Page Views`

### Campaign 2 — Conversion (Hot)
- Objective: `Leads`
- Pixel Event: `Lead` (APK Download Click)
- Audience: Lookalike — যারা আগে `PageView` করেছে

### Campaign 3 — Retargeting
- Objective: `Conversions`
- Audience: Custom — যারা `PageView` করেছে কিন্তু `Lead` হয়নি
- এই মানুষগুলো সাইটে এসেছে কিন্তু ডাউনলোড করেনি — তাদের আবার দেখাও

---

## ⚠️ গুরুত্বপূর্ণ নোট
- Pixel verify হতে ২৪-৪৮ ঘণ্টা লাগতে পারে
- iOS 14+ এ কিছু ডেটা miss হতে পারে — Conversions API পরে সেটআপ করো
- GTM Preview Mode দিয়ে সব ইভেন্ট আগে টেস্ট করো
