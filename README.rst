কি ঘটে যখন...
====================

এই রিপোজারিটা মূলত বিখ্যাত একটি পুরনো প্রশ্নের উত্তরের খোঁজে, "কি ঘটে যখন আপনি ব্রাউজারে গুগল.কম লিখে ঠাস করে এন্টার চাপ দেন?"। পুরো ব্যাপারটা `এই রিপো`_ থেকে অনুবাদ করা, তবে আমি চেষ্টা করেছি একেবারে লাইন বাই লাইন কপি না করে নিজের ভাষায় লিখার জন্য। সুতরাং প্রচুর ভুল ত্রুটি থাকবেই এটা স্বাভাবিক, খুঁজে পেলে PR পাঠান।

চলুন শুরু করা যাক...

Table of Contents
====================

.. contents::
   :backlinks: none
   :local:

যখন গুগলের 'g' কি প্রেস করা হয়
-------------------------
যখনই কেউ ব্রাউজারে গুগল ডট কম লেখার জন্য কি বোর্ডে 'g' প্রেস করে তখন ব্রাউজার এটিকে একটি ইভেন্ট হিসেবে গ্রহণ করে এবং সাধারণত অটো-কম্পিলিশন ফাংশন ট্রিগার করে। যদি আপনি প্রাইভেট/ইনকগনিটো মুডে থাকেন বা খুব বেশি সাজেশন যদি URL বার এর ড্রপডাউনে নাও দেখাতে পারে এই ব্যাপারটা ব্রাউজারের এলগোরিদমের উপর নির্ভর করে । সাধারণত এইগুলো ব্রাউজারের নিজস্ব এলগোরিদম বিভিন্ন ডাটা থেকে সর্ট এবং প্রায়োরিটিজ অনুযায়ী করে থাকে। এই ডাটা নেওয়া হয় ইউজারের সার্চ করা, বুকমার্কস, কুকিজ এবং ইন্টারনেটে পপুলার সার্চের উপর ভিত্তি করে। যখনই আপনি টাইপ করছেন 'google.com' তখন অনেকগুলো কোড ব্লক রান হয় এবং ক্রমাগত সাজেশন দেখাতে শুরু করে প্রতিটি কি-প্রেসে। এমনকি এটি আপনাকে 'google.com' সাজেস্ট করবে আপনি পুরোটা লেখার পুর্বেই, তখন আপনাকে খালি এন্টার-কি তে জোরে বাড়ি মারতে হবে।


যখন 'enter'-এ ঠাস করে বাড়ি মারেন
-----------------------------

একেবারে শূন্য থেকে বুঝার সুবিধার্থে চলুন ধরি আমরা জোরেশোরে কি-বোর্ডের "Enter" কি টাকে হিট করলাম, এরপর কি ঘটবে? এই সময় একটা ইলেকট্রিক্যাল সার্কিট যেটা "Enter" কি এর সাথে যুক্ত ছিল সেটা ক্লোজ হয়(সরাসরি বা ক্যাপাসিটিভলি)। এটা খুব সামান্য কিছু কারেন্টকে কি-বোর্ডের লজিক সার্কেটে পাস করে, যে লজিক সার্কিট সাধারণত প্রতিটা কি-সুইচের অবস্থা স্ক্যান করে সেই সার্কিট ইলেক্ট্রিক্যাল কারেন্টকে নোটিশ করে এবং সেটাকে একটা কি-বোর্ড ইন্টিজারে রূপান্তর করে, এই ক্ষেত্রে যেটা ১৩। এরপর কি-বোর্ড কন্টোলার সেই কি-কোডকে encode করে কম্পিউটারে ট্রান্সপোর্ট করে। যেটা এখন বর্তমানে ইউনিভার্সিলি একটা ব্লু-টুথ কানেকশন বা Universal Serial Bus (USB) এর মধ্যে দিয়ে যায়। আগে অবশ্য অন্য ব্যবস্থা ছিল, যাকে বলা হত, PS/2 or ADB কানেকশন।

*USB কিবোর্ডের ক্ষেত্রে যা ঘটেঃ*

