# CRM Database Structure  
## هيكل قاعدة بيانات CRM التفصيلي  
### منصة مجموعة الدخيل القابضة  
### Al Dakheel Holding Group

---

## 1. الهدف من هيكل قاعدة البيانات

هذا الملف يحدد البنية المقترحة لقاعدة بيانات نظام **CRM ولوحة التحكم الداخلية** الخاصة بمنصة **مجموعة الدخيل القابضة**.

الغرض منه أن يعرف المبرمج:

- ما الجداول المطلوبة؟
- ما الحقول داخل كل جدول؟
- كيف ترتبط الجداول ببعضها؟
- أين يتم حفظ بيانات العملاء؟
- كيف يتم حفظ الطلبات والاستفسارات؟
- كيف يتم ربط الطلب بالشركة والخدمة؟
- كيف يتم حفظ المواعيد والرسائل؟
- كيف يتم تتبع مصدر العميل؟
- كيف يتم إدارة الصلاحيات والمستخدمين؟
- كيف يتم استخراج التقارير؟

---

## 2. مبدأ التصميم العام

يجب بناء قاعدة البيانات بطريقة مرنة وقابلة للتوسع، بحيث يمكن مستقبلاً:

- إضافة شركات جديدة.
- إضافة خدمات جديدة.
- إضافة مستخدمين وصلاحيات.
- إضافة وكلاء ذكاء اصطناعي.
- إضافة قنوات تواصل جديدة.
- إضافة لغات جديدة.
- إضافة مراحل متابعة جديدة.
- إضافة تقارير متقدمة.

---

## 3. الكيانات الرئيسية في النظام

يتكون النظام من الكيانات التالية:

1. العملاء.
2. الشركات التابعة.
3. الخدمات.
4. الطلبات والاستفسارات.
5. حالات الطلب.
6. مصادر العملاء.
7. المواعيد.
8. الرسائل.
9. المحادثات.
10. المستخدمون.
11. الصلاحيات.
12. ملاحظات الطلبات.
13. الملفات والمرفقات.
14. سجلات النشاط.
15. وكلاء الذكاء الاصطناعي.
16. إعدادات النظام.

---

# القسم الأول: الجداول الأساسية

---

## 4. جدول الشركات التابعة  
### `companies`

هذا الجدول يحفظ بيانات الشركات التابعة للمجموعة.

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | رقم الشركة |
| `name_ar` | String | اسم الشركة بالعربية |
| `name_en` | String | اسم الشركة بالإنجليزية |
| `slug` | String | رابط مختصر للشركة |
| `description_ar` | Text | وصف الشركة بالعربية |
| `description_en` | Text | وصف الشركة بالإنجليزية مستقبلاً |
| `country` | String | الدولة |
| `city` | String | المدينة |
| `sector` | String | القطاع العام |
| `logo_url` | String | رابط شعار الشركة |
| `primary_color` | String | اللون الرئيسي |
| `secondary_color` | String | اللون الثانوي |
| `phone` | String | رقم الهاتف |
| `whatsapp` | String | رقم WhatsApp |
| `email` | String | البريد الإلكتروني |
| `address` | Text | العنوان |
| `map_url` | String | رابط الخريطة |
| `website_url` | String | رابط خارجي إن وجد |
| `status` | Enum | active / inactive |
| `sort_order` | Integer | ترتيب الظهور |
| `created_at` | DateTime | تاريخ الإنشاء |
| `updated_at` | DateTime | تاريخ التحديث |

### الشركات الأولية داخل الجدول

1. الوشاح للتجارة العامة.
2. Cross Border Business Advisory LTD.
3. أفق القوة التجارية.
4. دار الأخوة العامر للإسكان.

---

## 5. جدول الخدمات  
### `services`

