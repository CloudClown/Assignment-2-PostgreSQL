## ১. PostgreSQL কী?

**PostgreSQL** হলো একটি relational এবং extensible database system যেটা completely open-source এবং খুবই শক্তিশালী ও feature-rich। এটাতে আমরা complex query চালাতে পারি এবং বড় বড় data handling এর জন্য খুবই উপযোগী। PostgreSQL JSON, indexing, এবং বিভিন্ন ধরনের advanced query support করে।

Indexing এর ক্ষেত্রে এটি B-tree, Hash, GIN, GiST ইত্যাদি algorithm ব্যবহার করে। এটি পুরোপুরি ACID compliant, যার মানে হলো —
- **A**tomicity (সব কিছু সম্পূর্ণ হবে বা কিছুই হবে না)
- **C**onsistency (data ঠিকমতো থাকবে)
- **I**solation (transaction গুলো আলাদা থাকবে)
- **D**urability (transaction complete হলে সেটা হারাবে না)

PostgreSQL এ table এবং column নামগুলো case sensitive, তবে আমরা সাধারণত lowercase এ লিখে থাকি।

---

## ২. PostgreSQL-এ Schema এর উদ্দেশ্য কী?

ধরো একটা বাড়ি, সেই বাড়িতে অনেকগুলো রুম আছে — প্রতিটা রুমে আলাদা আলাদা জিনিস থাকতে পারে, আবার একই জিনিসও থাকতে পারে। ঠিক সেরকমভাবেই **Schema** হলো database এর মধ্যে একেকটা আলাদা group বা namespace।

একই নামের table তুমি একই Schema-তে রাখতে পারবে না, কিন্তু ভিন্ন Schema-তে একই নামে table রাখা সম্ভব। এতে করে বড় systems এ data structure গুলোকে ভাগ করা যায়, যেমন — user data, admin data, archive data ইত্যাদি আলাদা Schema-তে রাখা যায়।

---

## ৩. PostgreSQL-এ Primary Key এবং Foreign Key এর ধারণা ব্যাখ্যা করো।

**Primary Key** হলো এমন একটি column (বা column গুলোর combination) যেটা প্রতিটি row কে unique করে। মানে, একটি table-এর প্রতিটি row আলাদা হয় এই key এর মাধ্যমে। Primary Key কখনও NULL বা duplicate হতে পারে না।

**Foreign Key** হলো এমন একটি column যেটা অন্য table-এর Primary Key এর সাথে সম্পর্ক তৈরি করে। এর মাধ্যমে দুটি table-এর মধ্যে connection বা relationship তৈরি হয়।

**উদাহরণ:**
`sightings` table-এ `ranger_id` হলো `rangers` table-এর Primary Key এর উপর নির্ভরশীল — এই `ranger_id` ই হলো Foreign Key।

---

## ৪. VARCHAR এবং CHAR ডেটা টাইপের মধ্যে পার্থক্য কী?

- **CHAR(n):** fixed length string। যদি তুমি CHAR(10) ব্যবহার করো এবং value দাও "Cat", তাহলে system বাকি ৭টা জায়গা space দিয়ে পূরণ করে দিবে।
- **VARCHAR(n):** variable length string। যদি তুমি VARCHAR(10) দাও এবং value দাও "Cat", তাহলে শুধু ওই তিনটা character ই system ধরে রাখবে।

**VARCHAR** সাধারণত বেশি ব্যবহার করা হয় কারণ এটা space-efficient এবং flexible।

---

## ৫. SELECT statement-এ WHERE clause-এর উদ্দেশ্য কী?

**WHERE** clause ব্যবহার করে আমরা নির্দিষ্ট condition অনুযায়ী data filter করতে পারি। পুরো table থেকে সব row না দেখিয়ে, শুধু যেগুলো প্রয়োজন সেটাই দেখায়।

**উদাহরণ:**
```sql
SELECT * FROM rangers WHERE region = 'Mountain Range';