- কি-বোর্ডের USB সার্কিটটা সাধারণত 5V পাওয়ার সাপ্লাই করে কম্পিউটারের USB হোস্ট কন্ট্রোলারের পিন ১ এর মধ্যে দিয়ে।
- যে কি-কোডটা জেনারেট হয় সেটা স্টোর করা থাকে ইন্টারনাল কিবোর্ডের নিজস্ব মেমোরিতে যাকে বলা হয় "endpoint".
- হোস্ট USB কন্ট্রোলার সেই "endpoint" কে প্রতি ~10ms এ পুল করে(মিনিমাম ভ্যালু ডিক্লেয়ার করে কি-বোর্ড), যাতে কি-কোড ভ্যালুটা এর মধ্যে স্টোর করা থাকে।
- এই কি-কোড ভ্যালুটা এরপর যায় USB SIE (Serial Interface Engine) -এ এক বা এর অধিক USB প্যাকেটে কনভার্ট হয়ে যেটা সাধারণত লো-লেভেল USB প্রোটোকল ব্যবহার করে।
- সেই প্যাকেটগুলো পাঠানো হয় একটা অন্যরকম ইলেকট্রিক্যাল সিগনাল দ্বারা D+ and D- pins (the middle 2) ম্যাক্সিমাম 1.5 Mb/s স্পিড ব্যবহার করে, যেহেতু HID (Human Interface Device) সবসময় ভাবা হয় "লো-স্পিড ডিভাইস"(USB 2.0 compliance) হিসেবে।
- এই সিরিয়াল সিগনাল এরপর ডিকোড হয় কম্পিউটারের হোস্ট USB কন্ট্রোলারে, এবং ইন্টেরপ্রিটেড হয় কম্পিউটারের Human Interface Device (HID) ইউনিভার্সাল ক-বোর্ড ডিভাইস ড্রাইভার দ্বারা। কি এর ভ্যালু এরপর পাস হয় অপারেটিং সিস্টেমের হার্ডওয়্যারের এবস্ট্রাকশন লেয়ারে।

*ভার্চুয়াল কি-বোর্ডের ক্ষেত্রে(টাচ-স্ক্রীন ডিভাইস):*

- যখন ইউজার আধুনিক ক্যাপাসিটিভ টাচ-স্ক্রীনে আংগুল দিয়ে প্রেস করে, তখন খুবই অল্প পরিমাণ কারেন্ট আঙ্গুলে ট্রান্সফার হয়। এটি সার্কিট পরিপূর্ন করে ইলেক্ট্রোস্ট্যাটিক ফিল্ডে এর কনডাকটিভ লেয়ার এর মাধ্যেমে এবং স্ক্রিনের সেই পয়েন্টে ভোল্টেজ ড্রপ তৈরি করে। স্ক্রীণ কন্ট্রোলার তখন একটা ইন্টারাপশন রিপোর্ট করে কি-প্রেসের অবস্থান নিয়ে।
- তারপর মোবাইল অপারেটিং সিস্টেম নোটিশ করে যে GUI elements(ভার্চুয়াল কি-বোর্ড) এর এপ্লিকেশনে একটা প্রেস ইভেন্ট ট্রিগার হয়েছে।
- ভার্চুয়াল কি-বোর্ড এখন সেই 'key pressed' সফটওয়্যার interrupt মেসেজ হিসেবে অপারেটিং সিস্টেমের নিকট পাঠায়।
- সেই interrupt তখন সেই এপ্লিকেশনকে এই 'key pressed' ইভেন্টের ব্যাপারে নোটিফাই করে।

URL থেকে Parse করা
-----------------

* ব্রাউজারের কাছে এখন নিচের এই ইনফরমেশন গুলো রয়েছে যেগুলো URL (Uniform Resource Locator) এর মধ্যে ছিলঃ

    - ``প্রটোকল`` "http"
        ব্যবহার করে 'Hyper Text Transfer Protocol'
    - ``রিসোর্স`` "/"
        মূল পেইজ (index) থেকে সংগ্রহ করা

এটা কি কোন URL নাকি সার্চ করলেন?
---------------------------

যখন কোন প্রোটোকল বা ভ্যালিড ডোমেইন নাম ব্রাউজারকে দেওয়া হয় না, তখন ব্রাউজার সেই এড্রেস বক্সে দেওয়া টেক্সটকে ব্রাউজারের ডিফল্ট ওয়েব সার্চ ইঞ্জিনে সার্চ করে। অনেক সময় দেখা যায়, URL এ কোন স্পেশাল টেক্সটের অংশ যুক্ত হয়েছে যেটায় সার্চ ইঞ্জিনকে বলা হয় যে এটি স্পেসিফিক ব্রাউজারের ইউজার বার থেকে যাচ্ছে/আসছে।

non-ASCII Unicode characters কে হোস্টনেমে রূপান্তর করা
-----------------------------------------------

* ব্রাউজার হোস্টনেম চেক করে এই অক্ষরগুলোর জন্য যেগুলো ( ``a-z``, ``A-Z``, ``0-9``, ``-``, or ``..`` ) এর মধ্যে নেই।
* যেহেতু আমরা ধরে নিয়েছি আমাদের হোস্টনেম "google.com" সেহেতু এইখানে এমন কিছু নেই, কিন্তু যদি থাকতো তবে ব্রাউজার হোস্টনেম অংশে `Punycode`_ encoding ব্যবহার করতো।


HSTS লিস্ট চেক করা
---------------
* একটা রিকোয়েস্ট করার সময় ব্রাউজার তার নিজস্ব "preloaded HSTS (HTTP Strict Transport Security)" লিস্ট চেক করে। এটি হচ্ছে ওয়েবসাইটের একটি লিস্ট যেগুলো শুধুমাত্র HTTPS দ্বারা যোগাযোগ করার জন্য বলা হয়। 

