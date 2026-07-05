# Door Opener App - তৈরির নির্দেশনা

## এই অ্যাপটি কী করে
অ্যাপ ওপেন হলেই স্বয়ংক্রিয়ভাবে এই URL-এ রিকোয়েস্ট পাঠায়:
```
http://192.168.68.106/form/Device?act=9
```
সাথে একটা বড় "OPEN DOOR" বাটনও আছে, চাইলে আবার চাপ দিয়ে দরজা খুলতে পারবেন।

## APK বানানোর ধাপ (Android Studio দিয়ে)

1. **Android Studio ইন্সটল করুন** (যদি না থাকে): https://developer.android.com/studio
2. Android Studio ওপেন করে **Open** করুন এই ফোল্ডারটা (`DoorOpener`)
3. প্রথমবার Gradle sync হতে কিছুক্ষণ সময় লাগবে (ইন্টারনেট লাগবে)
4. উপরের মেনু থেকে **Build > Build Bundle(s) / APK(s) > Build APK(s)** ক্লিক করুন
5. Build শেষ হলে নিচে একটা notification আসবে "locate" লিংক সহ — ওখানে ক্লিক করলে APK ফাইল পাবেন
   (সাধারণত: `app/build/outputs/apk/debug/app-debug.apk`)
6. এই APK ফাইলটা ফোনে কপি করে ইন্সটল করুন (Settings > Security তে "Unknown apps" ইন্সটল অনুমতি দিতে হতে পারে)

## IP/URL পরিবর্তন করতে চাইলে
`app/src/main/java/com/dooropener/app/MainActivity.java` ফাইলে এই লাইনটা খুঁজুন:
```java
private static final String DOOR_URL = "http://192.168.68.106/form/Device?act=9";
```
এখানে শুধু URL বদলে দিলেই হবে।

## গুরুত্বপূর্ণ নোট
- ফোনটা অবশ্যই সেই WiFi নেটওয়ার্কে কানেক্টেড থাকতে হবে যেখানে 192.168.68.106 ডিভাইসটি আছে (এটা একটা লোকাল/প্রাইভেট IP)
- এই কন্টেইনার এনভায়রনমেন্টে Android SDK/Gradle না থাকা এবং ইন্টারনেট বন্ধ থাকায় আমি নিজে সরাসরি .apk ফাইল কম্পাইল করে দিতে পারিনি — এই সোর্স কোড থেকে আপনাকে Android Studio দিয়ে বিল্ড করে নিতে হবে।
- বিকল্প হিসেবে, আপনি চাইলে অনলাইন কোনো APK বিল্ড সার্ভিস (যেমন GitHub Actions দিয়ে নিজের রিপোতে বিল্ড) ব্যবহার করেও এই একই সোর্স কোড দিয়ে APK বানাতে পারেন।