هذا الجدول يحفظ جميع الخدمات التي تقدمها الشركات.

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | رقم الخدمة |
| `company_id` | Foreign Key | الشركة المرتبطة بالخدمة |
| `category_id` | Foreign Key | تصنيف الخدمة |
| `name_ar` | String | اسم الخدمة بالعربية |
| `name_en` | String | اسم الخدمة بالإنجليزية |
| `slug` | String | رابط مختصر للخدمة |
| `short_description_ar` | Text | وصف مختصر |
| `description_ar` | Long Text | وصف كامل |
| `target_audience_ar` | Text | الفئة المستهدفة |
| `requirements_ar` | Text | المتطلبات |
| `application_method_ar` | Text | طريقة التقديم |
| `icon_url` | String | أيقونة الخدمة |
| `featured_image_url` | String | صورة رئيسية |
| `status` | Enum | active / inactive |
| `sort_order` | Integer | ترتيب الظهور |
| `created_at` | DateTime | تاريخ الإنشاء |
| `updated_at` | DateTime | تاريخ التحديث |

---

## 6. جدول تصنيفات الخدمات  
### `service_categories`

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | رقم التصنيف |
| `name_ar` | String | اسم التصنيف بالعربية |
| `name_en` | String | اسم التصنيف بالإنجليزية |
| `slug` | String | رابط مختصر |
| `description_ar` | Text | وصف التصنيف |
| `icon_url` | String | أيقونة |
| `status` | Enum | active / inactive |
| `sort_order` | Integer | ترتيب الظهور |
| `created_at` | DateTime | تاريخ الإنشاء |
| `updated_at` | DateTime | تاريخ التحديث |

### التصنيفات الأولية

- التجارة العامة.
- الاستشارات التجارية.
- الاستيراد والتصدير.
- الإسكان والأراضي.

---

## 7. جدول العملاء  
### `customers`

هذا الجدول يحفظ بيانات جميع العملاء أو الزوار الذين أرسلوا طلبات.

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | رقم العميل |
| `full_name` | String | الاسم الكامل |
| `first_name` | String | الاسم الأول إن أمكن |
| `last_name` | String | اسم العائلة إن أمكن |
| `phone` | String | رقم الهاتف |
| `whatsapp` | String | رقم WhatsApp |
| `email` | String | البريد الإلكتروني |
| `country` | String | الدولة |
| `city` | String | المدينة |
| `preferred_contact_method` | Enum | call / whatsapp / email |
| `customer_type` | Enum | individual / company / investor / supplier / trader / other |
| `company_name` | String | اسم شركة العميل إن وجد |
| `job_title` | String | صفة العميل |
| `source_id` | Foreign Key | مصدر العميل |
| `language` | String | اللغة المفضلة |
| `notes` | Text | ملاحظات عامة |
| `status` | Enum | new / active / inactive / blocked |
| `created_at` | DateTime | تاريخ الإنشاء |
| `updated_at` | DateTime | تاريخ التحديث |
| `last_contact_at` | DateTime | آخر تواصل |
| `created_by` | Foreign Key | المستخدم الذي أضاف العميل |

### ملاحظة مهمة

يجب منع تكرار العملاء قدر الإمكان من خلال مقارنة:

- رقم الهاتف.
- WhatsApp.
- البريد الإلكتروني.

---

## 8. جدول الطلبات والاستفسارات  
### `requests`

هذا أهم جدول في النظام، لأنه يحفظ جميع الطلبات القادمة من الموقع أو WhatsApp أو الذكاء الاصطناعي.

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | رقم الطلب |
| `request_number` | String | رقم مرجعي للطلب |
| `customer_id` | Foreign Key | العميل صاحب الطلب |
| `company_id` | Foreign Key | الشركة المرتبطة بالطلب |
| `service_id` | Foreign Key | الخدمة المطلوبة |
| `category_id` | Foreign Key | قطاع الطلب |
| `source_id` | Foreign Key | مصدر الطلب |
| `assigned_to` | Foreign Key | المستخدم المسؤول |
| `status_id` | Foreign Key | حالة الطلب |
| `priority` | Enum | high / medium / normal |
| `request_type` | Enum | inquiry / quote / consultation / import_export / real_estate / appointment / general |
| `subject` | String | عنوان الطلب |
| `message` | Long Text | نص الطلب أو الاستفسار |
| `budget` | String | الميزانية التقريبية إن وجدت |
| `preferred_contact_time` | String | وقت التواصل المفضل |
| `preferred_contact_method` | Enum | call / whatsapp / email |
| `is_urgent` | Boolean | هل الطلب عاجل؟ |
| `ai_summary` | Text | ملخص الذكاء الاصطناعي إن وجد |
| `internal_notes` | Text | ملاحظات داخلية |
| `closed_reason` | Text | سبب الإغلاق |
| `created_at` | DateTime | تاريخ إنشاء الطلب |
| `updated_at` | DateTime | تاريخ آخر تحديث |
| `closed_at` | DateTime | تاريخ الإغلاق |