* যদি ওয়েবসাইটটি এই লিস্টে থেকে থাকে, তাহলে ব্রাউজার HTTP এর বদলে শুধুমাত্র HTTPS দ্বারা রিকোয়েস্ট পাঠায়। আর যদি লিস্টে না থাকে তাহলে ইনিশিয়াল রিকোয়েস্টটা HTTP দ্বারা পাঠানো হয়। নোটঃ একটি ওয়েবসাইট HSTS পলিসি HSTS লিস্টে না থাকলেও ব্যবহার করতে পারে। এই ক্ষেত্রে ইউজার প্রথম রিকোয়েস্টটা HTTP দ্বারা পাঠালে সেটা একটা রেসপন্স করে যে শুধুমাত্র HTTPS রিকোয়েস্ট পাঠানোর জন্য। এইখানে একটা আশঙ্কা এই যে, এই প্রথম HTTP রিকোয়েস্টও কিন্তু ইউজারকে "downgrade attack" এর সম্মুখীন করতে পারে। এই জন্য বর্তমানে সকল মর্ডাণ ওয়েব ব্রাউজারেই HSTS লিস্ট অবশ্যই সংযুক্ত থাকে।  


DNS খোঁজাখুঁজি
-----------

* ব্রাউজার চেক করে যদি রিকোয়েস্ট করা ডোমেইনটা cache-এ আছে কিনা? (ক্রোম ব্রাউজারে DNS cache দেখার জন্য এই খানে যান `chrome://net-internals/#dns <chrome://net-internals/#dns>`_) 

* যদি পাওয়া না যায়, তখন ব্রাউজার ``gethostbyname`` নামে একটা লাইব্রেরী ফাংশনকে কল করে DNS খোঁজার(lookup) জন্য। নোটঃ `ফাংশনটা OS অনুযায়ী আলাদাও হতে পারে`_। 

*  ``gethostbyname`` ফাংশন চেক করে যদি হোস্টনেমটা লোকাল ``hosts`` ফাইলে থেকে নেওয়া বা রিসলভ করা যায় কিনা। 
* যদি ``gethostbyname`` ফাংশন এটাকে cache বা লোকাল ``hosts`` ফাইলে না খুঁজে পায় তখন সে নেটওয়ার্ক স্ট্যাকে থাকা DNS সার্ভারে একটা রিকোয়েস্ট পাঠায়। এটা সাধারণত লোকাল রাউটার বা আইএসপির caching DNS server হয়ে থাকে। 
* DNS সার্ভার যদি একই সাবনেটে থেকে থাকে তাহলে নেটওয়ার্ক লাইব্রেরী নিচের ``ARP process`` ফলো করে DNS সার্ভারের সাথে। 
* DNS সার্ভার যদি একই সাবনেটে না থাকে, অন্য একটা সাবনেটে থাকে তাহলে নেটওয়ার্ক লাইব্রেরী নিচের ``ARP process`` ফলো করে ডিফল্ট গেটওয়ে আইপির সাথে।   


ARP process
-----------

ARP (Address Resolution Protocol)  ব্রডকাস্ট মেসেজ পাঠানোর জন্য নেটওয়ার্ক লাইব্রেরীর আইপি এড্রেস লাগে লুকআপের জন্য। এছাড়া যে ইন্টারফেসের মাধ্যেমে ARP পাঠানো হবে সেই ইন্টারফেসের ম্যাক এড্রেসেরও (MAC-Media Acess Control) প্রয়োজন হয়।  

ARP cache তে প্রথমে খোঁজা হয় ARP এন্ট্রি আছে কিনা টার্গেটেড আইপির। যদি cache এ পাওয়া যায়, তাহলে লাইব্রেরী ফাংশন একটা রেজাল্ট ফেরত পাঠায় Target IP = MAC. 

আর যদি ARP cache এ পাওয়া না যায়ঃ 

* রাউট টেবিলে খোঁজ করে দেখা হয় যদি সেই টার্গেটেড আইপি এড্রেস লোকাল রাউট টেবিলের অন্য কোন সাবনেটের সাথে মিলে কিনা। যদি মিলে যায়, লাইব্রেরী সেই সাবনেটের সাথে যুক্ত ইন্টারফেস ব্যবহার করে। আর যদি না মিলে, লাইব্রেরী ডিফল্ট গেটওয়ের ইন্টারফেস করে। 
* এরপর যে ইন্টারফেস সিলেক্ট করা হয়েছে সেই ইন্টারফেসের MAC এড্রেস খোঁজা হয়। 
* তারপর নেটওয়ার্ক লাইব্রেরী একটি  Layer 2 (data link layer of the `OSI model`_) ARP request সেন্ড করে।

``ARP Request``::

    Sender MAC: interface:mac:address:here
    Sender IP: interface.ip.goes.here
    Target MAC: FF:FF:FF:FF:FF:FF (Broadcast)
    Target IP: target.ip.goes.here

কি রকম হার্ডওয়্যার কম্পিউটার ও রাউটারের মাঝে রয়েছে তার উপর নির্ভর করেঃ 

