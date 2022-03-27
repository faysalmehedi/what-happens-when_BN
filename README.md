# কি ঘটে যখন... 
এই রিপোজারিটা মূলত বিখ্যাত একটি পুরনো প্রশ্নের উত্তরের খোঁজে, "কি ঘটে যখন আপনি ব্রাউজারে গুগল.কম লিখে ঠাস করে এন্টার চাপ দেন?"। পুরো ব্যাপারটা [এই রিপো](https://github.com/alex/what-happens-when) থেকে অনুবাদ করা, তবে আমি চেষ্টা করেছি একেবারে লাইন বাই লাইন কপি না করে নিজের ভাষায় লিখার জন্য। সুতরাং প্রচুর ভুল ত্রুটি থাকবেই এটা স্বাভাবিক, খুঁজে পেলে PR পাঠান। 

চলুন শুরু করা যাক... 

সূচীপত্র 

- যখন গুগলের 'g' কি প্রেস করা হয় 
- যখন 'enter'-এ ঠাস করে বাড়ি মারেন  
- Interrupt fires [NOT for USB keyboards]
- (On Windows) A WM_KEYDOWN message is sent to the app
- (On OS X) A KeyDown NSEvent is sent to the app 
- (On GNU/Linux) the Xorg server listens for keycodes
- URL থেকে Parse করা 
- এটা কি কোন URL নাকি সার্চ করলেন? 
- non-ASCII Unicode characters থেকে হোস্টনেমে রূপান্তর 
- HSTS list খুঁজে দেখা 
- DNS খোঁজাখুঁজি 
- ARP অনুরোধ ব্যবস্থা 
- একটা socket খুলে ফেলা 
- TLS করমর্দন
- প্যাকেট যদি অকালেই ঝড়ে পড়ে 
- HTTP রীতিনীতি (protocol)  
- HTTP সার্ভারে আবেদন সামলানো 
- ব্রাউজারের বিহাইন্ড দ্যা সিন 
- ব্রাউজার 
- HTML parsing
- CSS interpretation
- Page Rendering
- GPU Rendering
- Window Server
- Post-rendering and user-induced execution