### مثال رقم طلب

`ADH-2026-0001`

---

## 9. جدول حالات الطلب  
### `request_statuses`

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | رقم الحالة |
| `name_ar` | String | اسم الحالة بالعربية |
| `name_en` | String | اسم الحالة بالإنجليزية |
| `code` | String | كود الحالة |
| `color` | String | لون الحالة |
| `sort_order` | Integer | ترتيب الحالة |
| `is_closed` | Boolean | هل هذه الحالة تعتبر إغلاقاً؟ |
| `created_at` | DateTime | تاريخ الإنشاء |
| `updated_at` | DateTime | تاريخ التحديث |

### الحالات الأولية

| الحالة | الكود |
|---|---|
| طلب جديد | `new` |
| قيد المراجعة | `under_review` |
| بيانات ناقصة | `missing_info` |
| تم التواصل | `contacted` |
| موعد مجدول | `scheduled` |
| عرض مرسل | `proposal_sent` |
| فرصة تجارية | `opportunity` |
| قيد التنفيذ | `in_progress` |
| مكتمل | `completed` |
| مغلق | `closed` |
| غير مهتم حالياً | `not_interested_now` |

---

## 10. جدول مصادر العملاء  
### `lead_sources`

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | رقم المصدر |
| `name_ar` | String | اسم المصدر بالعربية |
| `name_en` | String | اسم المصدر بالإنجليزية |
| `code` | String | كود المصدر |
| `description` | Text | وصف |
| `is_active` | Boolean | فعال أم لا |
| `created_at` | DateTime | تاريخ الإنشاء |
| `updated_at` | DateTime | تاريخ التحديث |

### المصادر الأولية

| المصدر | الكود |
|---|---|
| الموقع الإلكتروني | `website` |
| WhatsApp | `whatsapp` |
| Instagram | `instagram` |
| Facebook | `facebook` |
| LinkedIn | `linkedin` |
| QR Code | `qr_code` |
| حملة إعلانية | `campaign` |
| إحالة | `referral` |
| معرض | `exhibition` |
| اجتماع مباشر | `direct_meeting` |

---

# القسم الثاني: جداول النماذج المتخصصة

---

## 11. جدول تفاصيل طلب الاستيراد والتصدير  
### `import_export_details`

يرتبط بطلب من جدول `requests`.

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | الرقم |
| `request_id` | Foreign Key | الطلب المرتبط |
| `operation_type` | Enum | import / export / supplier_search / buyer_search |
| `product_type` | String | نوع المنتج |
| `quantity` | String | الكمية |
| `target_country` | String | الدولة المستهدفة |
| `origin_country` | String | دولة المنشأ |
| `has_supplier` | Boolean | هل يوجد مورد؟ |
| `has_buyer` | Boolean | هل يوجد مشتري؟ |
| `shipping_method` | String | طريقة الشحن |
| `expected_timeline` | String | المدة المتوقعة |
| `additional_notes` | Text | ملاحظات |
| `created_at` | DateTime | تاريخ الإنشاء |
| `updated_at` | DateTime | تاريخ التحديث |

---

## 12. جدول تفاصيل الطلبات العقارية  
### `real_estate_details`

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | الرقم |
| `request_id` | Foreign Key | الطلب المرتبط |
| `property_type` | Enum | land / housing / apartment / project / investment |
| `preferred_location` | String | الموقع المطلوب |
| `budget_range` | String | الميزانية |
| `payment_method` | String | طريقة الدفع |
| `purchase_purpose` | Enum | residence / investment / development / other |
| `preferred_contact_time` | String | وقت التواصل |
| `additional_notes` | Text | ملاحظات |
| `created_at` | DateTime | تاريخ الإنشاء |
| `updated_at` | DateTime | تاريخ التحديث |

---