সরাসরি যুক্তঃ  
* কম্পিউটার যদি সরাসরি রাউটারের সাথে যুক্ত থাকে তাহলে রাউটার রেসপন্স করে একটি ARP রিপ্লাই পাঠাবে(নিচে দেখুন)।  

হাবের(Hub) মাধ্যেমে যুক্তঃ 
* যদি কম্পিউটার কোন হাবের সাথে যুক্ত থাকে তবে হাব ARP request ব্রডকাস্ট করবে অন্য সব পোর্টে(port) -এ। যদি রাউটার সেই একই তারে(wire) যুক্ত থাকে, তাহলে সেটি রেসপন্স করে একটি ``ARP Reply`` পাঠাবে(নিচে দেখুন)।  

সুইচের(switch) মাধ্যেমে যুক্তঃ 
* যদি কম্পিউটার কোন সুইচের মাধ্যমে যুক্ত থাকে, তাহলে সুইচ তার নিজস্ব CAM/MAC table খুঁজে দেখবে কোন পোর্টে সেই ম্যাক এড্রেস রয়েছে যেটা আমরা খুঁজছি। যদি সুইচে সেই ম্যাক এড্রেসের খোজ না পাওয়া যায় তবে এটি পুনরায় একটা ARP রিকোয়েস্ট পাঠাবে অন্য সকল পোর্টে। 
* যদি সুইচের MAC/CAM table এ পাওয়া যায়, তবে সেই পোর্টকে চিহ্নিত করে সে ARP রিকোয়েস্ট পাঠাবে। 
* যদি রাউটার সেই একই তারে(wire) যুক্ত থাকে, তাহলে সেটি রেসপন্স করে একটি ``ARP Reply`` পাঠাবে(নিচে দেখুন)।

``ARP Reply``::

    Sender MAC: target:mac:address:here
    Sender IP: target.ip.goes.here
    Target MAC: interface:mac:address:here
    Target IP: interface.ip.goes.here

এখন যেহেতু নেটওয়ার্ক লাইব্রেরীর কাছে DNS সার্ভার কিংবা ডিফল্ট গেটওয়ের আইপি এড্রেস রয়েছে, সে এখন DNS প্রসেস শুরু করতে পারেঃ 

* DNS ক্লায়েন্ট একটি সকেট এস্টাবলিশ করে DNS সার্ভারের UDP পোর্ট 53 তে, সোর্স পোর্ট 1023 ব্যবহার করে। 
* যদি রেসপন্সের সাইজটা বড় হয়ে যায় সেক্ষেত্রে TCP প্রটোকল ব্যবহার হয় UDP এর পরিবর্তে। 
* যদি লোকাল/আইএসপি DNS সার্ভারের কাছে ইনফরমেশন না পায়, তাহলে একটি রিকার্সিভ সার্চ রিকোয়েস্ট করা হয় এবং সেটি লিস্টে থাকা অন্য সকল DNS সার্ভারে পৌঁছায় যতক্ষণ না  SOA(start of authority) record না পাওয়া যায়, এবং যখন পাওয়া যায় তখন উত্তর রিটার্ন করে।

Opening of a socket
-------------------

যখন ব্রাউজার ডেসটিনেশন সার্ভারের আইপি এড্রেস পেয়ে যায়, ব্রাউজার সেই আইপি ও URL এর সাথে থাকা পোর্ট নাম্বার  (the HTTP protocol defaults to port 80, and HTTPS to port 443) নেয় এবং ``socket`` নামে একটি সিস্টেম লাইব্রেরী ফাংশন কল করে এবং রিকোয়েস্ট পাঠায় TCP socket stream - ``AF_INET/AF_INET6`` and ``SOCK_STREAM`` -এ। 

* রিকোয়েস্টটি প্রথমে ট্রান্সপোর্ট লেয়ারে যায় যেখানে একটি TCP সেগমেন্ট তৈরি হয়। ডেস্টিনেশন পোর্ট হেডারের সাথে যুক্ত করা হয় এবং একটি সোর্স পোর্ট নেওয়া হয় কার্নেলের ডায়নামিক পোর্ট রেঞ্জ থেকে  (ip_local_port_range in Linux). 
* সেগমেন্টটি এরপর নেটওয়ার্ক লেয়ারে পাঠানো হয়, সেখানে গিয়ে আইপি হেডার যুক্ত হয়। সেই আইপি হেডারে ডেস্টিনেশন সার্ভারের আইপি এবং সোর্স আইপি হিসেবে ডিভাইসের আইপি যুক্ত করা হয় এবং প্যাকেট তৈরি হয়। 
* এরপর প্যাকেটটি লিংক লেয়ারে পৌঁছায়। এইবার একটি ফ্রেম হেডার যেখানে ডিভাইসের NIC কার্ডের MAC এড্রেস যুক্ত করা হয় সেই সাথে লোকাল রাউটারের বা গেটওয়ের MAC যুক্ত করা হয়। পূর্বের মত, যদি কার্নেল যদি গেটওয়ের MAC এড্রেস না থাকে তাহলে ARP কুয়েরি করতে ব্রডকাস্ট করার মাধ্যেমে। 

