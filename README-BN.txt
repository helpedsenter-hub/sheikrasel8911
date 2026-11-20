# Star Hub BD Shops — Login & Registration Update

এই ZIP-এ মূল ওয়েবসাইটের ফাইল রেখে user account system যোগ করা হয়েছে।

## নতুন ফিচার
- মোবাইল নম্বর অথবা ইমেইল দিয়ে Registration
- Password দিয়ে Login (OTP লাগবে না)
- Secure, hashed password storage (scrypt)
- HttpOnly login session cookie
- Profile page: `/profile`
- Logout
- Home page-এ Login / Register shortcut
- User balance field default ৳0 (payment verification/auto top-up এই আপডেটে অন্তর্ভুক্ত নয়)

## Render-এ Deploy
1. ZIP Extract করুন।
2. Extract করা ফোল্ডারের সব ফাইল GitHub repository-র root-এ আপলোড করে পুরোনো একই নামের ফাইল Replace করুন।
3. Render-এ Manual Deploy → Deploy latest commit দিন।
4. Render Environment-এ আগের GitHub persistence variables ঠিক রাখুন:
   - `FFX-G` = GitHub token (Contents: Read and write)
   - `FFX-REPO` = `helpedsenter-hub/sheikrasel8911`
   - `FFX-BRANCH` = `ffx-data`
   - `AUTH_SECRET` = দীর্ঘ random secret (কমপক্ষে 32 অক্ষর; একবার সেট করে অপরিবর্তিত রাখুন)
5. Deploy শেষ হলে `https://আপনার-সাইট/login` খুলে নতুন অ্যাকাউন্ট খুলে পরীক্ষা করুন।

`FFX-G` এবং `FFX-REPO` ঠিক থাকলে user database GitHub-এর `ffx-data/users.json`-এ সেভ হবে, তাই Render restart/deploy হলেও account থাকবে। GitHub persistence variables না থাকলে ডাটা শুধু local disk-এ থাকবে; Render-এ persistent disk না থাকলে restart/deploy-এ account data হারাতে পারে।

## গুরুত্বপূর্ণ
এই আপডেট Login/Registration/Profile তৈরি করে। এখনো Free Fire order processing, wallet top-up/payment verification বা automatic diamond delivery যুক্ত হয়নি। Payment verify না করে balance বাড়াবেন না।


## Add Money (ম্যানুয়াল বিকাশ/নগদ/রকেট)
- Home-এর Add Money-তে চাপলে লগইন না থাকলে Login/Register হবে; লগইনের পর Add Money পেজে ফিরবে।
- পেমেন্ট নম্বর: 01863445965 (বিকাশ/নগদ/রকেট)।
- ব্যবহারকারী পরিমাণ, প্রেরক নম্বর ও Transaction ID জমা দেবে।
- Admin প্যানেল: `/admin-topups` — আগের `FFX-PASS` পাসওয়ার্ড দিয়ে লগইন করে অনুরোধ Approve/Reject করুন।
- Approve করলেই একবার ব্যালেন্স যোগ হবে; Reject করলে ব্যালেন্স যোগ হবে না।
- `FFX-G`, `FFX-REPO`, `FFX-BRANCH` ঠিকভাবে সেট থাকা জরুরি, কারণ top-up অনুরোধও users.json-এর সঙ্গে সংরক্ষিত হয়।
- এটি ম্যানুয়াল পেমেন্ট যাচাই; কোনো payment gateway বা স্বয়ংক্রিয় পেমেন্ট যাচাই নয়। নম্বরটি সব তিন মাধ্যমে চালু/merchant account কিনা নিজে নিশ্চিত করুন।