## 13. جدول تفاصيل الاستشارات التجارية  
### `consultation_details`

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | الرقم |
| `request_id` | Foreign Key | الطلب المرتبط |
| `consultation_type` | Enum | expansion / partnership / market_study / cross_border / general |
| `business_sector` | String | القطاع التجاري |
| `target_market` | String | السوق المستهدف |
| `current_business_status` | Enum | existing_business / idea_stage / startup / other |
| `challenge_description` | Text | وصف التحدي أو الهدف |
| `preferred_meeting_method` | String | طريقة الاجتماع المفضلة |
| `additional_notes` | Text | ملاحظات |
| `created_at` | DateTime | تاريخ الإنشاء |
| `updated_at` | DateTime | تاريخ التحديث |

---

# القسم الثالث: المواعيد والرسائل والمحادثات

---

## 14. جدول المواعيد  
### `appointments`

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | رقم الموعد |
| `request_id` | Foreign Key | الطلب المرتبط |
| `customer_id` | Foreign Key | العميل |
| `company_id` | Foreign Key | الشركة |
| `assigned_to` | Foreign Key | الموظف المسؤول |
| `appointment_type` | Enum | business_meeting / consultation / follow_up / real_estate / import_export / management |
| `meeting_method` | Enum | phone / whatsapp / google_meet / zoom / in_person |
| `preferred_date` | Date | التاريخ المقترح |
| `preferred_time` | Time | الوقت المقترح |
| `confirmed_date` | Date | التاريخ المؤكد |
| `confirmed_time` | Time | الوقت المؤكد |
| `meeting_link` | String | رابط الاجتماع |
| `location` | String | الموقع إن كان حضورياً |
| `status` | Enum | requested / confirmed / completed / cancelled / rescheduled |
| `notes` | Text | ملاحظات |
| `created_at` | DateTime | تاريخ الإنشاء |
| `updated_at` | DateTime | تاريخ التحديث |

---

## 15. جدول الرسائل  
### `messages`

يحفظ الرسائل المرسلة للعملاء عبر Email أو WhatsApp أو SMS مستقبلاً.

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | رقم الرسالة |
| `customer_id` | Foreign Key | العميل |
| `request_id` | Foreign Key | الطلب المرتبط |
| `appointment_id` | Foreign Key | الموعد المرتبط |
| `channel` | Enum | email / whatsapp / sms / internal |
| `direction` | Enum | incoming / outgoing |
| `subject` | String | عنوان الرسالة |
| `body` | Long Text | نص الرسالة |
| `template_code` | String | كود القالب المستخدم |
| `status` | Enum | draft / sent / delivered / failed / read |
| `sent_at` | DateTime | وقت الإرسال |
| `delivered_at` | DateTime | وقت الوصول |
| `read_at` | DateTime | وقت القراءة |
| `created_by` | Foreign Key | المستخدم المرسل |
| `created_at` | DateTime | تاريخ الإنشاء |

---

## 16. جدول قوالب الرسائل  
### `message_templates`

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | الرقم |
| `name_ar` | String | اسم القالب |
| `code` | String | كود القالب |
| `channel` | Enum | email / whatsapp / sms |
| `subject` | String | عنوان البريد إن وجد |
| `body_ar` | Long Text | نص القالب |
| `variables` | JSON | المتغيرات مثل الاسم والتاريخ |
| `is_active` | Boolean | فعال أم لا |
| `created_at` | DateTime | تاريخ الإنشاء |
| `updated_at` | DateTime | تاريخ التحديث |

### قوالب أولية

- استلام طلب.
- طلب بيانات ناقصة.
- تأكيد موعد.
- تذكير موعد.
- متابعة بعد اجتماع.
- رسالة شكر.
- إغلاق طلب.

---

## 17. جدول المحادثات  
### `conversations`

يحفظ المحادثات مع العميل، سواء كانت عبر المساعد الذكي أو WhatsApp أو الموقع.

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | رقم المحادثة |
| `customer_id` | Foreign Key | العميل |
| `request_id` | Foreign Key | الطلب المرتبط |
| `channel` | Enum | website_chat / whatsapp / ai_agent / manual |
| `started_at` | DateTime | وقت البداية |
| `ended_at` | DateTime | وقت النهاية |
| `summary` | Text | ملخص المحادثة |
| `ai_agent_id` | Foreign Key | وكيل الذكاء الاصطناعي إن وجد |
| `status` | Enum | open / closed / transferred |
| `created_at` | DateTime | تاريخ الإنشاء |