এই পয়েন্টে প্যাকেট প্রস্তুত নিচের যেকোন মাধ্যেমে ট্রান্সমিট হওয়ার জন্যঃ 
* `Ethernet`_
* `WiFi`_
* `Cellular data network`_

বেশিরভাগ বাড়ী বা ছোট ব্যবসা প্রতিষ্ঠানের ইন্টারনেট কানেকশনের ক্ষেত্রে, প্যাকেটটি নিজস্ব কম্পিউটার, এরপর খুব সম্ভবত লোকাল নেটওয়ার্ক এবং এরপর মডেম (MOdulator/DEModulator) এর মধ্যে দিয়ে যেটি মূলত ডিজিটাল  1's and 0's কে রূপান্তর করে এনালগ সিগনালে যাতে করে টেলিফোন, ক্যাবল, বা ওয়্যারলেস কানেকশনের মধ্যে দিয়ে যেতে পারে। অন্যদিকে অন্য প্রান্তে থাকা মডেম ও একইভাবে এনালগ সিগনালটিকে পুনরায় ডিজিটাল ডাটায় রূপান্তর করে পরবর্তী নেটওয়ার্কে নোডে(`network node`_) যেখানে প্যাকেটে থাকা "From" এবং "to" এড্রেসগুলো এনাইসিস করা হয়। 

বেশিরভাগ বড় ব্যবসা প্রতিষ্ঠান এবং অনেক বাসাবাড়িতেও এখন ফাইবার অপটিক বা সরাসরি ইথারনেট কানেকশন রয়েছে, সেসব ক্ষেত্রে ডাটা রূপান্তর করতে হয় না, ডিজিটাল ডাটাই সরাসরি পরবর্তী নেটওয়ার্কের নোডের কাছে পাঠিয়ে দেওয়া হয় প্রসেসিং করার জন্য।   

অবশেষে প্যাকেটটি রাউটারে পৌঁছায় যেটা লোকাল সাবনেটকে ম্যানেজ করে। সেখান থেকে এটা তার ট্রাভেলিং অব্যাহত রাখে autonomous system's (AS) border রাউটারে, অন্যান্য AS(autonomous system) এ, এবং সর্বশেষে ডেস্টিনেশন সার্ভারে। এই ট্রাভেলিংয়ের সময় প্রতিটা রাউটার আইপি হেডার থেকে ডেস্টিনেশন এড্রেস দেখে এবং  যথাযথ পরবর্তী গন্তব্য(Next hop) এর কাছে পাঠায়। আইপি হেডারে থাকা time to live (TTL) ফিল্ড প্রতিবার রাউটার অতিক্রম করার সময়ে এর মান "এক" করে কমিয়ে নেয়। যদি TTL ফিল্ডটি শূন্য হয়ে যায় অথবা রাউটারের queue তে যদি কোন জায়গা খালি না (এমন হতে পারে network congestion এর জন্য) তাহলে প্যাকেটটি ড্রপড হয়ে যাবে। 

এই "send and receive" প্রসেস কয়েকবার ঘটে নিচের দেওয়া TCP কানেকশন ফ্লো অনুযায়ীঃ 

* ক্লায়েন্ট একটি initial sequence number (ISN) নাম্বার নেয় এবং প্যাকেটটিকে সার্ভারে পাঠায় SYN bit সেট করে বুঝানোর জন্য। 

* সার্ভার সেই SYN bit রিসিভ করে এবং যদি সে এই রিকোয়েস্টে সম্মত হতে চায়ঃ 
   * সার্ভার তার নিজের ISN বাছাই করে 
   * সার্ভার SYN সেট করে এটা বুঝানোর জন্য সে নিজের ISN বাছাই করেছে। 
   * সার্ভার (ক্লায়েন্ট SYN + 1) কপি করে ACK ফিল্ডে এবং ACK ফ্ল্যাগ যোগ করে এটা নির্দেশ করে এটা হচ্ছে একটা  acknowledging receipt প্রথম প্যাকেটটার জন্য। 

* ক্লায়েন্ট একনলেজ করে কানেকশনের ব্যাপারে আরও একটি প্যাকেট পাঠানোর মাধ্যেমেঃ 
   * নিজের sequence নাম্বার বাড়িয়ে দেয় 
   * রিসিভারের acknowledgment নাম্বারও বাড়িয়ে দেয়  
   * ACK ফিল্ডকে সেট করে দেয় 
* ডাটা ট্রান্সফার হয় যেভাবেঃ 
   * যেহেতু একটা সাইড N বাইট ডাটা পাঠায়, এটা তার SEQ বা sequence নাম্বারও সেই বাইট অনুযায়ী বাড়িয়ে দেয়। 
   * যখন অপর সাইড প্যাকেট প্রাপ্তির ব্যাপার acknowledge করে, তখন সেটি একটা ACK প্যাকেট পাঠায় ACK ভ্যালু সেট করে যেটি সর্বশেষ পাওয়া অন্য সাইডের sequence নাম্বারের সমান 