---

## 18. جدول رسائل المحادثات  
### `conversation_messages`

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | رقم الرسالة |
| `conversation_id` | Foreign Key | المحادثة |
| `sender_type` | Enum | customer / ai_agent / user |
| `sender_id` | String | رقم المرسل إن وجد |
| `message_text` | Long Text | نص الرسالة |
| `message_type` | Enum | text / image / file / audio |
| `created_at` | DateTime | وقت الإرسال |

---

# القسم الرابع: المستخدمون والصلاحيات

---

## 19. جدول المستخدمين  
### `users`

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | رقم المستخدم |
| `full_name` | String | الاسم الكامل |
| `email` | String | البريد الإلكتروني |
| `phone` | String | الهاتف |
| `password_hash` | String | كلمة المرور المشفرة |
| `role_id` | Foreign Key | الصلاحية |
| `company_id` | Foreign Key | الشركة المرتبطة إن وجدت |
| `status` | Enum | active / inactive / suspended |
| `last_login_at` | DateTime | آخر دخول |
| `created_at` | DateTime | تاريخ الإنشاء |
| `updated_at` | DateTime | تاريخ التحديث |

---

## 20. جدول الأدوار  
### `roles`

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | رقم الدور |
| `name_ar` | String | اسم الدور |
| `name_en` | String | اسم الدور بالإنجليزية |
| `code` | String | كود الدور |
| `description` | Text | وصف |
| `created_at` | DateTime | تاريخ الإنشاء |
| `updated_at` | DateTime | تاريخ التحديث |

### الأدوار الأولية

- Super Admin.
- مدير المجموعة.
- مسؤول شركة.
- مسؤول خدمة العملاء.
- محرر محتوى.

---

## 21. جدول الصلاحيات  
### `permissions`

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | رقم الصلاحية |
| `name` | String | اسم الصلاحية |
| `code` | String | كود الصلاحية |
| `module` | String | القسم المرتبط |
| `description` | Text | وصف |
| `created_at` | DateTime | تاريخ الإنشاء |

### أمثلة صلاحيات

- عرض العملاء.
- تعديل العملاء.
- حذف العملاء.
- عرض الطلبات.
- تعديل الطلبات.
- تعيين الطلبات.
- عرض التقارير.
- إدارة الشركات.
- إدارة الخدمات.
- إدارة المستخدمين.
- إدارة المحتوى.

---

## 22. جدول ربط الأدوار بالصلاحيات  
### `role_permissions`

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | الرقم |
| `role_id` | Foreign Key | الدور |
| `permission_id` | Foreign Key | الصلاحية |
| `created_at` | DateTime | تاريخ الإنشاء |

---

# القسم الخامس: الملاحظات والملفات وسجل النشاط

---

## 23. جدول ملاحظات الطلبات  
### `request_notes`

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | رقم الملاحظة |
| `request_id` | Foreign Key | الطلب |
| `user_id` | Foreign Key | صاحب الملاحظة |
| `note` | Text | نص الملاحظة |
| `visibility` | Enum | internal / customer_visible |
| `created_at` | DateTime | تاريخ الإنشاء |

---

## 24. جدول المرفقات  
### `attachments`

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | الرقم |
| `related_type` | Enum | customer / request / company / service / appointment |
| `related_id` | UUID / Integer | رقم العنصر المرتبط |
| `file_name` | String | اسم الملف |
| `file_url` | String | رابط الملف |
| `file_type` | String | نوع الملف |
| `file_size` | Integer | حجم الملف |
| `uploaded_by` | Foreign Key | المستخدم الذي رفع الملف |
| `created_at` | DateTime | تاريخ الرفع |

---

## 25. جدول سجل النشاط  
### `activity_logs`

يحفظ كل العمليات المهمة داخل النظام.

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | الرقم |
| `user_id` | Foreign Key | المستخدم |
| `action` | String | نوع العملية |
| `module` | String | القسم |
| `related_type` | String | نوع العنصر |
| `related_id` | String | رقم العنصر |
| `description` | Text | وصف العملية |
| `ip_address` | String | عنوان IP |
| `user_agent` | String | معلومات المتصفح |
| `created_at` | DateTime | تاريخ العملية |

### أمثلة نشاط

- إنشاء طلب جديد.
- تغيير حالة طلب.
- تعيين طلب لموظف.
- إرسال رسالة.
- تسجيل دخول.
- تعديل بيانات عميل.
- حذف خدمة.
- رفع ملف.

---

# القسم السادس: وكلاء الذكاء الاصطناعي

---

## 26. جدول وكلاء الذكاء الاصطناعي  
### `ai_agents`

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | رقم الوكيل |
| `name_ar` | String | اسم الوكيل |
| `code` | String | كود الوكيل |
| `description` | Text | وصف عمل الوكيل |
| `agent_type` | Enum | receptionist / customer_service / sales_followup / appointment / real_estate / import_export / consultation |
| `status` | Enum | active / inactive |
| `created_at` | DateTime | تاريخ الإنشاء |
| `updated_at` | DateTime | تاريخ التحديث |

---

## 27. جدول ملخصات الذكاء الاصطناعي  
### `ai_summaries`

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | الرقم |
| `conversation_id` | Foreign Key | المحادثة |
| `request_id` | Foreign Key | الطلب |
| `ai_agent_id` | Foreign Key | الوكيل |
| `summary_text` | Text | ملخص المحادثة |
| `detected_intent` | String | نية العميل |
| `recommended_company_id` | Foreign Key | الشركة المقترحة |
| `recommended_service_id` | Foreign Key | الخدمة المقترحة |
| `confidence_score` | Decimal | درجة الثقة |
| `created_at` | DateTime | تاريخ الإنشاء |

---

# القسم السابع: إعدادات الموقع والمحتوى

---

## 28. جدول صفحات الموقع  
### `pages`

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | رقم الصفحة |
| `title_ar` | String | عنوان الصفحة |
| `title_en` | String | عنوان إنجليزي مستقبلاً |
| `slug` | String | رابط الصفحة |
| `content_ar` | Long Text | محتوى الصفحة |
| `meta_title_ar` | String | عنوان SEO |
| `meta_description_ar` | Text | وصف SEO |
| `featured_image_url` | String | صورة الصفحة |
| `status` | Enum | draft / published |
| `created_at` | DateTime | تاريخ الإنشاء |
| `updated_at` | DateTime | تاريخ التحديث |

---

## 29. جدول إعدادات النظام  
### `settings`

| الحقل | النوع المقترح | الوصف |
|---|---|---|
| `id` | Integer / UUID | الرقم |
| `key` | String | مفتاح الإعداد |
| `value` | Long Text | قيمة الإعداد |
| `group` | String | مجموعة الإعدادات |
| `type` | String | نوع القيمة |
| `updated_at` | DateTime | تاريخ التحديث |

### أمثلة إعدادات

- site_name_ar
- site_name_en
- main_domain
- main_phone
- main_whatsapp
- main_email
- instagram_url
- facebook_url
- linkedin_url
- google_analytics_id
- default_language

---

# القسم الثامن: العلاقات بين الجداول

---

## 30. العلاقات الرئيسية

### علاقة الشركات بالخدمات

- الشركة الواحدة يمكن أن تمتلك عدة خدمات.
- الخدمة الواحدة تتبع غالباً شركة واحدة.

العلاقة:

`companies.id` → `services.company_id`

---

### علاقة العميل بالطلبات

- العميل الواحد يمكن أن يرسل عدة طلبات.
- كل طلب يتبع عميلاً واحداً.

العلاقة:

`customers.id` → `requests.customer_id`

---

### علاقة الطلب بالشركة

- الطلب الواحد يمكن أن يرتبط بشركة واحدة.
- الشركة يمكن أن تستقبل عدة طلبات.

العلاقة:

`companies.id` → `requests.company_id`

---

### علاقة الطلب بالخدمة

- الطلب قد يرتبط بخدمة محددة.
- الخدمة يمكن أن يكون لها عدة طلبات.

العلاقة:

`services.id` → `requests.service_id`

---