* কানেকশন ক্লোজ করার জন্যঃ 
   * "closer" একটি FIN প্যাকেট পাঠায় 
   * অন্য সাইড FIN প্যাকেটটি  acknowledge করে, এবং নিজের FIN পাঠায় 
   * "closer" সেই FIN প্যাকেটটি acknowledge করে একটি ACK দ্বারা    

TLS handshake
-------------
* The client computer sends a ``ClientHello`` message to the server with its
  Transport Layer Security (TLS) version, list of cipher algorithms and
  compression methods available.

* The server replies with a ``ServerHello`` message to the client with the
  TLS version, selected cipher, selected compression methods and the server's
  public certificate signed by a CA (Certificate Authority). The certificate
  contains a public key that will be used by the client to encrypt the rest of
  the handshake until a symmetric key can be agreed upon.

* The client verifies the server digital certificate against its list of
  trusted CAs. If trust can be established based on the CA, the client
  generates a string of pseudo-random bytes and encrypts this with the server's
  public key. These random bytes can be used to determine the symmetric key.

* The server decrypts the random bytes using its private key and uses these
  bytes to generate its own copy of the symmetric master key.

* The client sends a ``Finished`` message to the server, encrypting a hash of
  the transmission up to this point with the symmetric key.

* The server generates its own hash, and then decrypts the client-sent hash
  to verify that it matches. If it does, it sends its own ``Finished`` message
  to the client, also encrypted with the symmetric key.

* From now on the TLS session transmits the application (HTTP) data encrypted
  with the agreed symmetric key.

If a packet is dropped
----------------------

Sometimes, due to network congestion or flaky hardware connections, TLS packets
will be dropped before they get to their final destination. The sender then has
to decide how to react. The algorithm for this is called `TCP congestion
control`_. This varies depending on the sender; the most common algorithms are
`cubic`_ on newer operating systems and `New Reno`_ on almost all others.

* Client chooses a `congestion window`_ based on the `maximum segment size`_
  (MSS) of the connection.
* For each packet acknowledged, the window doubles in size until it reaches the
  'slow-start threshold'. In some implementations, this threshold is adaptive.
* After reaching the slow-start threshold, the window increases additively for
  each packet acknowledged. If a packet is dropped, the window reduces
  exponentially until another packet is acknowledged.

HTTP protocol
-------------

If the web browser used was written by Google, instead of sending an HTTP
request to retrieve the page, it will send a request to try and negotiate with
the server an "upgrade" from HTTP to the SPDY protocol.

If the client is using the HTTP protocol and does not support SPDY, it sends a
request to the server of the form::

    GET / HTTP/1.1
    Host: google.com
    Connection: close
    [other headers]

where ``[other headers]`` refers to a series of colon-separated key-value pairs
formatted as per the HTTP specification and separated by single newlines.
(This assumes the web browser being used doesn't have any bugs violating the
HTTP spec. This also assumes that the web browser is using ``HTTP/1.1``,
otherwise it may not include the ``Host`` header in the request and the version
specified in the ``GET`` request will either be ``HTTP/1.0`` or ``HTTP/0.9``.)

HTTP/1.1 defines the "close" connection option for the sender to signal that
the connection will be closed after completion of the response. For example,

    Connection: close

HTTP/1.1 applications that do not support persistent connections MUST include
the "close" connection option in every message.

After sending the request and headers, the web browser sends a single blank
newline to the server indicating that the content of the request is done.

The server responds with a response code denoting the status of the request and
responds with a response of the form::

    200 OK
    [response headers]

Followed by a single newline, and then sends a payload of the HTML content of
``www.google.com``. The server may then either close the connection, or if
headers sent by the client requested it, keep the connection open to be reused
for further requests.

If the HTTP headers sent by the web browser included sufficient information for
the webserver to determine if the version of the file cached by the web
browser has been unmodified since the last retrieval (ie. if the web browser
included an ``ETag`` header), it may instead respond with a request of
the form::

    304 Not Modified
    [response headers]

and no payload, and the web browser instead retrieve the HTML from its cache.

After parsing the HTML, the web browser (and server) repeats this process
for every resource (image, CSS, favicon.ico, etc) referenced by the HTML page,
except instead of ``GET / HTTP/1.1`` the request will be
``GET /$(URL relative to www.google.com) HTTP/1.1``.

If the HTML referenced a resource on a different domain than
``www.google.com``, the web browser goes back to the steps involved in
resolving the other domain, and follows all steps up to this point for that
domain. The ``Host`` header in the request will be set to the appropriate
server name instead of ``google.com``.

HTTP Server Request Handle
--------------------------
The HTTPD (HTTP Daemon) server is the one handling the requests/responses on
the server-side. The most common HTTPD servers are Apache or nginx for Linux
and IIS for Windows.