### علاقة الطلب بالحالة

- كل طلب له حالة واحدة حالية.
- كل حالة يمكن أن تكون مستخدمة في عدة طلبات.

العلاقة:

`request_statuses.id` → `requests.status_id`

---

### علاقة الطلب بالمواعيد

- الطلب الواحد يمكن أن يكون له موعد أو أكثر.
- كل موعد يرتبط بطلب.

العلاقة:

`requests.id` → `appointments.request_id`

---

### علاقة الطلب بالرسائل

- الطلب يمكن أن يحتوي على عدة رسائل.
- كل رسالة قد ترتبط بطلب.

العلاقة:

`requests.id` → `messages.request_id`

---

### علاقة المستخدم بالطلبات

- المستخدم يمكن أن يكون مسؤولاً عن عدة طلبات.
- كل طلب يمكن تعيينه لمستخدم واحد.

العلاقة:

`users.id` → `requests.assigned_to`

---

# القسم التاسع: مخطط ERD نصي مبسط

```text
companies
  └── services
        └── requests
              ├── customers
              ├── request_statuses
              ├── lead_sources
              ├── appointments
              ├── messages
              ├── request_notes
              ├── attachments
              ├── import_export_details
              ├── real_estate_details
              └── consultation_details

customers
  ├── requests
  ├── appointments
  ├── messages
  └── conversations

conversations
  ├── conversation_messages
  └── ai_summaries

users
  ├── roles
  ├── requests assigned_to
  ├── request_notes
  └── activity_logs

roles
  └── role_permissions
        └── permissions

ai_agents
  ├── conversations
  └── ai_summaries
```

---

# القسم العاشر: بيانات أولية Seed Data

---

## 31. الشركات الأولية

| الاسم العربي | الاسم الإنجليزي | القطاع | الدولة |
|---|---|---|---|
| الوشاح للتجارة العامة | Al Wasah General Trading L.L.C | تجارة عامة | الإمارات |
| Cross Border Business Advisory LTD | Cross Border Business Advisory LTD | استشارات تجارية |  |
| أفق القوة التجارية | Power Horizon Trading Company | استيراد وتصدير | الأردن |
| دار الأخوة العامر للإسكان | Dar Al Okhwa Al Amer Housing | إسكان وأراضي | الأردن |

---

## 32. الخدمات الأولية

| الخدمة | الشركة | التصنيف |
|---|---|---|
| خدمات التجارة العامة | الوشاح | التجارة العامة |
| الاستشارات التجارية العابرة للحدود | Cross Border | الاستشارات التجارية |
| خدمات الاستيراد والتصدير | أفق القوة التجارية | الاستيراد والتصدير |
| خدمات الإسكان والأراضي | دار الأخوة العامر | الإسكان والأراضي |

---

## 33. حالات الطلب الأولية

| الحالة | كود الحالة | لون مقترح |
|---|---|---|
| طلب جديد | new | أزرق |
| قيد المراجعة | under_review | بنفسجي |
| بيانات ناقصة | missing_info | برتقالي |
| تم التواصل | contacted | سماوي |
| موعد مجدول | scheduled | كحلي |
| عرض مرسل | proposal_sent | ذهبي |
| فرصة تجارية | opportunity | أخضر |
| قيد التنفيذ | in_progress | أزرق داكن |
| مكتمل | completed | أخضر داكن |
| مغلق | closed | رمادي |
| غير مهتم حالياً | not_interested_now | أحمر خفيف |

---

## 34. مصادر العملاء الأولية

| المصدر | الكود |
|---|---|
| الموقع الإلكتروني | website |
| WhatsApp | whatsapp |
| Instagram | instagram |
| Facebook | facebook |
| LinkedIn | linkedin |
| QR Code | qr_code |
| حملة إعلانية | campaign |
| إحالة | referral |
| معرض | exhibition |
| اجتماع مباشر | direct_meeting |

---

## 35. الأدوار الأولية

| الدور | الكود |
|---|---|
| مدير النظام | super_admin |
| مدير المجموعة | group_manager |
| مسؤول شركة | company_manager |
| مسؤول خدمة العملاء | customer_service |
| محرر محتوى | content_editor |

---

# القسم الحادي عشر: قواعد عمل مهمة