* The HTTPD (HTTP Daemon) receives the request.
* The server breaks down the request to the following parameters:
   * HTTP Request Method (either ``GET``, ``HEAD``, ``POST``, ``PUT``,
     ``PATCH``, ``DELETE``, ``CONNECT``, ``OPTIONS``, or ``TRACE``). In the
     case of a URL entered directly into the address bar, this will be ``GET``.
   * Domain, in this case - google.com.
   * Requested path/page, in this case - / (as no specific path/page was
     requested, / is the default path).
* The server verifies that there is a Virtual Host configured on the server
  that corresponds with google.com.
* The server verifies that google.com can accept GET requests.
* The server verifies that the client is allowed to use this method
  (by IP, authentication, etc.).
* If the server has a rewrite module installed (like mod_rewrite for Apache or
  URL Rewrite for IIS), it tries to match the request against one of the
  configured rules. If a matching rule is found, the server uses that rule to
  rewrite the request.
* The server goes to pull the content that corresponds with the request,
  in our case it will fall back to the index file, as "/" is the main file
  (some cases can override this, but this is the most common method).
* The server parses the file according to the handler. If Google
  is running on PHP, the server uses PHP to interpret the index file, and
  streams the output to the client.

Behind the scenes of the Browser
----------------------------------

Once the server supplies the resources (HTML, CSS, JS, images, etc.)
to the browser it undergoes the below process:

* Parsing - HTML, CSS, JS
* Rendering - Construct DOM Tree → Render Tree → Layout of Render Tree →
  Painting the render tree

Browser
-------

The browser's functionality is to present the web resource you choose, by
requesting it from the server and displaying it in the browser window.
The resource is usually an HTML document, but may also be a PDF,
image, or some other type of content. The location of the resource is
specified by the user using a URI (Uniform Resource Identifier).

The way the browser interprets and displays HTML files is specified
in the HTML and CSS specifications. These specifications are maintained
by the W3C (World Wide Web Consortium) organization, which is the
standards organization for the web.

Browser user interfaces have a lot in common with each other. Among the
common user interface elements are:

* An address bar for inserting a URI
* Back and forward buttons
* Bookmarking options
* Refresh and stop buttons for refreshing or stopping the loading of
  current documents
* Home button that takes you to your home page

**Browser High-Level Structure**

The components of the browsers are:

* **User interface:** The user interface includes the address bar,
  back/forward button, bookmarking menu, etc. Every part of the browser
  display except the window where you see the requested page.
* **Browser engine:** The browser engine marshals actions between the UI
  and the rendering engine.
* **Rendering engine:** The rendering engine is responsible for displaying
  requested content. For example if the requested content is HTML, the
  rendering engine parses HTML and CSS, and displays the parsed content on
  the screen.
* **Networking:** The networking handles network calls such as HTTP requests,
  using different implementations for different platforms behind a
  platform-independent interface.
* **UI backend:** The UI backend is used for drawing basic widgets like combo
  boxes and windows. This backend exposes a generic interface that is not
  platform-specific.
  Underneath it uses operating system user interface methods.
* **JavaScript engine:** The JavaScript engine is used to parse and
  execute JavaScript code.
* **Data storage:** The data storage is a persistence layer. The browser may
  need to save all sorts of data locally, such as cookies. Browsers also
  support storage mechanisms such as localStorage, IndexedDB, WebSQL and
  FileSystem.

HTML parsing
------------

The rendering engine starts getting the contents of the requested
document from the networking layer. This will usually be done in 8kB chunks.

The primary job of the HTML parser is to parse the HTML markup into a parse tree.

The output tree (the "parse tree") is a tree of DOM element and attribute
nodes. DOM is short for Document Object Model. It is the object presentation
of the HTML document and the interface of HTML elements to the outside world
like JavaScript. The root of the tree is the "Document" object. Prior to
any manipulation via scripting, the DOM has an almost one-to-one relation to
the markup.

**The parsing algorithm**

HTML cannot be parsed using the regular top-down or bottom-up parsers.

The reasons are:

* The forgiving nature of the language.
* The fact that browsers have traditional error tolerance to support well
  known cases of invalid HTML.
* The parsing process is reentrant. For other languages, the source doesn't
  change during parsing, but in HTML, dynamic code (such as script elements
  containing `document.write()` calls) can add extra tokens, so the parsing
  process actually modifies the input.

Unable to use the regular parsing techniques, the browser utilizes a custom
parser for parsing HTML. The parsing algorithm is described in
detail by the HTML5 specification.

The algorithm consists of two stages: tokenization and tree construction.

**Actions when the parsing is finished**

The browser begins fetching external resources linked to the page (CSS, images,
JavaScript files, etc.).

At this stage the browser marks the document as interactive and starts
parsing scripts that are in "deferred" mode: those that should be
executed after the document is parsed. The document state is
set to "complete" and a "load" event is fired.

Note there is never an "Invalid Syntax" error on an HTML page. Browsers fix
any invalid content and go on.

CSS interpretation
------------------

* Parse CSS files, ``<style>`` tag contents, and ``style`` attribute
  values using `"CSS lexical and syntax grammar"`_
* Each CSS file is parsed into a ``StyleSheet object``, where each object
  contains CSS rules with selectors and objects corresponding CSS grammar.
* A CSS parser can be top-down or bottom-up when a specific parser generator
  is used.

Page Rendering
--------------

* Create a 'Frame Tree' or 'Render Tree' by traversing the DOM nodes, and
  calculating the CSS style values for each node.
* Calculate the preferred width of each node in the 'Frame Tree' bottom-up
  by summing the preferred width of the child nodes and the node's
  horizontal margins, borders, and padding.
* Calculate the actual width of each node top-down by allocating each node's
  available width to its children.
* Calculate the height of each node bottom-up by applying text wrapping and
  summing the child node heights and the node's margins, borders, and padding.
* Calculate the coordinates of each node using the information calculated
  above.
* More complicated steps are taken when elements are ``floated``,
  positioned ``absolutely`` or ``relatively``, or other complex features
  are used. See
  http://dev.w3.org/csswg/css2/ and http://www.w3.org/Style/CSS/current-work
  for more details.
* Create layers to describe which parts of the page can be animated as a group
  without being re-rasterized. Each frame/render object is assigned to a layer.
* Textures are allocated for each layer of the page.
* The frame/render objects for each layer are traversed and drawing commands
  are executed for their respective layer. This may be rasterized by the CPU
  or drawn on the GPU directly using D2D/SkiaGL.
* All of the above steps may reuse calculated values from the last time the
  webpage was rendered, so that incremental changes require less work.
* The page layers are sent to the compositing process where they are combined
  with layers for other visible content like the browser chrome, iframes
  and addon panels.
* Final layer positions are computed and the composite commands are issued
  via Direct3D/OpenGL. The GPU command buffer(s) are flushed to the GPU for
  asynchronous rendering and the frame is sent to the window server.

GPU Rendering
-------------

* During the rendering process the graphical computing layers can use general
  purpose ``CPU`` or the graphical processor ``GPU`` as well.

* When using ``GPU`` for graphical rendering computations the graphical
  software layers split the task into multiple pieces, so it can take advantage
  of ``GPU`` massive parallelism for float point calculations required for
  the rendering process.


Window Server
-------------

Post-rendering and user-induced execution
-----------------------------------------

After rendering has been completed, the browser executes JavaScript code as a result
of some timing mechanism (such as a Google Doodle animation) or user
interaction (typing a query into the search box and receiving suggestions).
Plugins such as Flash or Java may execute as well, although not at this time on
the Google homepage. Scripts can cause additional network requests to be
performed, as well as modify the page or its layout, causing another round of
page rendering and painting.

.. _`Creative Commons Zero`: https://creativecommons.org/publicdomain/zero/1.0/
.. _`"CSS lexical and syntax grammar"`: http://www.w3.org/TR/CSS2/grammar.html
.. _`analog-to-digital converter`: https://en.wikipedia.org/wiki/Analog-to-digital_converter
.. _`network node`: https://en.wikipedia.org/wiki/Computer_network#Network_nodes
.. _`TCP congestion control`: https://en.wikipedia.org/wiki/TCP_congestion_control
.. _`cubic`: https://en.wikipedia.org/wiki/CUBIC_TCP
.. _`New Reno`: https://en.wikipedia.org/wiki/TCP_congestion_control#TCP_New_Reno
.. _`congestion window`: https://en.wikipedia.org/wiki/TCP_congestion_control#Congestion_window
.. _`maximum segment size`: https://en.wikipedia.org/wiki/Maximum_segment_size
.. _`varies by OS` : https://en.wikipedia.org/wiki/Hosts_%28file%29#Location_in_the_file_system
.. _`简体中文`: https://github.com/skyline75489/what-happens-when-zh_CN
.. _`한국어`: https://github.com/SantonyChoi/what-happens-when-KR
.. _`日本語`: https://github.com/tettttsuo/what-happens-when-JA
.. _`downgrade attack`: http://en.wikipedia.org/wiki/SSL_stripping

.. _`Spanish`: https://github.com/gonzaleztroyano/what-happens-when-ES

.. _`এই রিপো`: https://github.com/alex/what-happens-when
.. _`Punycode`: https://en.wikipedia.org/wiki/Punycode
.. _`ফাংশনটা OS অনুযায়ী আলাদাও হতে পারে` : https://en.wikipedia.org/wiki/Hosts_%28file%29#Location_in_the_file_system
.. _`OSI Model`: https://en.wikipedia.org/wiki/OSI_model
.. _`Ethernet`: http://en.wikipedia.org/wiki/IEEE_802.3
.. _`WiFi`: https://en.wikipedia.org/wiki/IEEE_802.11
.. _`Cellular data network`: https://en.wikipedia.org/wiki/Cellular_data_communication_protocol