---

## 36. قواعد منع تكرار العملاء

عند وصول طلب جديد، يجب فحص وجود العميل مسبقاً عبر:

1. رقم الهاتف.
2. رقم WhatsApp.
3. البريد الإلكتروني.

إذا وجد العميل:

- يتم ربط الطلب الجديد بنفس العميل.
- يتم تحديث `last_contact_at`.
- يتم عدم إنشاء عميل مكرر.

---

## 37. قواعد إنشاء رقم الطلب

يفضل إنشاء رقم طلب تلقائي بهذا الشكل:

```text
ADH-YYYY-0001
```

مثال:

```text
ADH-2026-0001
ADH-2026-0002
ADH-2026-0003
```

---

## 38. قواعد توزيع الطلبات

يمكن توزيع الطلب تلقائياً حسب نوع الخدمة:

| نوع الطلب | الشركة المقترحة |
|---|---|
| تجارة عامة | الوشاح |
| استشارة تجارية | Cross Border |
| استيراد وتصدير | أفق القوة التجارية |
| عقار أو أرض | دار الأخوة العامر |
| تواصل إداري | الإدارة العامة |

---

## 39. قواعد الأولوية

### أولوية عالية

- طلب واضح ومكتمل.
- عميل يطلب اجتماعاً قريباً.
- طلب تجاري مهم.
- طلب استثماري.
- طلب عقاري بميزانية واضحة.

### أولوية متوسطة

- طلب واضح لكنه يحتاج تفاصيل إضافية.
- عميل مهتم ولم يحدد موعداً.
- استفسار قابل للتحول إلى فرصة.

### أولوية عادية

- سؤال عام.
- طلب غير مكتمل.
- عميل غير جاهز حالياً.

---

## 40. قواعد إغلاق الطلب

لا يتم إغلاق أي طلب إلا بعد:

- تسجيل سبب الإغلاق.
- تسجيل آخر إجراء.
- تحديد هل يحتاج متابعة مستقبلية.
- حفظ ملاحظة داخلية.
- تحديث تاريخ الإغلاق.

---

# القسم الثاني عشر: توصيات تقنية

---

## 41. توصيات عامة للمبرمج

- استخدام UUID إن كان النظام سيكبر مستقبلاً.
- استخدام Soft Delete للجداول المهمة بدلاً من الحذف النهائي.
- تفعيل Audit Logs.
- تشفير كلمات المرور.
- حماية بيانات العملاء.
- فهرسة الحقول كثيرة البحث مثل:
  - phone
  - email
  - request_number
  - status_id
  - company_id
  - created_at
- فصل الصلاحيات بوضوح.
- جعل الحالات والمصادر قابلة للتعديل من لوحة التحكم.
- دعم اللغة الإنجليزية مستقبلاً من خلال حقول `name_en` و `description_en`.

---

## 42. أقل نسخة CRM يمكن البدء بها MVP

إذا أردنا بداية بسيطة، يمكن البدء بالجداول التالية فقط:

1. `companies`
2. `services`
3. `customers`
4. `requests`
5. `request_statuses`
6. `lead_sources`
7. `users`
8. `roles`
9. `request_notes`
10. `appointments`

ثم إضافة لاحقاً:

- messages.
- conversations.
- AI summaries.
- attachments.
- advanced reports.

---

# 43. الخلاصة

بهذا الملف أصبح لدى المبرمج تصور واضح لقاعدة بيانات CRM تشمل:

- الشركات.
- الخدمات.
- العملاء.
- الطلبات.
- الحالات.
- المصادر.
- المواعيد.
- الرسائل.
- المحادثات.
- المستخدمين.
- الصلاحيات.
- المرفقات.
- سجل النشاط.
- وكلاء الذكاء الاصطناعي.
- إعدادات الموقع.

## الخطوة التالية المقترحة

بعد اعتماد هيكل قاعدة البيانات، الخطوة التالية الأفضل هي إعداد:

# User Stories & Acceptance Criteria  
## قصص المستخدم ومعايير القبول

لأنها ستحوّل كل المتطلبات إلى سيناريوهات عملية يستطيع المبرمج وفريق الاختبار تنفيذها والتحقق منها.